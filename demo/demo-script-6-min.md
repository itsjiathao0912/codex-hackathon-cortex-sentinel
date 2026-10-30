# Cortex Sentinel: six-minute demo script

Template, not verified product claims. Replace all bracketed fields before presenting. The seven slots total 360 seconds, including live actions and pauses. Rehearse with a timer; placeholder length and product latency change the speaking pace. Aim for roughly 115–130 spoken words/minute during narration. Do not read stage cues aloud.

| Slide | Time | Duration |
|---|---|---|
| 1. Cortex Sentinel | 0:00–0:25 | 25 seconds |
| 2. The problem | 0:25–1:05 | 40 seconds |
| 3. A complete product journey | 1:05–3:05 | 120 seconds |
| 4. How it works | 3:05–3:45 | 40 seconds |
| 5. Build quality and Codex | 3:45–4:40 | 55 seconds |
| 6. Value and build direction | 4:40–5:30 | 50 seconds |
| 7. What we built | 5:30–6:00 | 30 seconds |

## 1. Cortex Sentinel · 0:00–0:25

Hello, we are [TEAM], and this is Cortex Sentinel. We help [TARGET USER] accomplish [CORE JOB] when [PAINFUL SITUATION]. Today, we will show one complete journey, from [STARTING INPUT] to [VERIFIABLE RESULT]. Our focus is [OFFICIAL BUILD DIRECTION], and the part we built during the hackathon is [NEW SCOPE].

## 2. The problem · 0:25–1:05

Consider [SPECIFIC USER] trying to [JOB] during [REAL SITUATION]. Today, they rely on [CURRENT APPROACH]. The difficult step is [BOTTLENECK], because [CAUSE]. That creates [CONSEQUENCE]. Our evidence is [SOURCE OR OBSERVATION], collected in [CONTEXT]. We chose this problem because the user needs [DESIRED OUTCOME], and the existing approach leaves [SPECIFIC GAP]. Cortex Sentinel addresses that gap through [CORE MECHANISM]. In the demo, watch for [SUCCESS CONDITION]. That is the outcome we will check, rather than asking you to take our claim on trust.

## 3. A complete product journey · 1:05–3:05

Here is [USER ROLE] in [STARTING SCREEN]. This scenario uses [SYNTHETIC OR APPROPRIATELY ANONYMIZED DEMO DATA], and our starting condition is [BASELINE]. First, I [ACTION ONE]. You can see [VISIBLE RESPONSE]. The important detail is [DETAIL], because it gives the user [BENEFIT].

Next, I [ACTION TWO]. The product now [ACTUAL BEHAVIOR]. While it runs, notice [STATUS OR EXPLANATION]. This step uses [IMPLEMENTED COMPONENT], and [HUMAN DECISION OR AUTOMATIC STEP] controls what happens next. I will open [RESULT VIEW] so you can inspect the outcome.

We now have [OUTPUT]. To verify it, I [CHECK ACTION]. The evidence is [VISIBLE PROOF], which matches [SUCCESS CONDITION]. Compared with the starting workflow, the user now [CONCRETE CHANGE]. Any values shown here are [MEASURED, SYNTHETIC, OR ILLUSTRATIVE], and the scope of this demonstration is [SCOPE].

Finally, I will try [BOUNDARY INPUT]. The expected behavior is [SAFE RESPONSE]. Here you can see [OBSERVED HANDLING]. This matters because [USER CONSEQUENCE]. That completes the journey: the user started with [PROBLEM] and ended with [VERIFIED RESULT].

**Stage cues:** Switch to the prepared app at 1:05. Allocate 30 seconds to setup and first action, 35 seconds to the core action, 30 seconds to verifying the result, and 25 seconds to the boundary case. Keep silent while the audience inspects the result. Return to slides at 3:05.

## 4. How it works · 3:05–3:45

The original contribution is [MECHANISM], compared with [BASELINE]. This diagram traces [INPUT] through [PROCESSING] to [RESULT]. We compared [CONFIGURATION A] and [B] on the same cases: [TIMINGS] with [QUALITY RESULTS]. We chose [OPTION], accepting [DOWNSIDE]. For privacy, [FIELDS] leave the app, [DATA] persists for [RETENTION], and [ACCESS CONTROL] limits access. Deletion is [IMPLEMENTED BEHAVIOR OR UNIMPLEMENTED LIMIT]. The boundary at [POINT] enforces [CONTROL]. [PLANNED CONTROL] remains future work.

## 5. Build quality and Codex · 3:45–4:40

Our [NUMBER] evaluation cases produced [PASS COUNT] passes, including [CRITICAL CASE RESULT]. End-to-end latency was [OBSERVED RANGE] under [CONDITIONS]. When [TIMEOUT OR API ERROR] occurs, the app [RECOVERY BEHAVIOR], without reporting false success. These are prototype observations, not production reliability claims.

Codex helped implement [TASK]. In one iteration, [TEST] exposed [FAILURE]. Codex changed [FILE OR COMPONENT], we reviewed [DECISION], and the rerun showed [RESULT]. The commit and test log are [ARTIFACT LINKS]. We verified [PRIVACY CONTROL] with [CHECK]; [REMAINING LIMIT] is still unresolved.

## 6. Value and build direction · 4:40–5:30

The immediate beneficiary is [USER OR ORGANIZATION]. For the task you saw, the baseline was [BEFORE], and our result is [AFTER], measured in [UNIT] using [METHOD AND SAMPLE]. If this has not been measured yet, our validation plan is [PILOT OR TEST], and the benefit remains a hypothesis. The meaningful change is [USER OUTCOME], rather than simply adding another tool to their workflow.

This aligns with [OFFICIAL BUILD DIRECTION] because [SPECIFIC CAPABILITY] enables [DIRECTION'S INTENT]. You saw that capability at [DEMO MOMENT]. The next validation step is [NEXT STEP] with [TARGET USER], focusing on [SUCCESS METRIC].

## 7. What we built · 5:30–6:00

We built [NEW SCOPE] on-site, with [FOUNDATION AND ATTRIBUTION] documented. Next is a [DURATION] pilot with [USERS]. Success means [MEASURED OUTCOME] while meeting [QUALITY AND PRIVACY GATE]. Estimated cost is [COST PER TASK AND ASSUMPTIONS]. Our biggest risk is [RISK]; we will test it through [NEXT EXPERIMENT]. Thank you.

## Failure fallback

If the app stalls for more than 10 seconds, say: “The live environment is not responding. I will show our recorded run of this same scenario. This recording shows [CAPTURE DATE / BUILD], and [LIMITATION] remains unresolved.” Play the prepared recording or show sequential screenshots, then resume at the current timestamp. Never describe a recording as live.

If time runs short, omit the optional boundary-case interaction and state its verified result briefly. Preserve the visible main result, Codex evidence, build-direction alignment, and closing. Stop at 6:00.

## Rehearsal checklist

- Prepare a repeatable scenario, seeded data, signed-in session, and reset steps.
- Record a backup of the exact scenario and store it in `demo/` once available.
- Verify every result and distinguish measured data from synthetic examples.
- Replace placeholders in both formats and speaker notes.
- Rehearse twice with slide transitions and clicks included.
- Record actual segment times and shorten text before increasing speaking speed.

## Deeper judging questions (outside the six-minute script)

Use `judges-evidence-template.md` for the measured latency comparison, privacy inventory, and pilot plan. Keep each answer to a decision, evidence, downside, and remaining risk. Do not read this section during the timed presentation.

- Latency: Where does time go? What quality or cost did the faster configuration sacrifice? What happens on timeout?
- Privacy: Which fields reach external services and logs? Who can access them? What deletion has actually been verified?
- Beyond the event: Who will try it next? What outcome would justify continuing? What dependency, cost, or risk could prevent that?
- Rehearsal: Slides 4, 5 and 7 retain their 40-, 55- and 30-second allocations. Shorten filled-in answers if needed; total remains six minutes.
