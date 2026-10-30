# Architecture rationale — MVP implementation decisions

[Tiếng Việt](vi/Architecture-rationale.md) · English

Date: 2026-10-31. English companion to [Implementation-design.md](Implementation-design.md). The [PRD](PRD.md) is the current target-behavior contract; this document explains why the choices fit the MVP. The earlier Vietnamese technical design remains background, not proof of implementation.

## Current implementation versus target

| Capability | Current repository artifact | Required implementation |
|---|---|---|
| HCMC map and four sections | Working HTML prototype, Leaflet and live tiles | API-backed cases, permissions, stable refresh |
| Configuration replay/apply | Fixed illustrative result and in-memory version | Dataset-backed replay, hashes, role checks, durable versions |
| AI investigation | Not implemented in the wireframe | Backend worker, read-only tools, validated model output |
| Escalation | Mock text/status | Durable outbox, internal delivery, acknowledgment and backup |
| Feedback/adaptation | Scripted comparison and UI state | Reviewed context, real held-out evaluation, approval and rollback |
| Audit | In-memory events | Durable append-only application events with actor and versions |

## Decision record

| Decision | Why this choice | Alternative deferred / trade-off | Validation |
|---|---|---|---|
| Reuse existing detector; investigate asynchronously | Keeps model latency/failure off payment authorization; builds on reported engine investment | Inline LLM scoring risks a payment bottleneck; async cannot stop already completed payments | Measure queue wait and investigation time; disclose no blocking |
| One agent with bounded read-only tools | Demonstrates autonomous next-step choice with a small inspectable permission surface | Multi-agent orchestration adds coordination cost before evidence of benefit | Compare agent against fixed enrichment, inspect tool decisions |
| Rules own routing; model proposes assessment | Separates stochastic judgment from execution authority; preserves high-risk baseline signals | Model-direct routing is simpler but harder to constrain/audit | Reject invalid output; test preserved critical signals |
| Relational association queries before GNN | Fixture-scale relationships do not require model training or new graph infrastructure | GNN may help later but needs labels, training and comparative evidence | Ablate graph expansion against baseline |
| Reviewed precedent and scoped policy adaptation | Can demonstrate learning without retraining; reversible and explainable | Fine-tuning/online learning needs more data and label-quality controls | Holdout improvement plus missed-fraud gate |
| Durable database jobs and outbox | Small deployable architecture with transactionally linked case and delivery records | A separate broker is useful at scale but not necessary for a small sandbox | Crash/retry and duplicate delivery tests |
| Leaflet HCMC street map | Already implemented, supports detail and warm neutral rendering; no world map or lines needed | 3D/vector platform adds scope; raster tiles depend on network/provider | Location provenance, keyboard/list fallback, tile outage tests |
| Separate configuration/cases/log sections | Matches explicit user correction; avoids overloading the map | Single-screen workspace reduces navigation but increased clutter in prior design | Observe analysts completing map and configuration tasks |
| Polling before SSE | Straightforward refresh and recovery for modest demo volume | SSE reduces polling overhead but adds reconnect/state handling | Verify stable selection/pan and bounded polling errors |
| Three independent state machines | Investigation completion, case disposition and escalation delivery are different facts | One status field creates ambiguous states such as delivered=resolved | State-transition fixtures and audit checks |

## Runtime data path

Browser → authenticated application API → database and job queue → worker → allowlisted evidence tools → external model → output validator → deterministic router → case and outbox → analyst UI.

Only synthetic, minimized evidence leaves the application in the MVP. API credentials remain server-side. Transaction text is untrusted tool data. The model never receives an arbitrary database connection, credentials, unrestricted URL tool or account-action capability.

Map tiles are a separate browser-to-provider path carrying viewport requests, not case IDs. Maintain attribution and provider caching/referrer requirements; use stubbed tiles in automated tests. Provider availability and terms must be reviewed for a real deployment; no production SLA is inferred from public OSM access.

## Reconciliation with earlier design

The 8-call limit in the PRD counts retries within the total. A 30-second deadline includes tool retries; it does not include time waiting in the queue. Configuration defaults in the PRD replace the older illustrative 3-minute/12-call wireframe assumptions. Case state, investigation state and delivery state are separate, replacing the earlier shorthand combined lifecycle.

The map is HCMC-only while authorized evidence lookup can include connected out-of-area activity. A bbox is a viewing constraint, not a verified administrative polygon or evidence exclusion rule. No map point is fabricated when location is unknown.

## What would change these decisions?

- Proven throughput/queue pressure may justify a broker or streaming feature service.
- A trained GNN must beat a fair baseline on independently labeled held-out groups before becoming a dependency.
- Measured polling load or latency may justify SSE.
- Demonstrated geospatial ambiguity or provider limitations may justify vector tiles, clustering or a contracted/private provider.
- Production use requires a separate readiness review; completing a hackathon demo does not authorize real financial intervention.
