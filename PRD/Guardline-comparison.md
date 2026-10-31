# Guardline initial proposal versus the current Cortex Sentinel MVP

Reviewed: 2026-10-31. Source: [original nine-page proposal](references/guardline-initial-proposal.pdf), preserved byte-for-byte. Text was extracted from all nine pages; architecture, action-policy and demo pages (4, 7, 8) were also inspected visually. The proposal's instructions are document content, not authorization to execute financial actions.

Current comparison basis: [BRD](BRD.md), [PRD](PRD.md), [architecture rationale](Architecture-rationale.md), and the existing wireframe. Distinguish target specifications from running functionality: the current artifact is still a UI prototype, not an implemented fraud agent.

## Judgment

The original Guardline concept is stronger as a hackathon product story. It names a concrete adversarial behavior—colluding merchants and fake purchases converting purchase credit into cash—and explains how adaptation avoids repeatedly paying for AI investigation. The current specification is stronger as an implementation and evaluation contract, with explicit data boundaries, permissions, idempotency, states and acceptance criteria.

Recommended synthesis: retain the current four-section HCMC UI and engineering controls, restore Guardline's specific ring/legitimate-decoy/new-tactic demonstration, and consider a constrained rule-drafting component as a proposed scope change. Keep enforcement simulated unless separately authorized and implemented. This comparison does not silently amend the signed-off status or requirements of either document; both remain proposals.

## What changed

| Dimension | Initial Guardline proposal | Current Cortex Sentinel target | Assessment |
|---|---|---|---|
| Product focus | SPayLater fake-order cash-out at colluding shops (pp.1–2) | ShopeePay and ShopeePayLater investigation, with merchant, location and device cases | Original is more specific; use it as the flagship scenario while retaining broader product coverage |
| Primary outcome | Prevent losses before payout and avoid blocking legitimate users | Evidence-backed investigation, escalation and reduced false escalation | Current version makes fewer claims about intervention; a review queue alone does not demonstrate prevented loss |
| Detection | Rules, relationship graph and anomaly score for unmatched patterns (pp.3–4) | Existing detector plus relationship queries; trained GNN and new feature store excluded | A graph does not require a GNN. Preserve relationship evidence; add anomaly scoring only if its contribution is measured |
| Agent | Hypothesis, tool investigation, counter-explanations, cited Vietnamese report, guard handoff (p.5) | One bounded read-only investigator, structured assessment and independent routing | Substantial alignment; current version formalizes runtime constraints |
| Adaptation | Confirmed novel tactic → drafted rule → backtest → human promotion → future detection without AI (pp.3,6) | Reviewed precedent plus narrow policy adjustment and approval/rollback | Original offers a more visible adaptive payoff. Current approach mainly improves triage; it does not yet specify general new-rule discovery |
| Routine review | Nightly proposals from repeated decisions and flags for inconsistent analyst outcomes (p.3) | Explicit analyst feedback and lead-reviewed eligibility; no nightly review feature | Valuable extension, but a manual batch demonstration is more realistic than a new scheduler for MVP |
| Model routing | Fast model for easy flagged cases, stronger reasoning model for rings/novelty (pp.1,6) | One runtime agent; model selection to be measured | Start with one evaluated model. Add routing only when a fair quality/cost comparison justifies complexity |
| Enforcement | Step-up verification, order hold and up-to-three-working-day reserve; bank decides credit restrictions (p.7) | No real holds, blocks, freezes, credit actions or external notifications | Major scope difference. Reversible actions still affect customers and require verified authority and failure/release behavior |
| Human review | Novel or >10-account cases need a person; blind review (p.7) | Role-based review/approval, protected critical signals and deterministic routing | Consider evidence-first blind review to reduce anchoring. Do not import thresholds as validated operational values |
| UI | Investigation/demonstration story; no HCMC map requirement | Detailed HCMC map, separate Configuration, Risk cases and Activity log | Map is a later presentation requirement, not the fraud-detection mechanism |
| Data context | Orders, phones, addresses normalized for Vietnam, devices, repayments (pp.1,4–5) | Transactions/accounts/merchants/devices/IPs and reviewed cases | Restore order/refund context if available. Do not claim fake orders are confirmed using only IP/device associations |
| Evidence of performance | Synthetic targets: ~95% without AI, 0→90%+ new-tactic catch rate, zero genuine-user blocks (p.8) | Proposed held-out comparison and critical gates; UI numbers still scripted | Neither establishes measured efficacy. Original explicitly labels its numbers as targets, not results |

## Original ideas worth preserving

1. **One precise fraud story.** Show coordinated behavior across several individually ordinary purchases, with explicit merchant and order evidence. Where the mock data cannot establish a fake sale or cash movement, use “suspected coordinated merchant abuse,” not “proven cash-out.”
2. **A convincing legitimate decoy.** A family sharing a phone or unrelated tenants using a public network forces the investigator to look for counter-evidence. Shared devices/addresses are associations, not proof.
3. **A second-wave demonstration.** A newly approved rule catches a new, separate wave of the same tactic using the detector. Demonstrate reduced AI invocations only if the actual routing trace confirms this. Merely replaying identical training examples is not generalization.
4. **Vietnamese analyst reports.** Keep machine-readable fields and evidence identifiers, with a concise Vietnamese report for the target analyst. Validate semantic support as well as identifier existence.
5. **Decision-consistency review.** Flag conflicting dispositions for human investigation; do not automatically force the same result when evidence or policy versions differ.

## Conflicts and gaps to resolve in the initial deck

- **14 accounts versus the >10-account gate:** p.8 describes automatic order holds for a 14-account ring; p.7 requires a human for anything affecting more than 10 accounts. Require human approval before the simulated hold, or use a smaller ring consistent with the policy.
- **Novel-case actions:** p.6 permits mild reversible actions on unknown patterns, whereas p.7 requires a person for novel cases. Define precedence: for the MVP recommendation, novelty triggers review and no autonomous financial hold.
- **Who acts:** p.5 says the agent only recommends and the code guard decides; p.7 says “Agent alone.” Prefer “automatic execution by the policy-controlled application” so the model is not mistaken for the authority layer.
- **Evidence validation:** checking that a cited record ID exists (p.5) does not prove the record supports the claim. Also validate case ownership, event time, completeness and narrative grounding.
- **Risk/confidence values:** the example values 0.91 and 0.88 (p.5) are illustrative; do not present model self-confidence as calibrated risk. Define a separate calibrated scorer or omit the probability labels.
- **~95% cleared:** distinguish “not selected for AI,” “low-priority under existing rules,” and “confirmed legitimate.” Sample unflagged activity in evaluation to detect false negatives.
- **Anomaly versus rule coverage:** if “no rule fires,” show exactly which graph/anomaly detector triggers an investigation. That detector, its threshold and its baseline need implementation and testing.
- **Pre-payout claim:** the current asynchronous investigator does not stop completed payments. A sandbox hold simulation can illustrate a future control, but cannot substantiate prevented monetary losses.
- **Three-day expiry:** the deck does not fully define working-day calendars, release failure, repeated holds or who owns escalation. Do not implement real holds from this slide alone.
- **Legal, economic and team claims:** the deck includes lending statistics, risk targets, team history and a broad Vietnam-law statement. This comparison does not independently verify them or interpret the law. A 90-day delinquency measure is not a fraud-rate measure, and the deck does not establish that fraud is the largest cause of credit loss.

## Proposed synthesis, not an automatic PRD change

### Preserve existing P0

Engine adapter, durable case/job state, scoped read-only tools, validated evidence, deterministic policy guard, explicit analyst review, frozen evaluation, approved versioning, rollback, four-section UI and synthetic-only data.

### Candidate addition: constrained rule drafting

Use one explicit structured rule template rather than arbitrary generated executable code. For example, allowed fields could describe a time window, distinct-account count, shared-device condition, merchant concentration and an escalation outcome. Validation must reject unsupported fields, unbounded queries and any payment-write action. Store the rule in a versioned registry, test it against fraud and legitimate decoys, then require lead approval.

This would extend today's narrow shared-IP policy adjustment. Before adding it to P0, replace or reduce another nonessential feature and define rule-language semantics, evaluator behavior and activation gates. Do not claim arbitrary unseen-fraud detection from one synthetic example.

### Demonstration sequence

1. Detector flags a synthetic coordinated ring; agent gathers supporting and contradictory evidence and routes a case.
2. A household/public-network decoy remains under review or is marked legitimate by the analyst without automatic payment blocking.
3. A separately seeded novel pattern prompts investigation; analyst confirms the pattern, the constrained rule writer drafts a candidate, and a frozen replay reports both caught fraud and legitimate cases affected.
4. A lead promotes a passing candidate; a fresh synthetic wave is caught by that rule. Show actual AI calls and latency before/after.
5. Reject a harmful candidate, roll back a promoted version, or demonstrate tool-timeout recovery.

## Recommendation

Keep **Guardline's business story**, **Cortex Sentinel's implementation discipline**, and the **user-requested HCMC workspace**. The next implementation should prove the investigation and second-wave adaptation loop before spending more effort on additional dashboards. Simulated financial actions, broader rule generation and nightly review are explicit future scope decisions, not capabilities already delivered.
