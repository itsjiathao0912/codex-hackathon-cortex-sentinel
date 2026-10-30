# Business Requirements Document — Cortex Sentinel MVP

Version: 1.0 · Date: 2026-10-31 (Asia/Ho_Chi_Minh)

Status: implementation-ready proposal for stakeholder review, not production authorization. Language: English. Owner: product team; named business sponsor and technical owner remain to be assigned.

## 1. Executive decision

Build a bounded autonomous investigation layer on the existing transaction/use-case engine, serving ShopeePay risk and fraud analysts across ShopeePay and ShopeePayLater. Demonstrate it with synthetic data, a detailed Ho Chi Minh City map, separate configuration and case workspaces, and measurable, approval-controlled adaptation.

The commercial/business hypothesis is that evidence gathering and repeated low-value investigation consume analyst attention. This has not yet been validated through interviews or operational data. Existing public Alipay/WeChat Pay research supports layered controls and governance, not the effectiveness of this particular solution.

The MVP must demonstrate actual runtime investigation and an evaluation result. A polished wireframe or hardcoded improvement is not sufficient to claim completion of the Autonomous & Adaptive AI track objective.

## 2. Current state and problem

The user reports that ingestion and use-case configuration already exist. Their API, data completeness, throughput and integration availability have not been verified. The repository currently contains an interactive wireframe: street map, four navigation sections, mock cases, simulated configuration testing and feedback. It does not contain the production capability implied by these screens.

Analysts need to understand which alerts are connected, what evidence supports or contradicts suspicion, what the agent did while unattended, and when a human must intervene. Investigation quality must not be traded away merely to reduce the number of alerts.

## 3. Stakeholders and responsibilities

| Stakeholder | Responsibility / decision |
|---|---|
| Risk analyst | Inspect cases, acknowledge escalations, record evidence-based dispositions |
| Risk lead | Own routing policy, approve configuration/adaptation, authorize rollback |
| Product owner | Approve business scope, demo claims and acceptance evidence |
| Engineering owner | Verify engine contract, implement reliability and access boundaries |
| Evaluation reviewer | Review fixture labels and critical cases; assess outputs independently of the generation prompt |
| Hackathon judges | Assess demonstrated value, autonomy, adaptation and build quality |

One person may perform multiple roles in a hackathon, but role changes and approval events must be explicit; no claim of independent approval where the same person performed both roles.

## 4. Business objectives and measures

| ID | Objective | Measure and MVP acceptance |
|---|---|---|
| BO-01 | Reduce repeated evidence gathering | Compare rules-only, fixed-enrichment and agent workflows on the same frozen cases; report analyst review time including corrections |
| BO-02 | Investigate reliably without continuous supervision | Five complete replay runs finish or explicitly enter Needs review; critical failure scenarios never disappear or become cleared |
| BO-03 | Preserve important fraud signals | Every designated critical fraud fixture escalates; report missed fraud and unresolved cases across all labeled fixtures |
| BO-04 | Demonstrate useful adaptation | A scoped candidate reduces at least one false escalation on the frozen evaluation set without increasing missed fraud; otherwise report no validated gain and retain baseline |
| BO-05 | Make decisions inspectable | Every assessment supplies evidence references and unknowns; every disposition/policy change has actor, time and version |
| BO-06 | Support geographic investigation | HCMC street map and list remain consistent; source/uncertainty visible; cases without location remain accessible |

These are proposed hackathon acceptance targets, not observed outcomes, production SLAs or statistical guarantees. Do not reuse the wireframe's illustrative 20→12 result as measurement. If BO-04 fails, the evaluation workflow may be complete but the adaptive-benefit objective is not achieved.

## 5. Business scope

### Included in the release

- Synthetic accounts, merchants, transactions, device/network associations and historical reviewed cases.
- Three seeded use cases: merchant coordination, location anomalies, shared-device clusters; one flagship coordinated-merchant investigation with the same generic tool workflow supporting the others.
- Reuse of the existing engine through a verified adapter, or a clearly labeled synthetic adapter if access is unavailable.
- Asynchronous investigation, relationship queries, counter-evidence checks, bounded recovery, consolidated case creation and internal escalation.
- Four sections: Map, Configuration, Risk cases, Activity log.
- Analyst decisions, scoped adaptation proposal, real replay evaluation, explicit approval, versioning and rollback.
- A reproducible demonstration, measured evaluation results, and honest limitations.

### Excluded

Real customer data; production payment execution; automatic payment declines, freezes or credit decisions; AML regulatory submissions; sanctions screening programs; full AML compliance coverage; all-city administrative-boundary certification; a trained GNN; a new streaming feature store; continuous online model retraining; external email/SMS delivery; global-map navigation; map relationship lines.

## 6. Business rules

1. An alert, suspicious assessment, confirmed fraud disposition and money-laundering finding are different concepts. The MVP does not determine legal guilt.
2. Missing evidence routes to review. Low priority is not automatic clearance or case closure.
3. The model may investigate and recommend; deterministic policy decides permitted routing. Only an authorized human can activate policy changes.
4. Shared IP, geographic distance or delinquency alone cannot establish fraud. Authorized borrowing is not sham cash-out.
5. HCMC is the map/demo scope, not an evidence boundary: related out-of-area activity remains visible in case evidence.
6. Map display filters do not modify detection rules. Browser hiding or filtering cannot change backend authorization.
7. Analyst feedback is a reviewed observation, not unquestionable ground truth. Only validated decisions become retrieval context; evaluation labels remain separate.
8. No application secret or sensitive account data is embedded in map-provider URLs or browser model calls.

## 7. Business journey

Select existing monitor → inspect HCMC map or case list → agent gathers evidence asynchronously → policy routes a consolidated case → analyst acknowledges/reviews → reasoned disposition is stored → candidate adjustment is evaluated → lead approves or rejects → version activates or baseline remains → rollback available.

Configuration editing is a separate optional journey: select configuration → edit draft → run replay → inspect results → approve/apply → monitor. There is no mandatory setup wizard before viewing seeded data.

## 8. Research justification

[Alipay research](../research/alipay-wechat-bnpl/alipay-findings.md) documents merchant/identity controls and group-level AML claims with source limits. [WeChat research](../research/alipay-wechat-bnpl/wechat-findings.md) documents real-time transaction assessment, device/network processing purposes and governance. Neither proves this product's graph model, LLM autonomy or false-positive reduction. Chinese contract/regulatory context is not asserted as a Vietnamese compliance determination.

The [feasibility report](Solution-feasibility-report.md) supports proceeding with a supervised sandbox vertical slice. Maps aid orientation; evidence-backed triage is the differentiating capability.

## 9. Assumptions, dependencies and risks

| Item | Working assumption / response | Owner |
|---|---|---|
| Existing engine access | Verify schema and adapter before implementation; disclose synthetic fallback | Engineering |
| Team/time budget | Unknown; prioritize P0 in PRD, cut P1/P2 before weakening evidence gates | Product |
| Analyst access | Seek 2–3 analysts; label teammates as proxy participants if needed | Product |
| LLM availability | Backend credentials and budget available; timeout yields explicit review | Engineering |
| Data labels | Synthetic labels reviewed before evaluation; ring/time leakage prevented | Evaluation |
| Map provider | Network and usage terms apply; map outage does not block list workflow | Engineering |
| Feedback poisoning / error | Scoped candidates, review, held-out test, audit and rollback | Risk lead |
| Overstated claims | Separate implemented, simulated, measured and planned features | Product |

## 10. Business acceptance and handover

Release requires all P0 acceptance criteria in the PRD, recorded baseline/candidate results, critical failure handling, one reproducible reset/run procedure and reviewable audit/evidence artifacts. No approved improvement claim is made if the adaptive evaluation fails. A non-improving candidate must still be rejectable in the demo.

Handover includes source commit, fixture manifest, configuration/model/prompt versions, evaluation report with raw counts and timings, known limitations, and a six-minute demonstration script. Business approval does not authorize production financial actions.

## 11. After the hackathon

A pilot needs real analyst interviews, access/legal review, validated labels, persistent access controls and operational monitoring. Define a timeboxed shadow-mode study before intervention on real transactions. Forecast analyst savings only from measured task-time changes and realistic task frequency; no ROI or loss-prevention claim is supported today.
