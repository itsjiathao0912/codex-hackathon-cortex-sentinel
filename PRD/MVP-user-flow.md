# Cortex Sentinel: proposed MVP scope and user flow

**Date:** 2026-10-31 (Asia/Ho_Chi_Minh)
**Status:** Proposal for discussion before formal BRD and PRD
**Track:** Autonomous & Adaptive AI
**Primary users:** ShopeePay risk and fraud analysts
**Product coverage:** ShopeePay and ShopeePayLater

## 1. Intent and existing context

An existing engine already ingests data and configures detection use cases. The proposed MVP adds an AI investigation layer and an analyst workspace. It monitors candidate alerts, investigates connected activity, escalates high-risk cases while analysts are away, and uses reasoned analyst feedback to improve future triage.

The hackathon uses mock transactions, accounts, merchants, devices, IP locations, and analyst decisions. The flagship scenario is coordinated merchant abuse. AML-relevant relationship and money-flow evidence can support investigation, but this is not a complete AML compliance system and does not determine that money laundering has occurred.

The central demonstration is: **the agent discovers a connected ring, assembles an evidence-backed case, escalates it, and avoids repeating an unnecessary escalation after a tested analyst correction.**

## 2. Proposed scope

### Included

- Reuse the existing ingestion and use-case configuration engine.
- Select a synthetic dataset and validate required identifiers and timestamps.
- Configure evidence checks, graph expansion, investigation budgets, and escalation routing.
- Run a labeled replay before activating sandbox monitoring.
- Investigate candidate alerts asynchronously, group related alerts, and create consolidated cases.
- Inspect observed facts, counter-evidence, unknowns, graph relationships, location context, and investigation history.
- Capture analyst dispositions and explanations.
- Retrieve relevant reviewed decisions for subsequent investigations.
- Propose narrowly scoped policy adjustments; evaluate, approve, version, and roll them back.
- Surface failures, incomplete investigations, paused work, and escalation delivery status.

### Excluded

- Real payment blocking, account freezing, or credit decisions.
- Regulatory reporting or full AML program coverage.
- Autonomous activation of learned policy changes.
- Automatic closure based on low confidence or missing evidence.
- Production throughput, latency, detection accuracy, or loss-prevention claims.
- A newly built streaming feature-store platform.
- A trained GNN unless later justified by suitable labeled data and comparison against a baseline.

Relationship queries and a network visualization are in scope; neither should be described as a trained GNN. The OpenAI API investigation layer is proposed functionality, not connected in the wireframe.

## 3. Full user journey

### Step 1 — Select data and the existing use case

**User action:** Open an existing use case and select the hackathon sandbox dataset.

**System response:** Check transaction ID, event timestamp, product, amount/currency, account, merchant, device, IP, and relationship integrity. Identify optional unavailable evidence.

**Proposed default:** Coordinated merchant abuse, covering both products.

**Completion:** Required data checks pass and the use case is selected. Missing required fields block activation. Missing optional data remains visible as a limitation.

### Step 2 — Configure the investigator

**User action:** Choose evidence checks and graph expansion depth.

**Proposed defaults:** Transaction velocity, shared devices, merchant concentration, reviewed-case retrieval, optional IP-location checks, two-hop expansion, and a maximum of three minutes or twelve tool calls per case. These numbers are design assumptions to validate, not agreed service levels.

**System response:** Save an investigation configuration with explicit limits. Budget exhaustion produces an incomplete case requiring review, never a benign determination.

**Completion:** A saved draft defines the evidence available to the investigator and its operating limits.

### Step 3 — Define autonomy and escalation

**User action:** Set escalation priority, destination, acknowledgment deadline, and backup owner.

**Proposed defaults:** High priority, Risk operations queue, acknowledgment within fifteen minutes, then escalation to Risk lead.

**Allowed automatically:** Enrichment, relationship expansion, alert grouping, case drafting, and routing within the configured policy.

**Approval required:** Activation of learned changes to triage policy.

**Excluded actions:** Freezing accounts, blocking payments, and filing regulatory reports.

**Completion:** Save a versioned draft. The wireframe uses named priority levels; precise scoring and threshold semantics remain a PRD decision.

### Step 4 — Validate with historical replay

**User action:** Run a labeled mock replay against the saved configuration.

**System response:** Show actual fraud escalated, legitimate cases escalated, missed fraud, and failure-routing checks. Keep evaluation cases separate from the historical decisions used for retrieval or adaptation.

**Proposed illustrative gates:** At least 18 of 20 fraud cases escalated, at most 20 of 80 legitimate cases escalated, and incomplete-evidence routing preserved.

**Completion:** Passing gates enables explicit sandbox activation. Failed gates return the analyst to configuration. These acceptance gates demonstrate a workflow; they are not adequate proof of production safety or generalization.

### Step 5 — Activate and monitor

**User action:** Activate sandbox monitoring, inspect exceptions, or pause/resume new investigations.

**System response:** Display the active policy, feed/tool health, processed volume, consolidated cases, escalations, and investigation activity. The existing engine handles transaction detection; the AI layer performs asynchronous investigation.

**Main questions answered:** What needs attention? Is the agent operating correctly? What has it done?

**Failure behavior:** Queue new investigations while paused. Retry transient enrichment failures within a bounded budget. Preserve failed checks and route unresolved cases for review. Record escalation delivery failure separately from successful delivery and acknowledgment. Re-escalate overdue cases to the backup owner.

**Completion:** The analyst can understand unattended work and identify cases requiring intervention.

### Step 6 — Investigate a consolidated case

**User action:** Open a case and inspect evidence, graph, location, and timeline views.

**Evidence:** Separate observed facts, model assessments, counter-evidence, and unknowns. Material claims link to supporting mock transaction or session records.

**Graph:** Show accounts, merchants, devices, IPs, and payment relationships with time-bounded connections. Shared infrastructure is evidence to examine, not proof of guilt. Beneficial ownership and settlement destinations must not be inferred when absent from the dataset.

**Location:** Separate approximate IP geolocation from merchant registered address. Show source, observation time, accuracy radius, and unavailable evidence. Do not imply exact person tracking or infer impossible travel from IP alone.

**Timeline:** Show actions, queried evidence, retries, policy version, routing, and delivery status. This is an operational trace and evidence summary, not private model chain-of-thought.

**Completion:** The analyst has enough evidence to make a disposition or request additional investigation.

### Step 7 — Record the analyst decision

**User action:** Select Confirmed fraud, Legitimate activity, or Insufficient evidence, and supply a reason.

**System response:** Store the disposition, evidence context, reviewer, timestamp, and applicable version. Confirmed/legitimate cases can be resolved; insufficient-evidence cases stay open. Resolution does not authorize a financial action.

**Completion:** A traceable reviewed decision becomes available as context. Analyst decisions are fallible labels and should not be treated as unconditional ground truth.

### Step 8 — Evaluate and approve an improvement

**User action:** Review an agent-proposed scoped adjustment and compare it against the current policy.

**Example:** Reduce the weight of a known public-IP association only where devices are independent, velocity is ordinary, and timing is not coordinated. Preserve escalation for stronger corroborating signals. Avoid a blanket IP allowlist.

**System response:** Evaluate the candidate on held-out labeled cases. Show both false escalations and missed fraud, not analyst agreement alone. Version the candidate, record approval, and provide expiry/review and rollback behavior.

**Completion:** An analyst approves activation or rejects the candidate. Approval is required even when illustrative metrics improve. The MVP demonstrates retrieval and policy adaptation; it does not imply that an API model automatically retrains on feedback.

## 4. Screen structure

| Workspace | Primary content | Main action |
| --- | --- | --- |
| Configure | Data, use case, investigation checks, autonomy limits | Save draft |
| Validate | Replay cohort, acceptance gates, comparison results | Activate sandbox |
| Monitor | Prioritized cases, agent activity, health, policy version | Open case / pause |
| Investigate | Evidence, graph, location, timeline, decision form | Save disposition |
| Improve | Proposed adjustment, comparison, scope and guardrails | Approve / roll back |
| Activity log | Configuration, investigation, decision and approval events | Inspect history |

The dashboard prioritizes exceptions rather than making a map the primary navigation. Geography is contextual evidence for the selected case.

## 5. Synthetic data and demo scenarios

Suggested mock inventory: 10,000 transactions, 500 accounts, 40 merchants, 700 devices, 120 IP records, and 120 historical analyst decisions. These are proposed seed sizes shown in the wireframe, not a generated dataset included with it. Use separate historical-context, held-out evaluation, and live-simulation partitions. Use a single currency (VND) for the first demo to avoid misleading aggregation.

### Scenario A — Coordinated merchant ring

Six accounts pay two merchants in a short window. Three accounts share a device; the other accounts connect through payments to the same merchants. The agent groups twelve alerts, checks corroborating timing and transaction evidence, and escalates one case. The displayed VND 48,000,000 is observed volume, not confirmed fraud loss or money saved.

### Scenario B — Legitimate shared-IP activity

Eight accounts share a public IP but use independent devices and show ordinary payment behavior. The analyst records a reasoned legitimate disposition. A scoped candidate reduces unnecessary escalation without suppressing stronger device or timing signals.

The illustrative replay has 100 labeled cases: 20 fraud and 80 legitimate. Both versions escalate 18 fraud cases and miss 2; false escalations fall from 20 to 12. The 40% reduction is scripted demonstration data, not measured model performance. False-positive rate changes from 20/80 to 12/80; this differs from the fraction of escalated cases that are false.

### Scenario C — Enrichment outage

An IP enrichment check fails and bounded retries are exhausted. The case remains incomplete and available for analyst review. Missing evidence does not turn into a clearance decision.

## 6. Wireframe fidelity and limitations

[Open the wireframe source/download](wireframe.html).

The standalone HTML is a throwaway interaction prototype. It supports configuration navigation, replay and activation, mock scenario selection, pause/resume, evidence tabs, decision capture, a scripted learning comparison, approval, rollback, and an activity log.

It does not implement the full requirements described above. Specifically, it has one current case rather than a persistent queue; no backend ingestion, schema validation, model calls, actual graph computation, real geolocation basemap, notification delivery, acknowledgment workflow, automatic expiry, authentication, or production audit storage. Replay numbers are fixed examples and do not recompute with configuration changes. A fresh policy-edit workflow after activation is described but not implemented. The prototype simulates these concepts to support scope and UX discussion.

## 7. Decisions to settle in the BRD and PRD

- Hackathon duration, team capacity, and existing engine integration contract.
- Exact risk-priority definition and policy activation authority.
- Final data schema, entity resolution, investigation windows, and mock labeling method.
- Investigation latency, cost, retry, and work-queue limits.
- Definition of case resolution, escalation acknowledgment, and reopening.
- Adaptation mechanism, minimum evidence, evaluation gates, drift checks, and expiry.
- Whether a trained GNN adds demonstrable value beyond graph queries.

The approved flow will feed the BRD's business outcomes and scope, and the PRD's detailed requirements, states, data contracts, acceptance criteria, and measurement plan.
