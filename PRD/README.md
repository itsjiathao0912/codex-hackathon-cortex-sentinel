# Cortex Sentinel — map-first MVP

Updated 2026-10-31. This revision replaces the multi-screen wizard with a single monitoring workspace inspired by World Monitor.

- [Interactive wireframe](wireframe.html): download or clone, then open in any modern browser. No server, API key, or network connection is required.
- [Revised MVP flow and scope](MVP-user-flow.md)
- [World Monitor research and design decisions](World-Monitor-research.md)
- [Three-loop verification and self-review](Verification-review.md)

![Map-first wireframe preview](wireframe-preview.png)

## Try the revised flow

1. Open the wireframe directly into the populated risk map.
2. Select a saved monitor under **My configurations**. Its cases, scope, map markers, and selected case update together.
3. Toggle layers, switch between Southeast Asia and World, change the period, drag to pan, or zoom.
4. Select a marker or case row to inspect evidence in the context panel.
5. Select **Edit configuration**, adjust fields, **Test changes**, then **Apply configuration** in the same panel.
6. In Merchant coordination with the 24-hour period selected, open C-105 and save **Legitimate activity** with a reason.
7. Use **Test & review improvement** in the feedback panel, approve the scripted candidate, then try rollback.
8. Select Location anomalies and inspect C-202 for incomplete evidence. Try pause/resume and expanding the map.

## Prototype boundaries

All case records, IPs, activity, evaluation outputs, and geographic activity locations are synthetic. Country boundaries are embedded Natural Earth geometry. The prototype uses no World Monitor application code or live services.

This is a wireframe, not a deployed investigator: tests are scripted, settings do not run a detection model, activity does not stream, and decisions/settings reset on reload. IP uncertainty rings are illustrative rather than scaled accuracy measurements. Links indicate related evidence, not proven cross-border payment flows. The relationship strip is not a trained GNN.

The flow document remains a proposal preceding formal BRD and PRD sign-off. Git history retains the earlier wizard design.
