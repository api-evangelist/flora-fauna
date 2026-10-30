# FLORA

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

FLORA is a Brooklyn, New York-based applied AI / HCI company building a browser-based "infinite canvas" creative workspace for professional creators. Founded in 2024 by Weber Wong out of NYU's Interactive Telecommunications Program (ITP), FLORA unifies 50+ third-party text, image, and video AI models inside a single node-based visual workspace where designers, filmmakers, photographers, and creative agencies wire prompts, references, characters, and outputs into reusable generative workflows called Techniques. The platform integrates leading image models (FLUX.2, FLUX Kontext, Stable Diffusion 3.5, Nano Banana, Recraft, Seedream, Minimax Hailuo) and video models (Veo 3, Sora 2, Runway Gen-4 Turbo / Gen-3 Alpha / Act-Two, Pika, Kling, Luma Ray 2, Seedance, Marey) alongside reasoning models such as Gemini 3 Pro and GPT-5.4, and ships a creative agent named FAUNA for ideation, iteration, and workflow scaffolding. FLORA is used at agencies and studios including Pentagram, Milk, and MSCHF; the company raised a $6.5M seed led by Mike Volpi at Hanabi Capital with Menlo Ventures, a16z Games Speedrun, Long Journey Ventures, Company Ventures, Alumni Ventures, Embedding VC, and angels including Justin Kan (Twitch) and Gabe Whaley (MSCHF), and operates in-person from the Domino Refinery in Williamsburg. Beyond the canvas FLORA now ships a public developer surface: the Flora.ai REST API (OpenAPI 3.1.1, base https://app.flora.ai/api/v1) for running Techniques, one-off generations, assets, projects, canvas patches and actions programmatically; a hosted remote MCP server at https://agents.flora.ai/mcp exposing two tools (search_docs, execute) over OAuth 2.1 + PKCE; first-party TypeScript and Go SDKs and a Go CLI; signed HMAC-SHA256 run webhooks; idempotency keys; and a Stainless-generated developer portal at developer.flora.ai. API and MCP access begin on the paid Starter plan.

**Areas:** Creative AI · Generative AI · Infinite Canvas · Node-Based Workflows · Creative Workspace · Image Generation · Video Generation · AI Agents · Multimodal AI · Design Tools · Creative Professionals · FAUNA

## FLORA on APIs.io

Everything profiled for FLORA is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/flora-fauna/](https://apis.io/providers/flora-fauna/)** — or go straight to one of the APIs or properties below.

### APIs (12)

- [FLORA MCP Server](https://apis.io/apis/flora-fauna/flora-mcp/) — FLORA's hosted remote Model Context Protocol server. Streamable HTTP at https://agents.flora.ai/mcp, authenticated with OAuth 2.1 + PKCE (RFC 8414…
- [FLORA Actions API](https://apis.io/apis/flora-fauna/flora-fauna-actions-api/) — Prebuilt action catalog endpoints.
- [FLORA Assets API](https://apis.io/apis/flora-fauna/flora-fauna-assets-api/) — Asset upload and retrieval endpoints.
- [FLORA Canvas API](https://apis.io/apis/flora-fauna/flora-fauna-canvas-api/) — Project canvas endpoints.
- [FLORA Feedback API](https://apis.io/apis/flora-fauna/flora-fauna-feedback-api/) — Product feedback endpoints.
- [FLORA Generations API](https://apis.io/apis/flora-fauna/flora-fauna-generations-api/) — Generation endpoints.
- [FLORA Models API](https://apis.io/apis/flora-fauna/flora-fauna-models-api/) — Model catalog endpoints.
- [FLORA Projects API](https://apis.io/apis/flora-fauna/flora-fauna-projects-api/) — Project management endpoints.
- [FLORA Runs API](https://apis.io/apis/flora-fauna/flora-fauna-runs-api/) — Top-level run creation endpoints.
- [FLORA Technique Runs API](https://apis.io/apis/flora-fauna/flora-fauna-technique-runs-api/) — Nested technique run endpoints.
- [FLORA Techniques API](https://apis.io/apis/flora-fauna/flora-fauna-techniques-api/) — Technique catalog endpoints.
- [FLORA Workspaces API](https://apis.io/apis/flora-fauna/flora-fauna-workspaces-api/) — Workspace discovery endpoints.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Flora Fauna Webhooks](https://apis.io/asyncapis/flora-fauna/flora-fauna-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [flora](https://apis.io/servers/flora-fauna/flora/)

#### Collections (1)

Postman and Open Collection request collections.

- [Flora.ai API](https://apis.io/collections/flora-fauna/open-flora-fauna-flora-api/)

#### Overlays (12)

OpenAPI overlays, including conversational phrasing for each operation.

- [Flora Fauna Actions Api Phrasing Overlay](https://apis.io/overlays/flora-fauna/flora-fauna-actions-api-phrasing-overlay/)
- [Flora Fauna Assets Api Phrasing Overlay](https://apis.io/overlays/flora-fauna/flora-fauna-assets-api-phrasing-overlay/)
- [Flora Fauna Canvas Api Phrasing Overlay](https://apis.io/overlays/flora-fauna/flora-fauna-canvas-api-phrasing-overlay/)
- [Flora Fauna Feedback Api Phrasing Overlay](https://apis.io/overlays/flora-fauna/flora-fauna-feedback-api-phrasing-overlay/)
- [Flora Fauna Flora Api Overlay](https://apis.io/overlays/flora-fauna/flora-fauna-flora-api-overlay/)
- [Flora Fauna Generations Api Phrasing Overlay](https://apis.io/overlays/flora-fauna/flora-fauna-generations-api-phrasing-overlay/)
- [Flora Fauna Models Api Phrasing Overlay](https://apis.io/overlays/flora-fauna/flora-fauna-models-api-phrasing-overlay/)
- [Flora Fauna Projects Api Phrasing Overlay](https://apis.io/overlays/flora-fauna/flora-fauna-projects-api-phrasing-overlay/)
- [Flora Fauna Runs Api Phrasing Overlay](https://apis.io/overlays/flora-fauna/flora-fauna-runs-api-phrasing-overlay/)
- [Flora Fauna Technique Runs Api Phrasing Overlay](https://apis.io/overlays/flora-fauna/flora-fauna-technique-runs-api-phrasing-overlay/)
- [Flora Fauna Techniques Api Phrasing Overlay](https://apis.io/overlays/flora-fauna/flora-fauna-techniques-api-phrasing-overlay/)
- [Flora Fauna Workspaces Api Phrasing Overlay](https://apis.io/overlays/flora-fauna/flora-fauna-workspaces-api-phrasing-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Flora Fauna Authentication](https://apis.io/security/flora-fauna/flora-fauna-authentication/)
- [Flora Fauna Domain Security](https://apis.io/security/flora-fauna/flora-fauna-domain-security/)
- [Flora Fauna Trust Center](https://apis.io/security/flora-fauna/flora-fauna-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Flora Fauna Scopes](https://apis.io/scopes/flora-fauna/flora-fauna-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Flora Fauna Plans Pricing](https://apis.io/plans/flora-fauna/flora-fauna-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Flora Fauna Rate Limits](https://apis.io/rate-limits/flora-fauna/flora-fauna-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.florafauna.ai)
- [Documentation](https://docs.flora.ai)
- [Getting started](https://developer.flora.ai/api)
- [API reference](https://developer.flora.ai/reference/resources/techniques)
- [Pricing](https://flora.ai/pricing)
- [Sign up](https://app.flora.ai)
- [Blog](https://flora.ai/blog)
- [Terms of service](https://flora.ai/legal/terms-of-service)
- [Privacy policy](https://docs.flora.ai/legal/privacy-policy)
- [GitHub](https://github.com/florafauna-ai)
- [Status](https://status.flora.ai)

## API Evangelist rating

**Kin Score 67.3** — exemplar · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 58.8 |
| Contract governance | 18.2 |
| Operational transparency | 42.1 |
| Developer ergonomics | 70.8 |
| Access clarity | 92.1 |

**Agent readiness 63.2** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | verified |
| Auth Clarity | served (partial credit) |
| Idempotency | verified |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | na |
| Operation Distinctiveness | distinct |

**Regulatory alignment 36.4** — AI & Biometrics

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/flora-fauna/](https://apis.io/providers/flora-fauna/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for FLORA: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/flora-fauna/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
