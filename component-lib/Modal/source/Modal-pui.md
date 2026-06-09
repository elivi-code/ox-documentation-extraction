---
component: Modal
package: "@8x8/oxygen-modal"
category: layout_overlay
role: pui
role_description: "Platform UI context — infrastructure hooks (navigation, notifications, session, event bus)"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Modal/props]]"
  - "[[Modal/examples]]"
  - "[[Modal/tokens]]"
  - "[[Modal/accessibility]]"
  - "[[Modal/Modal-figma]]"
  - "[[Modal/Modal-audit]]"
tags:
  - oxygen
  - component/Modal
  - role/pui
  - stage/spec_ready
  - category/layout_overlay
---
<!-- SOURCE: platform-ui-mcp snapshotId: 2026-02-24 -->
<!-- EXTRACTED: 2026-05-01 -->
<!-- COMPONENT: Modal -->
<!-- CONFIRMED BY: engineer (relevance check step 2) — replied "none" -->

# Modal — Platform UI Context

<!-- NO RELEVANT PUI CONTEXT -->

No Platform UI packages, hooks, events, or MFEs were identified as directly relevant to the Modal component.

## Candidates rejected

| Path | Title | Reason |
|------|-------|--------|
| `mfes/reusable-mfes/mfes/block-navigation-modal.md` | Block Navigation Modal | Separate shell-level MFE (not a PUI infrastructure concern for `@8x8/oxygen-modal` itself) |

## Notes

The `shell-navigation-block` event exists in the shell event bus and is related to blocking navigation (a common Modal use case), but it operates at the shell/MFE routing layer — not as an integration point for the Oxygen Modal component. An MFE using `@8x8/oxygen-modal` to implement a block-navigation confirmation dialog would consume `shell-navigation-block` independently.

_Source: platform-ui-mcp · Extracted 2026-05-01_
