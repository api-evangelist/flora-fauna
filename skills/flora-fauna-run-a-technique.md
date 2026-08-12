---
generated: '2026-08-12'
name: Run a FLORA Technique and collect its outputs
method: generated
description: Discover a saved FLORA Technique, read its input contract and per-run cost, start a run idempotently, poll to a terminal state, and read the output URLs.
api: openapi/flora-fauna-flora-api-openapi.yml
operations: [listTechniques, getTechnique, startTechniqueRun, getTechniqueRun]
source: >-
  Grounded in openapi/flora-fauna-flora-api-openapi.yml (Flora.ai API v1.6.0). All
  four operationIds verified verbatim in the spec. Conventions per
  conventions/flora-fauna-conventions.yml, errors per
  errors/flora-fauna-problem-types.yml, entity graph per
  data-model/flora-fauna-data-model.yml.
---

# Run a FLORA Technique and collect its outputs

The core FLORA flow. A Technique is a saved generative workflow authored in FLORA's visual canvas; the API runs it by slug or `tech_` id. It cannot create or edit one.

## Auth
- `Authorization: Bearer sk_live_...` on every request. See `authentication/flora-fauna-authentication.yml`.
- Base URL: `https://app.flora.ai/api/v1`.
- Requires a paid plan — Starter or above. The Free plan has no API access.

## Steps

1. **Find the Technique** — `listTechniques` (`GET /techniques`). Supports `query`, `workspace_id`, `cursor` and `limit`. If you already know the slug from the app URL `https://app.flora.ai/techniques/{slug}`, skip to step 2.

2. **Read its input contract and price** — `getTechnique` (`GET /techniques/{techniqueId}`). Accepts either the `tech_`-prefixed id or the slug. Returns `technique_id`, `name`, `description`, `run_cost` (USD per run), and the `inputs[]` / `outputs[]` arrays. **Do this before every run you have not run before.** Each input carries `id`, `name` and `type` (`text` | `imageUrl` | `videoUrl` | `audioUrl` | `documentUrl`), and your request must match every `id` and `type` exactly or you get `input_validation_error`.

3. **Check the budget before you spend it** — `run_cost` is the price of the call you are about to make, in dollars, deducted from the workspace budget. If you are about to fan out over a list, multiply first. A run that cannot be paid for fails with `402 insufficient_credits`.

4. **Start the run idempotently** — `startTechniqueRun` (`POST /techniques/{techniqueId}/runs`). Body:
   - `inputs`: array of `{ id, type, value }` matching step 2. Media values must be **HTTPS** URLs on an allowlisted host (FLORA media, GCS, S3, ImageKit) — `http://` is rejected.
   - `mode`: `"async"` (or `"stream"`).
   - `idempotency_key`: **always set this.** A duplicate run is a duplicate charge. Derive the key deterministically from the work itself (`q3-thumb-{market}`, `import-row-{row_hash}`), never from `uuidv4()` or `Date.now()` inside the retry loop.
   - `callback_url` (optional): an HTTPS endpoint for a signed `run.completed` / `run.failed` webhook instead of polling. See `asyncapi/flora-fauna-webhooks.yml`.

   Capture `run_id` and `poll_url` from the response.

5. **Poll to a terminal state** — `getTechniqueRun` (`GET /techniques/{techniqueId}/runs/{runId}`). Every 2–5 seconds. `status` walks `pending` → `running` → `completed` | `failed`, with `progress` 0–100.

6. **Read the outputs** — on `completed`, `outputs[]` holds `{ output_id, type, url }` and `charged_cost` holds what you actually paid. **Download anything you need to keep.** FLORA states output URLs are long-lived but not permanent.

## Critical: HTTP 200 does not mean the run succeeded

A run that starts fine returns HTTP 200 and can still terminate as `status: "failed"`, carrying `error_code` and `error_message`. Runs do **not** auto-retry. Branch on the run status, not the HTTP status:

- `model_timeout` — transient, retry.
- `safety_blocked` — the model refused; change the prompt, do not retry as-is.
- `input_unreachable` — a media URL could not be fetched; check the URL and the host allowlist.
- `internal_error` — retry with backoff.

## Errors
- `400 input_validation_error` — read the `fields[]` array; re-fetch the Technique with `getTechnique` and rebuild `inputs` rather than guessing.
- `402 insufficient_credits` — workspace budget exhausted. Stop the batch; do not spin.
- `404 not_found` — wrong slug, or the run was created in a different workspace than the key you are polling with.
- `429 rate_limited` — back off exponentially; honour `retry-after` when present, default to 5s when it is not, and drop batch concurrency to about 2. FLORA publishes no numeric limits.
- Capture the `request-id` response header on every call. Support generally cannot find a request without it.

See `errors/flora-fauna-problem-types.yml` for the full catalog.
