---
component: ToggleButton
status: draft
version: ""
category: form_inputs
package: "@8x8/oxygen-toggle-button"
figma: "https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=51776:7455"
variants:
  - Toggle Input (switch-only, 40×24px)
  - Toggle (switch + label, 148×24px default)
  - Toggle Group (wrapper, 320px wide)
props:
  - testId: string
  - id: string
  - label: node
  - value: "number|string|bool|object"
  - name: string
  - infoBoxText: node
  - infoBoxButtonLabel: string
  - isChecked: bool
  - isDisabled: bool
  - isIndeterminate: bool
  - showLabelTooltipOnOverflow: bool
  - onBlur: func
  - onChange: func
  - onFocus: func
  - "ToggleButtonGroup.isHorizontal": boolean
  - "ToggleButtonGroup.children": ReactNode
subcomponents:
  - "[[ToggleButtonGroup]]"
related:
  - "[[IconButton]]"
  - "[[Tooltip]]"
  - "[[Radio]]"
  - "[[Checkbox]]"
patterns: []
tokens:
  - "[[token.ui.ui33]]"
  - "[[token.actions.action01]]"
  - "[[token.interactive.focus01]]"
  - "[[token.ui.ui06]]"
  - "[[token.text.textcolor01]]"
  - "[[token.interactive.disabled02]]"
  - "[[token.actions.action03]]"
  - "[[token.error.error01]]"
  - "[[token.text.textcolor02]]"
  - "[[token.ui.ui23]]"
  - "[[token.ui.ui22]]"
spokes:
  - "[[ToggleButton.props]]"
  - "[[ToggleButton.anatomy]]"
  - "[[ToggleButton.tokens]]"
  - "[[ToggleButton.usage]]"
  - "[[ToggleButton.accessibility]]"
  - "[[ToggleButton.platform]]"
  - "[[ToggleButton.composition]]"
pipeline_stage: draft
audit_verdict: NO
audit_open_items:
  - "CONFLICT GAP-002 — ToggleButtonGroup isError: Figma has it, OX API does not. Human decision required."
  - "STUB GAP-003 — Usage editorial draft; replace with figma-extract-usage once Figma Do/Don't cards authored."
  - "STUB GAP-004 — Component keys missing (Desktop Bridge required)."
  - "STUB GAP-005 — Token alias chains unconfirmed (Desktop Bridge or Enterprise API required)."
  - "STUB GAP-008 — Spacing token CSS variable names unresolved (run get-theme-tokens category=spacing)."
  - "SKIP GAP-007 — Toggle Input individual importability unconfirmed; check package exports manually."
siblings:
  - "[[ToggleButton.props]]"
  - "[[ToggleButton.anatomy]]"
  - "[[ToggleButton.tokens]]"
  - "[[ToggleButton.usage]]"
  - "[[ToggleButton.accessibility]]"
  - "[[ToggleButton.platform]]"
  - "[[ToggleButton.composition]]"
tags:
  - oxygen
  - component/ToggleButton
  - role/hub
  - stage/draft
  - category/form_inputs
---

## Overview

`ToggleButton` is a controlled binary switch with an associated label, imported from `@8x8/oxygen-toggle-button`. The consuming application owns `isChecked` and updates it via `onChange`; the component has no internal state. The package exports `ToggleButtonGroup`, a vertical or horizontal wrapper for multiple toggles with optional header and footer slots.

> **Status: draft** — 2 CONFLICTs from the audit remain open. GAP-001 (Figma `isOn?` → OX `isChecked` naming divergence) is documented and marked. GAP-002 (`ToggleButtonGroup.isError` — design specifies this, OX API does not) requires designer/developer confirmation before the props and examples spokes can be finalised.

## Spokes

- [[ToggleButton.props]] — 14 props including `isChecked`, `isDisabled`, `infoBoxText`; plus 2 `ToggleButtonGroup` props (`isHorizontal`, `children`)
- [[ToggleButton.anatomy]] — 3 component sets (Toggle Input, Toggle, Toggle Group) across 4 variant axes, 4 interaction states; 2 CONFLICT markers + 2 STUB markers
- [[ToggleButton.tokens]] — 11 color tokens covering base, focus, label, feedback; typography tokens; spacing token CSS variable names unresolved (STUB GAP-008)
- [[ToggleButton.usage]] — 5 Do/Don't pairs covering binary state use, controlled state, label-less variant, info tooltip pairing, and error composition; editorial draft (STUB GAP-003)
- [[ToggleButton.accessibility]] — keyboard (`Tab`, `Space`), ARIA (`checkbox` role, `aria-checked`), focus (full-row ring), WCAG 2.1 AA checklist
- [[ToggleButton.platform]] — no PUI requirements
- [[ToggleButton.composition]] — `ToggleButton` used inside `ToggleButtonGroup`; adjacent `IconButton` pattern; composed error state; related to `Tooltip`, `Radio`, `Checkbox`
