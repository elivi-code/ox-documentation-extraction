---
parent: "[[ToggleButton]]"
section: tokens
pipeline_stage: draft
tags:
  - oxygen
  - component/ToggleButton
  - role/spoke
  - section/tokens
---

<!-- STUB:GAP-005 source="Enable Figma Desktop Bridge or obtain Enterprise API access; re-run figma_get_variables with resolveAliases=true against file 5YihJ5WuDvnvrlrRMC4sBp to confirm token alias chains (e.g. whether --ui/ui33 resolves via a collection alias)" -->
<!-- STUB:GAP-008 source="Run mcp__oxygen-mcp__get-theme-tokens category=spacing to resolve $spacing02 and $spacing03 against the Oxygen spacing token table and update with canonical CSS variable names" -->

## Color tokens

### Toggle Base (pill background)

| State | Token | Light | Dark |
|---|---|---|---|
| Default (off) | `--ui/ui33` | `#6c6862` | `#858585` |
| On / checked | `--actions/action01` | `#0056e0` | `#4687ed` |
| Disabled (any) | `--ui/ui33` | `#6c6862` | `#858585` |

### Focus ring — Toggle Input (switch only)

| State | Token | Light | Dark |
|---|---|---|---|
| Focused | `--interactive/focus01` | `#0056e0` (box-shadow) | `#d7e3f9` (box-shadow) |

### Focus ring — Toggle (full component)

| State | Token | Light | Dark |
|---|---|---|---|
| Focused border | `--ui/ui06` | `white` | `#171719` |
| Focused shadow | `--interactive/focus01` | `#0056e0` | `#d7e3f9` |

### Label text

| State | Token | Light | Dark |
|---|---|---|---|
| Default | `--text/textcolor01` | `#26252a` | `white` |
| Disabled | `--interactive/disabled02` | `#c8c8bd` | `#666666` |

### Required asterisk

| State | Token | Light | Dark |
|---|---|---|---|
| Default | `--actions/action03` | `#cb2233` | `#d83848` |

### Toggle Group — Feedback area

| Element | Token | Light | Dark |
|---|---|---|---|
| Helper text | `--text/textcolor02` | `#6c6862` | `#c2c2c2` |
| Error message text | `--error/error01` | `#cb2233` | `#f24d5f` |

### Toggle Group — Slot placeholder

| Element | Token | Light | Dark |
|---|---|---|---|
| Slot background | `--ui/ui23` | `#e7e3ff` | `#3c2f8e` |
| Slot border | `--ui/ui22` | `#0056e0` | `#ccddf9` |

## Toggle Knot (thumb)

No token bindings on the knot itself — rendered as image assets with three variants:

- **Normal:** white/standard knot
- **Disabled – Light mode:** muted knot
- **Disabled – Dark mode:** muted knot (dark palette)

## Typography tokens

| Token | Weight | Size | Line height | Letter spacing | Used on |
|---|---|---|---|---|---|
| `typography/body01` | 400 (Regular) | 14px | 20px | −0.06px | Label text |
| `typography/bodyBold01` | 600 (Semi Bold) | 14px | 20px | −0.06px | Required asterisk |
| `typography/label01` | 400 (Regular) | 12px | 16px | 0px | Helper/error message |
| `typography/heading01` | 600 (Semi Bold) | 20px | 28px | 0.0289px | Slot heading (Toggle Group) |

Font family: Inter (via `typography/body01/font-family`)

## Spacing tokens

<!-- STUB:GAP-008 source="Run get-theme-tokens category=spacing to confirm canonical CSS variable names for the values below" -->

| Usage | Value | Figma token (legacy) | OX CSS variable |
|---|---|---|---|
| Gap between stacked Toggle items | 8px | `$spacing03` | _unresolved — see GAP-008_ |
| Gap between Toggle and adjacent Icon Button | 4px | `$spacing02` | _unresolved — see GAP-008_ |

## Effect styles

No shared Figma effect styles — focus ring uses `box-shadow` inline, not a shared style.

_Source: Oxygen MCP + Figma MCP · Extracted 2026-04-29_
