---
generated: '2026-08-12'
name: Generate directly from a model, without a saved Technique
method: generated
description: Pick a model from the FLORA catalog, start a one-off image/video/audio/text generation in a project, and poll the run to completion.
api: openapi/flora-fauna-flora-api-openapi.yml
operations: [listWorkspaces, listProjects, listModels, startGeneration, createGenerationRun, getRun]
source: >-
  Grounded in openapi/flora-fauna-flora-api-openapi.yml (Flora.ai API v1.6.0). All
  six operationIds verified verbatim in the spec. Model parameter semantics from
  https://developer.flora.ai/guides/generations and
  https://developer.flora.ai/mcp/tools.
---

# Generate directly from a model, without a saved Technique

When there is no saved Technique to run — a plain prompt against one of the 50+ models FLORA fronts.

## Auth
- `Authorization: Bearer sk_live_...`. Base URL `https://app.flora.ai/api/v1`. Starter plan or above.

## Steps

1. **Resolve the workspace** — `listWorkspaces` (`GET /workspaces`). Returns `{ workspace_id, name, role, created_at }`. `workspace_id` is `ws_`-prefixed and required by the generation call. If the key only has one workspace, this is a one-time lookup.

2. **Resolve the project** — `listProjects` (`GET /projects?workspace_id=ws_...`), or `createProject` (`POST /projects`) if the work needs its own canvas. Generations land on a project canvas, so `project_id` (`prj_`-prefixed) is part of the request.

3. **Pick the model** — `listModels` (`GET /models?type=image`). `type` is optional and filters the catalog. Each entry carries `model_id`, `name`, `provider`, `type`, `estimated_credits`, `estimated_seconds`, and a `params[]` array of `{ name, required, type, default, min, max, options }`. **That `params[]` array is the real parameter contract for the model** — the OpenAPI cannot describe it because it varies per model. Read it before constructing `params`.

4. **Start the generation** — `startGeneration` (`POST /generate`). Body: `type` (`image` | `video` | `audio` | `text` — not `t2i`, not `text-to-image`), `prompt`, `workspace_id`, `project_id`, optional `model` (a `model_id` string from step 3), optional `params` (model-specific, per step 3), optional `callback_url`, and `idempotency_key`. Returns `run_id` plus `charged_cost` / `estimated_seconds`.

   `createGenerationRun` (`POST /runs/generation`) is the flat-resource equivalent. Note that FLORA's own sources disagree about which family is canonical — the spec calls `/runs/*` the normalized top-level resource while the SDK changelog calls `/runs/*` deprecated. Prefer `POST /generate`, which every published example uses. See `lifecycle/flora-fauna-lifecycle.yml`.

5. **Poll** — `getRun` (`GET /runs/{runId}`). Same terminal-state contract as a Technique run: `pending` → `running` → `completed` | `failed`, with `outputs[]`, `charged_cost`, or `error_code` / `error_message`.

## Notes
- `estimated_credits` and `estimated_seconds` from `listModels` let you budget a fan-out before spending anything. Failed generations are not charged.
- Prefer a saved Technique when one exists: it pins the model, the parameters and the prompt scaffolding, and its `run_cost` is exact rather than estimated.
- Every mutating call here spends real money against the shared workspace pool. Always send `idempotency_key`.

## Errors
- `400 input_validation_error` on `type` is the single most common failure — use the bare enum value.
- `400 input_validation_error` on `model` — pass the `model_id` string from `listModels`, not a display name.
- `402 insufficient_credits` — workspace balance too low; stop and top up.
- `429 rate_limited` — reduce concurrency; see `rate-limits/flora-fauna-rate-limits.yml`.

See `errors/flora-fauna-problem-types.yml` and `conventions/flora-fauna-conventions.yml`.
