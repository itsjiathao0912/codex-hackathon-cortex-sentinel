# Seven-hour Codex hackathon research and evidence playbook

Research date: 31 October 2026. Context: Codex Shopee Hackathon / Sea x OpenAI Codex Hackathon Vietnam. Recommendations below are our synthesis for a bounded prototype, not official scoring thresholds. Product-specific details remain unknown because the project contained only demo templates when inspected.

## Official event context

The [official Vietnam event site](https://codexhackathon.sea.com/) gives a 10:00–17:00 hacking window and three directions: Autonomous & Adaptive AI; AI-Native Products & Operations; Deep Domain AI. Teams may address one or several. Choose one primary direction and demonstrate it clearly.

There is an unresolved rule conflict: the website FAQ says to build from scratch, whereas the supplied event-day screenshot permits substantial extensions to existing projects with attribution and a new public repository. Ask an organizer which rule controls before relying on existing project code. Do not claim compliance without clarification. The repository remains private per the user's instruction. Templates and preparation should not be represented as work completed during the judged on-site window.

## 1. Problem framing: a 45-minute process

A good problem statement identifies a person, situation, job, obstacle, consequence, and existing workaround. It leaves room to test different solutions.

| Minutes | Technique | Output |
|---|---|---|
| 0–5 | Select a reachable user and one recurring task | Specific role and trigger |
| 5–20 | Two or three short interviews, or observe a recent real task | Notes and actual workflow |
| 20–30 | Separate observations from interpretations | Obstacle, consequence, and assumptions |
| 30–40 | Test the riskiest assumption first | Hypothesis, test, measure, pass condition |
| 40–45 | Bound the MVP to one complete journey | Input, result, quality constraint, exclusions |

Ask: “Tell me about the last time you did this.” “Show me the steps.” “Where did you get stuck?” “What did you do instead?” “What happened because of that?” Ask about frequency, effort and spending without suggesting answers. Avoid “Would you use my AI app?”

[YC's user-interview guidance](https://www.ycombinator.com/library/Iq-how-to-talk-to-users) emphasizes current behavior and workarounds rather than pitching hypothetical solutions. [IDEO's interview method](https://www.designkit.org/methods/interview.html) supports learning from people in their context. A few conversations provide directional evidence, not market validation. ChatGPT can help formulate questions and organize anonymized notes; generated personas and simulated interviews are not user evidence.

### Fill-in statement

> When [trigger], [specific user] needs to [job], but [observed obstacle] causes [consequence]. Today they use [workaround]. Evidence: [observation and sample]. We will test whether [intervention] improves [metric] while preserving [quality condition].

Example only, not a Cortex Sentinel product claim: “When a seller handles a delivery dispute, they must reconstruct events across several messages. Missing chronology causes repeated checking. We will test whether an evidence-linked summary reduces checking time without adding unsupported claims.”

Use a [Strategyzer Test Card](https://www.strategyzer.com/library/validate-your-ideas-with-the-test-card): assumption, experiment, measurement, threshold. Set the threshold before seeing results. Desirability, feasibility and usefulness are different assumptions. Test the highest-impact one with the weakest evidence.

### Framing acceptance criteria

- One named user role, trigger, and job.
- One traceable observation or source; explicit labels for assumptions.
- A current alternative, including manual work or plain ChatGPT.
- A consequence that matters to the user.
- One observable success condition and a quality constraint.
- A realistic complete demo path and explicit out-of-scope features.

## 2. Build quality: proposed prototype acceptance gates

These are suggested low-stakes prototype gates. Adjust thresholds to the task before testing. They are not official requirements or evidence of production readiness.

| Gate | Suggested acceptance condition | What to show |
|---|---|---|
| Complete journey | Five consecutive end-to-end runs succeed on disclosed fixtures | Input, final result, and run log |
| AI task quality | Frozen set of 10 cases; at least 8 meet the predefined rubric; every designated critical case passes | All case IDs, scores, failures and rubric |
| Grounding | For factual outputs, claims reference actual supplied evidence; missing evidence triggers uncertainty | Trace one output claim to a source; show missing-evidence case |
| Structured behavior | If JSON/tool use is needed, schema validation and allowed arguments hold on every test case | Validated output or rejected invalid action |
| Failure handling | Invalid input, missing evidence, and API timeout/error each produce a clear recoverable state | One live failure case plus logs for the others |
| Side effects and secrets | No key in browser or tracked files; consequential writes require explicit confirmation or stay in a sandbox | Permission boundary and safe rejected action |
| Speed and cost | Predeclare a demo wait budget, e.g. 15 seconds; report actual latency and usage per case | Raw run timings, token usage, dated cost assumptions |
| Reproducibility | README starts the app from a clean session; fixtures reset; exact build recorded | Startup/reset instructions, commit, backup recording |

Recommended 10-case mix: 5 ordinary cases, 2 edge cases, 2 missing/ambiguous-data cases, and 1 adversarial or invalid-action case. The mix is a starting point, not a complete safety evaluation. Mark critical cases explicitly. An overall 8/10 does not excuse a critical failure.

Freeze the set before tuning, keep expected outcomes independent of the current output, and use a small rubric: task completion, factual support, required fields, safe handling. Deterministic checks first, then human review of judgment-dependent output. Do not let the same model's self-confidence stand in for verification. Repeatedly tuning to this tiny set can overfit it; include a fresh case if time allows and disclose the limitation.

Use a lightweight local JSON/CSV test runner. Record build, model identifier, prompt/config version, input, expected result, observed result, pass/fail, latency and usage. Five runs demonstrate a repeatable demo, not a reliability estimate; 10 eval cases cannot certify safety. For medical, financial, legal or other high-stakes tasks, narrow to a supervised demonstration without real consequential actions.

The [OpenAI evaluation guide](https://developers.openai.com/api/docs/guides/evaluation-best-practices) supports early, task-specific evaluation with explicit objectives, representative and difficult cases, and human-calibrated scoring. [Structured Outputs](https://developers.openai.com/api/docs/guides/structured-outputs) constrains format, not factual correctness; handle refusals and incomplete responses separately. [Safety guidance](https://developers.openai.com/api/docs/guides/safety-best-practices) and the [API overview](https://developers.openai.com/api/reference/overview) inform bounded actions and server-side key handling. Also run the project's relevant build/type/lint checks and critical path tests.

## 3. Insight and originality: show the reasoning and the comparison

An insight explains a behavior or constraint. A feature is the response to that insight.

> We observed [behavior]. We think it happens because [constraint, with evidence or hypothesis label]. Therefore the product must [design implication]. We changed [specific decision], and tested [result].

[IDEO's insight-statement method](https://www.designkit.org/methods/create-insight-statements.html) derives useful learning from research themes. The [Strategyzer Learning Card](https://www.strategyzer.com/library/capture-customer-insights-and-actions-with-the-learning-card) separates observation, inference and action. Keep that chain visible in one example.

Compare the manual workflow, a fairly prompted ChatGPT baseline with the same permitted context, the closest relevant existing tool, and your prototype on the same task. Do not handicap alternatives or claim capabilities you have not checked.

| Comparison field | Record |
|---|---|
| Task and inputs | Identical scenario and required output |
| Existing alternative | Name, version/date, configuration, observed capability |
| Your contribution | Specific workflow, domain constraint, evidence check or recovery mechanism |
| Measured effect | Completion, correctness, effort, time, interventions |
| Reused foundations | APIs, libraries, prior code, attribution |
| Limitation | What the comparison cannot establish |

If feasible, remove your distinctive mechanism and rerun the same cases: does the result worsen? This ablation helps show why the mechanism matters. It does not prove causation beyond the test conditions or universal novelty.

Say “Among the alternatives we reviewed, our contribution is [difference], demonstrated on [cases].” Avoid “first ever.” A short search cannot prove nobody else has built it. New model usage, extra agents, and an attractive interface alone do not establish originality.

## 4. Real-world value: observe someone completing a task

Recruit two or three actual or likely users if accessible. Give them a realistic goal with neutral instructions. Observe rather than coach. Record task completion, elapsed time, errors, and assistance. If only teammates are available, label them proxy users.

[GOV.UK's moderated usability guidance](https://www.gov.uk/service-manual/user-research/using-moderated-usability-testing) supports realistic tasks and observing actual/likely users. Its [benchmarking guidance](https://www.gov.uk/service-manual/measuring-success/usability-benchmarking-a-website-or-whole-service) identifies success, time and false-success as useful measures. Our tiny hackathon test is exploratory, not a formal benchmark.

Use comparable inputs and the same definition of a correct result for baseline and prototype. Include verification and correction time. Vary test order if feasible to reduce learning effects. Show raw results, for example “[N] of [N] finished unaided; timings were […]; errors were […]”. Never fill these with invented numbers.

If extrapolating savings, show the calculation: verified time saved per task × realistic task frequency. Label projected savings separately from measured results. Faster incorrect output is not value. Ask for a concrete next step, such as a follow-up trial; compliments do not establish adoption or willingness to pay.

## 5. Alignment with the official focus areas

| Direction | Strong demonstration | Weak substitute |
|---|---|---|
| Autonomous & Adaptive AI | Change a condition; show detection, bounded recovery, and escalation at a limit | Calling a chain of prompts autonomous |
| AI-Native Products & Operations | Show how AI changes the complete workflow and what disappears or becomes possible | An unrelated chat box attached to a standard app |
| Deep Domain AI | A real domain constraint and exception change behavior; a knowledgeable user checks the result | Domain terminology in a generic prompt |

Choose one primary direction. Write: “We fit [direction] because the product [implemented behavior], visible at [demo timestamp].” Add a second only if demonstrable. Official descriptions are on the [event website](https://codexhackathon.sea.com/); the evidence examples above are recommendations.

## 6. Show how Codex contributed to the build

Separate roles: ChatGPT can assist research synthesis and design critique; Codex can inspect and change the repository, run checks, and help debug; the OpenAI API can power runtime behavior where useful. Using every tool is not itself evidence of effectiveness, and API usage alone does not show Codex's build contribution.

Keep three short iteration records:

1. Goal and constraints given to Codex.
2. Files or diff it produced and a concrete design decision.
3. Test result, failure or review finding.
4. Correction and final verified behavior.
5. Human judgment: what you accepted, rejected, or changed and why.

A useful task prompt: “Goal: implement [one user outcome]. Context: [files and behavior]. Constraints: [scope, permissions, dependencies]. Done when: [testable conditions]. Inspect first, implement, run the relevant checks, and report remaining failures.”

Show one complete issue → change → check loop in the demo, with two more linked in the README. Retain concise redacted prompts and artifact links rather than a wall of chat. Do not measure effectiveness by prompt count, lines generated, agent count, or unsupported hours-saved claims. If a coding task is delegated concurrently, use separate file ownership and integrate/test the results.

[Official Codex best practices](https://learn.chatgpt.com/guides/best-practices) recommends clear goals, context, constraints and completion conditions, plus verification and diff review. The iteration log above is our suggested way to make that process inspectable for judges.

## 7. Suggested seven-hour schedule

The event's published window is 10:00–17:00. This allocation totals 420 minutes and is a recommendation.

| Local event time | Work | Exit condition |
|---|---|---|
| 10:00–10:45 | Observe users, frame problem, pick direction | One problem statement and riskiest assumption |
| 10:45–11:15 | Baseline, scope, fixtures and eval rubric | Frozen cases and complete journey contract |
| 11:15–13:30 | Build one end-to-end slice with Codex | Working input-to-result path |
| 13:30–14:30 | Run evals, fix failures and permission boundaries | Gates pass or scope reduced with limits disclosed |
| 14:30–15:10 | User task test and baseline comparison | Raw outcome, time and error evidence |
| 15:10–15:40 | Buffer for integration and fixes | Stable demo build |
| 15:40–16:20 | Evidence, README, deck and backup recording | Every claim has an artifact |
| 16:20–17:00 | Rehearse six-minute demo, freeze and submit | Resettable build, accessible submission, two rehearsals |

If behind, cut features before cutting evidence. Avoid a late migration, a second user persona, or extra integrations unrelated to the demonstrated job. Protect time for a working deployment and rehearsal.

## 8. What the judges should see in six minutes

| Segment | Evidence |
|---|---|
| 0:00–0:25 | User, promised outcome, primary direction |
| 0:25–1:05 | Observed problem and current workaround |
| 1:05–3:05 | Complete journey, inspectable result, boundary case |
| 3:05–3:45 | Architectural choice and distinctive mechanism |
| 3:45–4:40 | Test outcomes and one Codex iteration |
| 4:40–5:30 | Baseline comparison, user value, direction alignment |
| 5:30–6:00 | Honest hackathon scope, limitation, next validation step |

Use `evidence-log-template.csv` to connect every claim to an artifact. Put exact sample sizes and limits beside results. Replace placeholders in `demo/` only after evidence exists.

## 9. Deeper judging: latency, data privacy, and what comes next

The user supplied an account of two judging rounds where Sea/OpenAI representatives examined latency trade-offs, privacy and development beyond the hackathon. Its original publication URL and applicability to this event have not been independently established. Treat the account as preparation context, not a replacement for the official rubric. The following techniques and targets are recommendations, not reported judging rules or verified product behavior.

### Latency: explain a measured choice

Compare two viable configurations on identical cases and score quality alongside speed. Record exact build/model/prompt, input size, network/cache conditions, retries and raw timings. Measure user submission to a usable result; for streaming, record time to first output separately. Include downstream tools and user verification where the claimed benefit is task completion. Note cost assumptions and their pricing date.

Choose the configuration that meets the quality constraint within the task's latency budget. Document the sacrificed benefit and the condition that would cause you to reconsider. Small samples show observed behavior, not production percentile reliability. Test a deadline and clear recovery state. If a failed request can produce a consequential action, verify that retrying cannot silently duplicate it.

For a seven-hour build, use the existing frozen evaluation cases and compare only one meaningful choice, such as model configuration, retrieval depth, or number of tool calls. Do not add an extensive benchmark project. Protect the demo and rehearsal time.

### Privacy: show the actual data path

Inventory input, external model/tool requests, application storage, logs, analytics and exports. For each, record the fields, purpose, destination, access, retention, deletion and verification status. Use synthetic or appropriately anonymized demo data and inspect a redacted request to establish what leaves the application. Check that standard API credentials remain server-side, consistent with the [OpenAI API overview](https://developers.openai.com/api/reference/overview).

Differentiate implemented-and-tested controls, unverified implementation, planned controls and unknowns. Verify service-specific data handling against current official documentation for the actual endpoint/account settings before making provider retention, training or residency claims. This playbook asserts no blanket provider data-handling guarantees. A private GitHub repository alone does not establish application privacy.

Prepare an evidence-backed answer to: what leaves the app, where it persists (including logs), who can access it, and what deletion actually removes. Record any untested boundary honestly. Avoid collecting sensitive production data merely to make the demo realistic.

### Beyond the hackathon: a testable pilot

Replace a broad feature roadmap with a named user segment, a timeboxed pilot, one measurable outcome, quality/privacy constraints and a stop condition. Identify the biggest unresolved assumption and the next experiment. Distinguish current capability from work required before real use.

Estimate cost with explicit volumes and dated assumptions: model usage, external tools, hosting, retries and human review. Record data/integration dependencies and an owner for the next validation step. Forecast savings and operating costs are projections until measured. A credible next step is stronger than an unsupported scaling claim.

### Integration into the existing seven hours and six-minute demo

- During scoping, declare the latency budget, privacy boundary and pilot hypothesis.
- During build/evaluation, reuse cases for the configuration comparison and test failure/privacy controls.
- During the user comparison, measure task time including verification and corrections.
- During evidence preparation, complete `demo/judges-evidence-template.md` and the three additional rows in `research/evidence-log-template.csv`.
- Slide 4: architecture, original mechanism, latency decision and privacy path.
- Slide 5: timing/quality evidence, timeout recovery, verified controls and Codex iteration.
- Slide 7: pilot users, measurable outcome, cost assumptions and biggest risk.

Keep detailed tables in the judging evidence template for follow-up questions. No additional timed slides are required; the seven-slide script remains 360 seconds including live actions and pauses.
