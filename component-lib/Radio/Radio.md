---
component: Radio
status: partial
package: "@8x8/oxygen-radio"
category: form_inputs
variants:
  - Vertical
  - Horizontal
props:
  - testId: string
  - label: node
  - value: "number | string | bool | { id: string }"
  - name: string
  - isChecked: bool
  - isDisabled: bool
  - onChange: func
  - infoBoxText: node
  - infoBoxButtonLabel: string
  - "RadioGroup.children": ReactNode
  - "RadioGroup.value": Value
  - "RadioGroup.onChange": function
  - "RadioGroup.isHorizontal": boolean
  - "RadioGroup.name": string
subcomponents: []
related:
  - "[[RadioGroup]]"
  - "[[Checkbox]]"
  - "[[Select]]"
  - "[[ToggleButton]]"
patterns:
  - "[[Forms]]"
  - "[[FormField]]"
tokens:
  - "$spacing(2)"
spokes:
  - "[[Radio.props]]"
  - "[[Radio.anatomy]]"
  - "[[Radio.tokens]]"
  - "[[Radio.usage]]"
  - "[[Radio.accessibility]]"
  - "[[Radio.platform]]"
  - "[[Radio.composition]]"
tags:
  - oxygen
  - component/Radio
  - role/hub
  - stage/spec_ready
  - category/form_inputs
---

## Overview

`@8x8/oxygen-radio` exports two co-dependent components: `Radio` (a single option) and `RadioGroup` (the container that manages selection state). A `Radio` is always nested inside a `RadioGroup` — the group enforces single-select by comparing its `value` prop against each child's `value` prop. The component supports vertical (default) and horizontal layouts, optional disabled options, and an inline info-tooltip via `infoBoxText`.

## Spokes

- [[Radio.props]] — 9 Radio props + 5 RadioGroup props including testId, value, isChecked
- [[Radio.anatomy]] — 2 variants (vertical, horizontal), 8 states; visual structure stub pending figma-extract (GAP-001)
- [[Radio.tokens]] — 1 spacing token (`$spacing(2)` = 8px); per-state colour/border/shadow tokens stub pending figma-extract (GAP-003)
- [[Radio.usage]] — 6 Do/Don't pairs covering single-select semantics, default preselection, grouping, list length, label brevity, layout direction
- [[Radio.accessibility]] — keyboard, ARIA, focus — WCAG 2.1 AA checklist (8 criteria)
- [[Radio.platform]] — no PUI requirements (GAP-002 stub; pui-mcp-extract confirmation pending)
- [[Radio.composition]] — always used inside RadioGroup; FormField Slot pattern for hint/error; info tooltip composition
