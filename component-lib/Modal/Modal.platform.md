---
parent: "[[Modal]]"
section: platform
component: Modal
role: spoke
pipeline_stage: published
audit_verdict: partial
siblings:
  - "[[Modal]]"
  - "[[Modal.props]]"
  - "[[Modal.anatomy]]"
  - "[[Modal.tokens]]"
  - "[[Modal.usage]]"
  - "[[Modal.accessibility]]"
  - "[[Modal.composition]]"
tags:
  - oxygen
  - component/Modal
  - role/spoke
  - stage/published
---

<!-- NO RELEVANT PUI CONTEXT -->

No Platform UI packages, hooks, events, or MFEs were identified as directly relevant to the Modal component.

## Candidates rejected

| Path | Title | Reason |
|------|-------|--------|
| `mfes/reusable-mfes/mfes/block-navigation-modal.md` | Block Navigation Modal | Separate shell-level MFE (not a PUI infrastructure concern for `@8x8/oxygen-modal` itself) |

## Notes

The `shell-navigation-block` event exists in the shell event bus and is related to blocking navigation (a common Modal use case), but it operates at the shell/MFE routing layer — not as an integration point for the Oxygen Modal component. An MFE using `@8x8/oxygen-modal` to implement a block-navigation confirmation dialog would consume `shell-navigation-block` independently.

_Source: platform-ui-mcp · Extracted 2026-05-01_
