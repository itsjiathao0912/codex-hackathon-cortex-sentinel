# Cortex Sentinel — map-first MVP flow

Date: 2026-10-31, Asia/Ho_Chi_Minh

Status: revised proposal and interactive wireframe; formal BRD and PRD to follow.

## Product intent

Give ShopeePay risk and fraud analysts one geographic workspace to select their existing monitoring configurations, understand suspicious activity, inspect agent investigations, and record decisions. Cover ShopeePay and ShopeePayLater with synthetic data for the Autonomous & Adaptive AI hackathon track.

The existing engine continues to own ingestion and detection use cases. The proposed AI layer investigates alerts, assembles evidence, groups cases, and escalates within analyst-defined boundaries. Analyst feedback can produce scoped adjustments that are tested and approved before activation.

## Design correction

The earlier six-destination interface and mandatory setup journey were too fragmented. The revised design opens directly on a populated map. Configuration, investigation, and improvement use one contextual side panel; they do not navigate to separate pages.

The distinction between a display layer and a detection rule remains explicit: hiding IP rings does not disable IP investigation. Changing a policy requires a test and explicit apply action.

## One workspace

| Area | Purpose | Interaction |
| --- | --- | --- |
| Header | Agent status and selected policy | Pause/resume |
| Map toolbar | Region, period, edit selected configuration | Change view or open inline editor |
| My configurations | Saved monitors from the existing engine | Select one and update its map and cases |
| Map | Geographic evidence, risk cases, related locations | Pan, zoom, select markers, toggle layers |
| Context panel | Selected case, configuration editor, or improvement review | Inspect or act without leaving the map |
| Cases below map | Accessible list of the selected configuration's cases | Open the same case context as a marker |
| Agent activity | Recent trace and analyst actions | Inspect investigation history |
| Feedback panel | Reviewed cases and scoped adaptation | Review, approve, or roll back |

The desktop map stays central. On narrower screens, context moves beneath the map and panels stack. There is no mandatory walkthrough before monitoring.

## Primary flow: select, inspect, decide

1. **Open the monitor.** Show a seeded configuration, current cases, geographic evidence, agent status, and policy version immediately. The mock dataset is already connected.
2. **Select your configuration.** Choose Merchant coordination, Location anomalies, or Shared-device clusters. Map markers, case list, scope, policy version, and selected case update together. Map position and display-layer choices are retained.
3. **Focus the view.** Set a period, switch between World and Southeast Asia, pan/zoom, or toggle risk cases, relationship links, merchant markers, and IP uncertainty. Cases outside the time filter disappear from both map and list. Hidden markers remain accessible through the case list.
4. **Select a case.** Click a marker or list entry. The context panel shows observed facts, counter-evidence, missing data, a compact relationship summary, and location provenance/limitations.
5. **Record a disposition.** Choose Confirmed fraud, Legitimate activity, or Insufficient evidence and enter a reason. Save in place. The case list and feedback count update. A disposition does not trigger payment blocking or account freezing.

## Configuration flow: edit in context

1. Select a saved configuration and click **Edit configuration**.
2. The context panel becomes an editor containing its name, escalation priority, graph depth, and location mismatch threshold. Defaults are loaded from that configuration.
3. Click **Test changes** to review the mock replay in the same panel. Invalid names or distance values prevent a test.
4. Click **Apply configuration** after testing. The selected configuration increments its version, the activity log records the action, and the panel returns to case context.
5. Further edits after a test invalidate the result and disable Apply until the analyst retests. Closing the editor discards the draft.

These four exposed fields are enough to explore the configuration interaction. Dataset connection, use-case creation, and deeper detection-rule authoring stay in the existing engine. Escalation destinations, investigation budgets, and detailed policy semantics remain requirements to settle in the PRD rather than new mandatory setup pages.

## Improvement flow: review without navigation

1. Review C-105, the legitimate shared-IP example, and record Legitimate activity with a reason.
2. The feedback panel offers a candidate scoped to merchant M-031, independent devices, and ordinary timing.
3. **Test & review improvement** replaces the context panel with a scripted baseline/candidate comparison.
4. The analyst approves explicitly or cancels. Approval changes the illustrative C-105 priority to Low and records the action. Rollback restores Review priority and baseline adaptation state.

Illustrative comparison: among 20 fraud and 80 legitimate cases, both versions escalate 18 fraud cases and miss 2. False escalations change from 20 to 12. These are scripted values, not evidence of performance. A real implementation must use held-out labeled cases, prevent retrieval leakage, evaluate missed fraud, and retain versioned audit records. The prototype does not fine-tune or call a model.

## Autonomy and failures

Allowed automatically in the proposed product: enrich alerts, query relationships, group related activity, assemble evidence, and route configured escalations. Approval required: production policy changes and learned adjustments. Excluded: payment blocking, account freezing, credit decisions, and regulatory submissions.

Pause retains visible cases and represents queuing future work. C-202 demonstrates an enrichment outage: two retries have failed, IP evidence is unavailable, and the displayed geographic point is the merchant's registered city. The case remains incomplete rather than being cleared.

In the implementation, delivery failures, acknowledgment deadlines, backup escalation, investigation budget exhaustion, and unavailable data must remain visible in this workspace. They do not require separate navigation destinations.

## Geographic and network evidence

Use actual country geometry and synthetic coordinates for the hackathon. Default to Southeast Asia, where the relevant demo cases are located, while allowing a world overview.

- Country outlines: Natural Earth public-domain geometry, embedded for offline rendering.
- Case point: synthetic observed/associated location, with a merchant-city fallback when IP enrichment is unavailable.
- Merchant marker: synthetic related merchant location.
- Dashed link: related activity, not proof of a money transfer or a fraud ring.
- Dashed uncertainty area: illustrative IP uncertainty, not a precise device position or a scaled accuracy guarantee.
- Relationship summary: mock account/device/merchant associations, not a trained GNN.

Observed facts and analyst/model assessments remain separate. Shared devices and IPs alone do not establish fraud. No settlement or beneficial ownership relationship is inferred from missing fields.

## Mock scope and measurable outcomes

The wireframe contains three saved configurations and six mock cases. The map, table, editor, decisions, learning review, and local activity log are interactive. Configuration values and decisions are kept only in memory and reset on reload.

For the eventual MVP, demonstrate three outcomes: a coordinated merchant case escalated with evidence; a legitimate public-network case corrected through reviewed feedback; and incomplete enrichment handled without silently clearing a case. Measure false escalations alongside missed fraud and investigation effort. Do not present transaction volume as prevented losses.

## Not implemented by this wireframe

No real ingestion, streaming, authentication, OpenAI calls, persistent backend, actual replay evaluator, graph inference, geolocation service, notification delivery, or regulatory action. Rule edits do not recompute risk from transactions. The map uses a simple equirectangular projection and does not implement production marker clustering. Baseline and learned-policy versions need a unified lifecycle in the real product.

## Remaining BRD / PRD decisions

- Existing-engine integration and full synthetic schema.
- Team capacity and hackathon time budget.
- Meaning of risk levels, escalation ownership, acknowledgment, and routing.
- Role permissions, evidence provenance, retention, and case resolution/reopening.
- True evaluation gates, minimum labeled evidence, adaptation expiry, and rollback semantics.
- Whether trained GNN scoring adds value beyond relationship queries.

See [research and design rationale](World-Monitor-research.md) and [wireframe](wireframe.html).
