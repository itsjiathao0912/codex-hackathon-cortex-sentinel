# Cortex Sentinel — MVP proposal

Hackathon track: **Autonomous & Adaptive AI**.

This folder preserves the proposed MVP journey and clickable wireframe for ShopeePay risk and fraud analysts. It is a discussion baseline before the formal BRD and PRD, not an approved production specification.

- [MVP user flow and scope](MVP-user-flow.md)
- [Clickable wireframe](wireframe.html) — download or clone the repository and open this file in a browser. GitHub's file view displays source rather than running the prototype.

The wireframe uses synthetic data and scripted results. It has no connection to Shopee systems, payment execution, or the OpenAI API. Its location panel is a map-layout placeholder, and its relationship view is not a trained graph neural network.

## Suggested walkthrough

1. Complete the three configuration steps.
2. Run the mock replay and activate sandbox monitoring.
3. Simulate the coordinated merchant ring and open its investigation.
4. Return to monitoring, select legitimate shared-IP activity, and simulate it.
5. Record **Legitimate activity** with a reason; evaluate and approve the proposed improvement.
6. Return to monitoring and replay the legitimate scenario under v2.
7. Try the enrichment outage, pause/resume, activity log, and policy rollback.

Navigation is clickable. Investigation evidence tabs and decision controls are interactive. Replay outputs are illustrative constants, not calculations from a complete transaction dataset. The prototype keeps only one current simulated case; it is not a persistent case-management system. Refresh/browser persistence depends on the standalone viewer's local state support.

Prepared: 2026-10-31, Asia/Ho_Chi_Minh.
