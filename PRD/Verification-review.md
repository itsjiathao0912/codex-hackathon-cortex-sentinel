# Three-loop verification and self-review

Date: 2026-10-31. Scope: the standalone map-first wireframe, not an operational fraud detector. All three loops were performed by the same author with browser checks and visual inspection, not by independent reviewers.

## Loop 1 — Workflow correctness

**Initial failures reproduced:** pausing erased an untested configuration-name edit; configuration cards continued saying Monitoring while the header said Paused. The editor held unsaved field values only in the DOM, while pause triggered a full rerender. Card status was hardcoded.

**Changes:** capture configuration drafts on input; derive configuration status from the shared pause state.

**Retest:** six checks passed: draft survival, consistent paused status, replay enabling Apply, edits invalidating replay, applied name/version, and configuration-specific cases.

**Judgment:** the main selection/edit/apply workflow works as a prototype. It still uses scripted replay outputs rather than evaluating configuration changes against transaction records.

## Loop 2 — Visual usability and responsive behavior

**Initial findings:** no horizontal overflow at 1600, 1024, 768, 390, or 320 pixels, but the map started around 953 pixels below the top on phones. Passing an overflow check did not mean the layout was map-first. Low-priority table rows were also amber while map markers were blue.

**Changes:** compact configuration selector on small screens; expandable map-layer controls; matching blue treatment for Low priority. Mobile controls retain useful touch targets without stretching circular markers.

**Retest:** all five widths retained no horizontal overflow. In the checked phone layouts, the map began around 405–424 pixels from the top. Mobile selection and layer expansion worked; Low rows matched the map. Before/after phone screenshots were inspected. The final desktop preview was refreshed.

**Judgment:** desktop is the strongest presentation. Mobile is functional and shows the map much earlier, but remains a long stacked workspace. Dense global marker clustering and label collision management are deferred.

## Loop 3 — Edge cases and regression checks

**Initial failures reproduced:** pause erased an unfinished analyst disposition/reason; replay accepted a distance of 26 km despite the input specifying 25 km increments.

**Changes:** preserve per-case decision drafts through rerenders; validate finite distance, range, and increment before replay.

**Retest:** eight checks passed: decision draft survival, invalid increment rejection, user-entered markup rendered as text, empty decision rejection, adaptation approval, rollback restoring baseline/priority, offline country rendering, and offline configuration switching. No JavaScript runtime errors were observed during this run.

**Final spot checks:** keyboard Enter selected a focused configuration; phone markers stayed circular; the phone layout had no horizontal overflow. The standalone HTML was opened directly from disk with browser networking disabled and rendered all 177 embedded country geometries.

## Self-assessment

| Criterion | Assessment | Reason |
| --- | --- | --- |
| Matches the requested direction | Strong | One geographic workspace; own configurations selectable beside the map |
| Workflow clarity | Good | Inspection, configuration testing/apply, and feedback stay in context |
| Visual hierarchy | Good on desktop | Map dominates; supporting operational panels remain visible |
| Mobile usability | Acceptable | Compact selector improves initial access; full workflow is still vertically long |
| Interaction reliability | Good within tested paths | Reproduced state-loss and validation defects fixed and retested |
| Fraud/AML effectiveness | Not assessed | No live engine, LLM investigation, measured replay, or trained GNN |
| Production readiness | Not ready | No persistence, authentication, real notifications, or operational backend |

**Overall judgment:** suitable for hackathon UX review and a scripted demonstration. It meets the map-first direction substantially better than the original wizard. It is not yet evidence that an autonomous fraud agent works or improves detection.

## Remaining limitations

- State resets on reload. Deliberately closing/changing a configuration discards its unfinished draft; there is no persistent draft system.
- Geography uses a simple projection. IP uncertainty rings are illustrative; geographic links do not prove payment movement.
- The activity feed is workspace-wide, while cases are configuration-specific.
- Settings and adaptation use simplified version handling. The real product needs a unified, auditable policy lifecycle.
- Keyboard checks covered configuration activation, not a comprehensive accessibility audit.
- No load, production security, or statistical model evaluation was performed.
