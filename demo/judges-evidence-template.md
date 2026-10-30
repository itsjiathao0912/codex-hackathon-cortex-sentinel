# Technical judging evidence template

Preparation material for questions after the six-minute demo. All bracketed values are placeholders. The user's judging account motivates these topics; it does not independently establish additional official rules for this event.

## 1. Latency decision

Claim: [specific user operation finishes within a task-appropriate budget].

| Configuration | Model / prompt / build | Case IDs and run count | Raw end-to-end times (seconds) | Task-quality passes | Usage / estimated cost |
|---|---|---|---|---|---|
| A | [versions] | [same cases] | [all measurements] | [passes/total] | [units and pricing date] |
| B | [versions] | [same cases] | [all measurements] | [passes/total] | [units and pricing date] |

- Start/stop definition: [user submit to usable verified result; include tool calls and retries].
- Conditions: [input sizes, network, cache state, streaming, concurrency and warm/cold start].
- If streaming: first visible output [seconds], full usable output [seconds]. Do not substitute first-token time for completed-task time.
- Decision: We chose [A/B] because [evidence], accepting [downside].
- Revisit when: [specific volume, quality, cost or latency threshold].
- Timeout: [deadline and visible state]; retry/cancel behavior: [implemented behavior].
- Verification: [test demonstrating no false success or duplicate consequential action].
- Limitation: [sample size and missing conditions]. Do not label a handful of runs a production p95 guarantee.

## 2. Data privacy inventory

Use synthetic data for the demo when possible. Verify anonymization rather than assuming removing a name is sufficient. Never put real secrets or sensitive records in this template.

| Stage | Fields and purpose | Recipient / storage | Access | Retention / deletion | Evidence / status |
|---|---|---|---|---|---|
| User input | [minimum fields] | [app] | [roles] | [behavior] | [test or unknown] |
| Model request | [fields after filtering] | [provider and endpoint] | [boundary] | [verified service settings] | [redacted trace and dated documentation] |
| Tool or external service | [fields or none] | [service] | [permissions] | [behavior] | [test or unknown] |
| Application storage | [records or none] | [store] | [roles] | [behavior] | [test or unknown] |
| Logs and analytics | [metadata/content] | [sinks] | [roles] | [behavior] | [test or unknown] |
| Output / exports | [fields] | [destination] | [sharing] | [behavior] | [test or unknown] |

Checks to record, where applicable:

- [ ] Inspect a redacted request and confirm only necessary fields leave the app.
- [ ] Confirm API keys are absent from client assets, tracked files, logs and screenshots.
- [ ] Verify unauthorized users cannot read another user's records.
- [ ] Test deletion across the stores under your control; identify backups/logs and external retention limits.
- [ ] Check provider behavior for the actual endpoint and account settings against current official documentation. Do not infer training, retention or residency policies from the product name.
- [ ] Label every control: implemented-and-tested / implemented-but-unverified / planned / unknown.

Judge answer: “[FIELDS] leave the application for [PURPOSE]. [DATA] is stored in [LOCATION] for [DURATION]. Access is [CONTROL]. We verified [TEST]. [LIMITATION] remains.”

## 3. Beyond-hackathon pilot

- User segment and recruitment route: [who and how].
- Owner and duration: [person/team; dates or timebox].
- Workflow and pilot scope: [one real task; exclusions].
- Baseline: [current workflow and measurement method].
- Success gate: [correct completion / effort / time metric, threshold, sample and method].
- Quality/privacy gate: [must-pass requirement; how checked].
- Stop or rollback condition: [specific failure and response].
- Biggest unresolved assumption: [risk and why it matters].
- Next experiment: [test that reduces that risk].
- Cost model: [tokens × dated rates + tools + hosting + retries + human review]; expected volume [assumption].
- External dependencies: [data permission, integration, expert review or deployment].
- What is working now: [verified capability].
- What must change before real use: [specific gap, owner, validation].

Closing sentence: “Next we will pilot [WORKFLOW] with [USERS] for [DURATION]. We continue only if [OUTCOME AND QUALITY/PRIVACY GATE]. Our largest risk is [RISK], which [EXPERIMENT] will test.”

## Evidence links

- Exact build / configuration: [commit and config version].
- Timing and evaluation log: [path].
- Privacy diagram and control checks: [paths].
- Pilot protocol and cost assumptions: [paths].
- Codex contribution to these changes: [prompt/task, diff, test, human decision].
