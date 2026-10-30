# World Monitor research and design rationale

Reviewed 2026-10-31. The user supplied the app, repository documentation, and a screenshot as design references.

## Sources inspected

- [World Monitor app/landing reference](https://www.worldmonitor.app/#agents): the fetched landing page describes an immediately populated map, country dossiers, selectable lenses, and map layers.
- [Live dashboard](https://www.worldmonitor.app/dashboard): opened in a browser to inspect the dashboard surface.
- [User-supplied repository documentation](https://github.com/tncsharetool/worldmonitor/blob/main/docs/DOCUMENTATION.md): the GitHub HTML did not expose the document body, so the raw Markdown was downloaded and relevant sections read.
- [Raw documentation](https://raw.githubusercontent.com/tncsharetool/worldmonitor/main/docs/DOCUMENTATION.md): Interactive Global Map, Marker Clustering, Regional Focus, Map Pinning, and System Health sections.
- [Natural Earth country geometry](https://github.com/nvkelso/natural-earth-vector/blob/master/geojson/ne_110m_admin_0_countries.geojson): embedded geographic basemap data, rounded to two decimals to reduce file size.
- [Natural Earth public-domain terms](https://www.naturalearthdata.com/about/terms-of-use/).

The supplied repository and live app may represent different versions. This research uses documented interaction patterns, not a claim that the fork exactly matches the current deployment. No World Monitor source code is copied into the wireframe.

## Findings applied

| Reference pattern | Adaptation for Cortex Sentinel |
| --- | --- |
| Populated map without a setup tour | Open into a seeded saved monitor |
| Multiple layers on one geographic surface | Risk cases, merchant locations, related activity, IP uncertainty |
| Region presets and time windows | Southeast Asia / World and 1h / 24h / 7d |
| Clickable markers and contextual detail | Case evidence and analyst disposition beside the map |
| Variant switching while preserving map state | Select saved configurations without changing pages |
| Intelligence panels below the map | Case queue, investigation trace, feedback review |
| Visible health/status | Agent pause/resume and incomplete-case evidence |

The selected configuration is more than a visual layer: it defines which cases and policy settings are being monitored. Display layers never silently change detection rules.

## Design decisions

Use the screenshot's dark operations workspace: deep blue-black background, slate geographic boundaries, muted labels, green running/approval state, amber review signals, red high-priority cases, and blue geographic context. Typography uses familiar system sans-serif for decisions and limited monospace for case/status metadata.

Keep the map as the largest surface. Replace the earlier wizard with saved configurations on the left, a contextual editor/investigation on the right, and concise operational panels below. There are no dedicated Configure, Validate, Investigate, or Improve pages.

Preserve the two consequential actions—test and apply—inside one panel rather than removing them to save clicks. Returning analysts start monitoring immediately; editing is optional.

## Deliberately deferred

World Monitor documents clustering, pinning, extensive providers, and many domain layers. Those are not necessary for this six-case interaction prototype. Production-scale clustering, tile rendering, URL state, persistent preferences, real data-source health, and an interactive multi-hop graph remain later implementation choices.

This repository deliverable is a UI prototype with embedded geographic data, not a clone or integration of World Monitor services.
