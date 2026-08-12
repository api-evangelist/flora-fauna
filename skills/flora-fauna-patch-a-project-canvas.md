---
generated: '2026-08-12'
name: Read and patch a FLORA project canvas
method: generated
description: Retrieve a project's canvas as a Mermaid flowchart, apply a Mermaid diff to add or connect nodes, add a prebuilt action node, and run it.
api: openapi/flora-fauna-flora-api-openapi.yml
operations: [getProject, listCanvasNodes, getProjectCanvas, patchProjectCanvas, listActions, getAction, createCanvasAction, runCanvasAction]
source: >-
  Grounded in openapi/flora-fauna-flora-api-openapi.yml (Flora.ai API v1.6.0). All
  eight operationIds verified verbatim in the spec. Mermaid representation and the
  "call search_docs first" caution per https://developer.flora.ai/mcp/tools.
---

# Read and patch a FLORA project canvas

The most unusual surface in the Flora.ai API, and the one most suited to an agent: the project canvas is exposed as a **Mermaid flowchart**, read whole and modified with a Mermaid diff. The node graph that is the product's core data structure is manipulated as diagram text.

## Auth
- `Authorization: Bearer sk_live_...`. Base URL `https://app.flora.ai/api/v1`.

## Steps

1. **Open the project** — `getProject` (`GET /projects/{projectId}`) with a `prj_`-prefixed id.

2. **Read the graph** — `getProjectCanvas` (`GET /projects/{projectId}/canvas`) returns the canvas topology as a Mermaid flowchart. Read it before writing anything; you are diffing against this exact text.

   `listCanvasNodes` (`GET /projects/{projectId}/nodes`) gives the same graph as an enumerable node list — better when you need to address one node by `node_id` rather than reason about the shape.

3. **Patch the graph** — `patchProjectCanvas` (`PATCH /projects/{projectId}/canvas`) with a `diagram` (the Mermaid diff that adds or connects nodes) and optional `node_params` for per-node parameter overrides. Because this is a diff over text, re-read the canvas in step 2 immediately before patching; do not patch against a stale render.

4. **Add a prebuilt action node** — `listActions` (`GET /actions`) and `getAction` (`GET /actions/{actionId}`) enumerate the deterministic editing tools (rotate, crop, and similar), addressed by human slug such as `rotate-image` — **not** by a prefixed id. Then `createCanvasAction` (`POST /projects/{projectId}/actions`) with `action_id` and optional `params` places one on the canvas.

5. **Run the action node** — `runCanvasAction` (`POST /projects/{projectId}/actions/{nodeId}/run`) executes an existing canvas action node. For a headless run that does not touch the canvas, use `createActionRun` (`POST /runs/action`) instead — the spec states direct action runs do not create or mutate canvas nodes.

## Notes
- FLORA's own documentation flags the canvas and action methods as the newest part of the surface and tells agents to call `search_docs` for exact argument shapes before writing code against them. Treat the shapes here as the contract, but expect drift.
- Action parameters are validated against a per-action schema (added in SDK 0.9.0), so a wrong param value fails rather than being ignored.
- Canvas edits are visible to humans working in FLORA in real time. This is a shared surface — patch narrowly.

## Errors
- `400 input_validation_error` — most often a malformed Mermaid diff or a `node_params` key that does not match a node in the diagram.
- `404 not_found` — the `node_id` was resolved from a stale canvas read. Re-read and retry.
- `403 forbidden` — the key's workspace role does not allow modifying projects.

See `errors/flora-fauna-problem-types.yml`, `data-model/flora-fauna-data-model.yml` and `conventions/flora-fauna-conventions.yml`.
