---
generated: '2026-08-12'
name: Upload a local file and use it as a Technique input
method: generated
description: Reserve a signed upload, push the bytes, mark the asset complete, attach it to a project canvas, and pass it into a run.
api: openapi/flora-fauna-flora-api-openapi.yml
operations: [uploadAsset, completeAssetUpload, retryAssetUpload, getAsset, listAssets, attachCanvasAsset]
source: >-
  Grounded in openapi/flora-fauna-flora-api-openapi.yml (Flora.ai API v1.6.0). All
  six operationIds verified verbatim in the spec. Flow per
  https://developer.flora.ai/recipes/upload-an-asset and
  https://developer.flora.ai/guides/assets.
---

# Upload a local file and use it as a Technique input

FLORA runs accept media only as HTTPS URLs on an allowlisted host. To use a local file you first turn it into a FLORA Asset. This is a three-step signed upload with an explicit completion step — the middle step is not a FLORA API call at all.

## Auth
- `Authorization: Bearer sk_live_...`. Base URL `https://app.flora.ai/api/v1`.

## Steps

1. **Reserve the upload** — `uploadAsset` (`POST /assets`). `source` is a string: `"signed-url"` to reserve a slot for local bytes, or an allowlisted HTTPS URL to have FLORA fetch it directly. Send `idempotency_key` — a duplicate reservation is a wasted slot. Capture the returned `asset_id` (`asset_`-prefixed) and the signed upload URL.

2. **Upload the bytes** — a plain `PUT`/`POST` to the signed URL. **This is not a FLORA API endpoint** and does not take your API key; it is a presigned storage URL with its own expiry. An agent needs shell or filesystem access to do this (curl/fetch on the raw bytes).

3. **Mark it complete** — `completeAssetUpload` (`POST /assets/{assetId}/complete`). Until this lands, the asset is not usable as a run input.

4. **Recover from an expired slot** — `retryAssetUpload` (`POST /assets/{assetId}/retry`) issues a fresh signed reservation for a failed or expired upload. Only call it on an asset that actually failed — retrying a healthy asset returns `409 conflict`.

5. **Confirm state** — `getAsset` (`GET /assets/{assetId}`) before using it, or `listAssets` (`GET /assets?workspace_id=ws_...`) to find one you uploaded earlier. Always check state before acting: `409 conflict` is the contract's way of saying you called the wrong transition.

6. **Attach it to a canvas (optional)** — `attachCanvasAsset` (`POST /projects/{projectId}/assets/{assetId}/attach`) places a ready asset on the project canvas as a static media node, so a human sees it in FLORA alongside the generated work.

7. **Use it in a run** — pass the asset's URL as the `value` of a Technique input whose `type` is `imageUrl` / `videoUrl` / `audioUrl` / `documentUrl`.

## Notes
- Bounded concurrency: FLORA's own guidance for 50+ files is about 4 uploads in parallel to stay under the unpublished rate limit.
- Agents without terminal access (web chat clients) cannot perform step 2 and can only use media that already lives at an HTTPS URL.
- Output URLs from previous runs are valid inputs and are the cheapest way to iterate — no re-upload needed while they still resolve.

## Errors
- `409 conflict` — completing an already-complete asset, or retrying one that did not fail. `GET /assets/{assetId}` first.
- `400 input_validation_error` on `source` — it is a string (`"signed-url"` or an allowlisted HTTPS URL), not an object.
- `404 not_found` — the asset belongs to a different workspace than the key.

See `errors/flora-fauna-problem-types.yml` and `data-model/flora-fauna-data-model.yml`.
