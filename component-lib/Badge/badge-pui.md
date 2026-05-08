---
component: Badge
package: "@8x8/oxygen-badge"
category: data_display
role: pui
role_description: "Platform UI context — infrastructure hooks (navigation, notifications, session, event bus)"
pipeline_stage: extracted
pipeline_note: "Core files present; audit not yet run"
siblings:
  - "[[Badge/props]]"
  - "[[Badge/examples]]"
  - "[[Badge/tokens]]"
  - "[[Badge/accessibility]]"
tags:
  - oxygen
  - component/Badge
  - role/pui
  - stage/extracted
  - category/data_display
---
<!-- SOURCE: platform-ui-mcp snapshotId: 2026-02-24 -->
<!-- EXTRACTED: 2026-04-29 -->
<!-- COMPONENT: Badge -->
<!-- CONFIRMED BY: engineer (relevance check — all candidates reviewed, none confirmed) -->

# Badge — Platform UI Context

## Hooks
<!-- NONE IDENTIFIED -->

No PUI hooks are relevant to the Badge component. The `@8x8/pui-use-notification` package (v1.6.0) exists in the PUI ecosystem but a search for "badge" and "notification badge" in PUI docs returned no matches linking it to Badge usage.

## Events
<!-- NONE IDENTIFIED -->

No PUI events are tied to Badge. Badge is a passive display component — it renders state but does not emit or subscribe to events itself.

## Related MFEs
<!-- NONE IDENTIFIED -->

No MFEs in the PUI registry reference Badge directly.

## Usage examples
<!-- NONE IN CONFIRMED DOCS -->

## Candidates rejected

| Path | Reason rejected |
|------|----------------|
| `docs/05-roadmap.md` | Only mentions "new badge documentation" as a completed roadmap item — no API content |

---

_Source: platform-ui-mcp (snapshotId: 2026-02-24) · Extracted 2026-04-29_
