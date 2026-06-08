---
component: Checkbox
package: "@8x8/oxygen-checkbox"
status: partial
category: form_inputs
figma: "https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=51776:5078"
variants: [Unchecked, Checked, Indeterminate, Disabled]
props:
  - testId: string
  - id: string
  - label: node
  - value: number|string|bool|shape
  - name: string
  - infoBoxText: node
  - infoBoxButtonLabel: string
  - isChecked: boolean
  - isDisabled: boolean
  - isIndeterminate: boolean
  - showLabelTooltipOnOverflow: boolean
  - onBlur: function
  - onChange: function
  - onFocus: function
  - isHorizontal: boolean
subcomponents: ["[[Tooltip]]", "[[Icon]]"]
related: ["[[Radio]]", "[[ToggleButton]]", "[[TextInput]]"]
patterns: ["[[Forms]]"]
tokens: ["[[--ui/ui21]]", "[[--ui/ui22]]", "[[--interactive/disabled02]]", "[[--interactive/focus01]]", "[[--text/textcolor01]]", "[[--error/error01]]"]
spokes:
  - "[[Checkbox.props]]"
  - "[[Checkbox.anatomy]]"
  - "[[Checkbox.tokens]]"
  - "[[Checkbox.usage]]"
  - "[[Checkbox.accessibility]]"
  - "[[Checkbox.platform]]"
  - "[[Checkbox.composition]]"
tags: [component, form_inputs, interactive]
---

## Overview

Checkbox is the canonical multi-select affordance in 8x8 products — form filters, permission lists, terms-and-conditions acknowledgements, and "select all" patterns. Each checkbox is independent (selecting one does not unselect another) unless nested under a parent, where the parent reflects the aggregate state of its children via `isIndeterminate`. One package, `@8x8/oxygen-checkbox`, exports `Checkbox` (default) and `CheckboxGroup` (named).

> **Status: partial.** All remaining gaps are minor — `CheckboxGroup` API is incomplete (GAP-008), usage Do/Don't pairs are editorial rather than Figma-native (GAP-001), and Storybook code examples / input-label spacing / typography tokens / component descriptions are pending upstream (GAP-003/004/005/006). Component is **Beta**.

## Spokes

- [[Checkbox.props]] — 14 `Checkbox` props (incl. `label`, `isChecked`, `isIndeterminate`, `infoBoxText`) + `CheckboxGroup.isHorizontal`; Beta API, CheckboxGroup incomplete (GAP-008)
- [[Checkbox.anatomy]] — 3 Figma component sets (Input, full, Group), 6 parts; 6 variant axes (24 variants each), 7-state matrix; input-label gap unmeasured (GAP-004)
- [[Checkbox.tokens]] — 6 confirmed color/state bindings + 2 spacing tokens covering border, fill, disabled, focus, label, error; typography pending (GAP-003)
- [[Checkbox.usage]] — 7 Do/Don't pairs covering multi-select vs single-select, binary commitment, indeterminate, labelling, grouping, error handling, info tooltips (editorial)
- [[Checkbox.accessibility]] — native `checkbox` role, keyboard map, `aria-checked` states, group + error patterns, WCAG 2.1 AA checklist
- [[Checkbox.platform]] — no PUI requirements
- [[Checkbox.composition]] — renders [[Tooltip]] + [[Icon]] (infoBox); grouped via `CheckboxGroup`; related [[Radio]], [[ToggleButton]], Forms
