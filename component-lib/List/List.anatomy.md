---
parent: "[[List]]"
section: anatomy
pipeline_stage: draft
tags:
  - component/List
  - role/anatomy
---

## Variants

Eight distinct `ListItem` variant types, each a separate `COMPONENT_SET` in Figma:

| # | Variant type | Variant axes |
|---|-------------|--------------|
| 1 | Single Action or Select | mode, state, selected? |
| 2 | Destructive | mode, state |
| 3 | Checkbox | mode, state, selected? (+ indeterminate) |
| 4 | Radio | mode, state, selected? |
| 5 | Add Item | mode, state |
| 6 | Sub Menu | mode, state |
| 7 | Collapsible | mode, state, open? |
| 8 | Remove Item | mode, state |

## Anatomy — Single Action or Select

Internal layer tree for `Single Action or Select — light / rest / selected=true`:

| Layer | Type | Size | Role |
|-------|------|------|------|
| Leading Visuals/Icon | INSTANCE | 24×24 px | Optional slot (hidden by default); `INSTANCE_SWAP` accepts Icon, Avatar, Status |
| Text Info | FRAME | 240×24 px | Vertical auto-layout content container |
| List Label (primary text) | TEXT | — | 14 px Inter Regular; `text/textColor01` |
| view-badge | FRAME | 16×20 px | Optional badge slot (hidden by default); controlled by `hasBadge` |
| Sub List Label (secondary text) | TEXT | — | 12 px Inter Regular; `text/textColor02`; controlled by `secondaryText?` |
| selectionVariant/single:true | INSTANCE | 24×24 px | Trailing checkmark; `icon/icon01`; visible when `selected?=true` |

## States

| State | Trigger | Background | Visual notes |
|-------|---------|------------|--------------|
| `rest` | Default | `ui/ui06` (`#FFFFFF` light / `#171719` dark) | — |
| `hover` | Pointer over item | `ui/ui02` (`#F4F3EE` light / `#3D3D3D` dark) | — |
| `active` | Pointer down | `ui/ui01` (`#EBEAE1` light / `#666666` dark) | — |
| `focus` | Keyboard Tab | `ui/ui06` (no bg change) | Focus ring expected — implementation unconfirmed |
| `disabled` | `state=disabled` | `ui/ui06` (no bg change) | Opacity reduction applied |
| `selected?=true` | Programmatic | `ui/ui06` (no bg change vs unselected) | Trailing icon becomes visible; selection is icon-only |
| `open?=yes` | Collapsible trigger | No bg change | Height expands 40 px → 108 px |

## Container dimensions

| Property | Value | Notes |
|----------|-------|-------|
| Width | 296 px | Fixed |
| Height (standard) | 40 px | All variants except Collapsible open |
| Height (Collapsible open) | 108 px | Expands downward |
| Padding left/right | 12 px | Hardcoded — no token binding |
| Padding top/bottom | 8 px | Hardcoded — no token binding |
| Gap between children | 8 px | Between leading visual, text block, trailing visual |
| Leading/trailing visual size | 24×24 px | Includes 2 px internal padding → 20 px rendered icon |

Auto-layout direction: **HORIZONTAL** · primary axis: **MIN** (start) · counter axis: **MIN** (top)

<!-- STUB:GAP-007 source="Ask designer to add a11y annotations (ARIA role, focus order, keyboard interactions) to at least the Single Action or Select variant Figma frame" -->

<!-- source: figma-only -->

_Source: Figma MCP · figma-console MCP (Desktop Bridge) · Extracted 2026-05-08_
