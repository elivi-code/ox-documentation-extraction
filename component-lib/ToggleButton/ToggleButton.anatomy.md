---
parent: "[[ToggleButton]]"
section: anatomy
pipeline_stage: draft
tags:
  - oxygen
  - component/ToggleButton
  - role/spoke
  - section/anatomy
---

<!-- CONFLICT:GAP-001 finding="Figma isOn? property vs OX isChecked prop — same concept, different naming convention. Fix applied: explicit note added to Persistent States table in source/ToggleButton-figma.md." HUMAN DECISION REQUIRED -->
<!-- CONFLICT:GAP-002 finding="Figma ToggleGroup has isError variant (full InlineValidationMessage with --error/error01). OX ToggleButtonGroup has no isError prop — only isHorizontal and children. Design specifies error-state behaviour the API cannot produce. Confirm with designer/developer: (a) add isError to ToggleButtonGroup, or (b) document consumer-composition pattern." HUMAN DECISION REQUIRED -->
<!-- STUB:GAP-004 source="Enable Figma Desktop Bridge; re-run figma_get_component_details for nodes 51776:7539, 51776:7580, 52689:99119 to retrieve component keys" -->
<!-- STUB:GAP-009 source="Inspect hover-state Toggle instances on examples page (node 50606:95349, Col 2 rows 1 and 5) via figma_get_component to determine hover fill tokens" -->

## Component sets

Three Figma component sets compose the ToggleButton family:

| Component set | Node | Size | Purpose |
|---|---|---|---|
| Toggle Input | `51776:7539` | 40×24px | Switch-only, no label |
| Toggle | `51776:7580` | 148×24px default | Switch + label |
| Toggle Group | `52689:99119` | 320px wide | Wrapper with header/slot/footer |

## Anatomy

### Toggle Input (switch-only, 40×24px)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Toggle Base | structural | Rounded pill, 24px border-radius; background changes by state |
| 2 | frame | Toggle Knot | structural | Circular thumb; left=off (~10% from left), right=on (~10% from right); 3 image variants (normal, disabled-light, disabled-dark) |
| 3 | frame | Focus ring | optional slot | Visible only when `isFocus=true` and `isDisabled=false`; 2px box-shadow ring on the switch only |

### Toggle (switch + label, 148×24px default)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | instance | Toggle Input | fixed sub-component | 40×24px switch (see above); shrink-0 |
| 2 | frame | LabelWrapper | structural | `py-2px` vertical padding wrapper; `items-start` |
| 3 | instance | Form Controls Label | content element | 14px Inter Regular; `disabled02` color when disabled |
| 4 | frame | Focus ring | optional slot | Covers **entire** toggle + label area (not just switch); `isFocus=true` only |

### Toggle Group (320px wide)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Toggle Group Label | optional slot | `header` boolean toggle; contains label text + optional info icon button |
| 2 | instance | Slot | content element | Placeholder — swapped with actual toggle content via instance swapper |
| 3 | frame | Toggle Group Feedback Text | optional slot | `footer` boolean toggle; shows helper message or error message when `isError=True` |

## Variant axes

### Toggle Input

| Property | Values | Default |
|---|---|---|
| Mode | Light, Dark | Light |
| isOn? | false, true | false |
| isDisabled? | false, true | false |
| isFocus? | false, true | false |

### Toggle (with label)

| Property | Values | Default |
|---|---|---|
| Mode | Light, Dark | Light |
| isOn? | false, true | false |
| isDisabled? | false, true | false |
| isFocus | false, true | false |

> **Naming divergence (GAP-001 resolved):** Figma `isOn?` maps to OX `isChecked` — same concept, different names.

### Toggle Group

| Property | Values | Default |
|---|---|---|
| Mode | Light, Dark | Light |
| isError | False, True | False |

### Boolean toggles (Toggle Group)

| Property | Default | Notes |
|---|---|---|
| header | true | Shows/hides the Toggle Group Label (label + info icon button) |
| footer | true | Shows/hides the feedback text area (helper or error message) |

## Interaction states

| State | Trigger | Visual change |
|---|---|---|
| hover | pointer over | Not a separate Figma variant — implied in implementation <!-- STUB:GAP-009 source="Inspect hover instances on examples page 50606:95349 to determine hover fill tokens" --> |
| isFocused | keyboard Tab | 2px focus ring; on Toggle Input: ring around switch only; on Toggle: ring covers switch + full label area |
| isOn / isChecked | click or Space | Toggle Base turns blue (`--actions/action01`); knot moves to right |
| isDisabled | `isDisabled?=true` | Toggle Base stays gray (`--ui/ui33`); knot uses disabled-variant image; label text turns `--interactive/disabled02` |
| isError (group) | `isError=True` | Footer shows `InlineValidationMessage` with error icon — **Figma only, not in OX API** <!-- CONFLICT:GAP-002 finding="isError in Figma has no corresponding OX prop" HUMAN DECISION REQUIRED --> |

## Spacing

| Usage | Value | Token |
|---|---|---|
| Gap: switch → label | 12px | — |
| Gap: stacked Toggle items | 8px | `$spacing03` |
| Gap: Toggle → adjacent Icon Button | 4px | `$spacing02` |
| Label vertical padding | 2px top + 2px bottom | — |
| Toggle Group internal gap | 12px | — |

## Auto-layout behaviour

- **Toggle Input:** relative positioning (not auto-layout)
- **Toggle:** horizontal auto-layout, gap 12px, `items-start`
- **Toggle Group:** vertical auto-layout (`flex-col`), gap 12px, `items-start`
- **Multiline label:** switch stays top-aligned (`items-start`); does not centre vertically
- **Browser font scaling:** font size increases but toggle switch stays fixed at 40×24px, aligned to top
- **Browser zoom:** font size and toggle switch both scale proportionally

## Design decisions

> "Use the Toggle Input component if you don't want to include a label. It can be used in scenarios where the function of the Toggle is clear from the context or design of the interface. An example could be a cell within a table or an item in a list."

> "The gap between Toggle items is 8px (represented by `$spacing03`)."

> "Place the icon button to the right of the Toggle component. The gap between the two separate components is 4px, represented by `$spacing02`."

_Source: Figma MCP · figma-console MCP · Extracted 2026-04-29_
