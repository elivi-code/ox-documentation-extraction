---
component: TextField
package: "@8x8/oxygen-textField"
category: form_inputs
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[TextField/props]]"
  - "[[TextField/examples]]"
  - "[[TextField/accessibility]]"
  - "[[TextField/figma]]"
  - "[[TextField/TextField-pui]]"
  - "[[TextField/TextField-audit]]"
tags:
  - oxygen
  - component/TextField
  - role/tokens
  - stage/spec_ready
  - category/form_inputs
---
# TextField — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md) · [figma.md](figma.md)

## Input background tokens

| Token | Light | Dark | Usage |
|-------|-------|------|-------|
| `--ui/ui05` | `#F4F3EE` (offwhite10) | `#2F2E32` (purple02) | Input field background (rest & filled states) |
| `--ui/hover06` | `#EBEAE1` (offwhite09) | `#666666` (gray05) | Input hover background |

## Text tokens

| Token | Light | Dark | Usage |
|-------|-------|------|-------|
| `--text/textColor01` | `#26252A` (offwhite02) | `#FFFFFF` (white) | Label text, filled input value text |
| `--text/textColor02` | `#6C6862` *(from Figma)* | — | Placeholder text, hint text |

## Border / UI tokens

| Token | Light | Dark | Usage |
|-------|-------|------|-------|
| `--ui/ui01` | `#EBEAE1` (offwhite09) | `#666666` (gray05) | Primary border, dividers |
| `--ui/ui02` | `#F4F3EE` (offwhite10) | `#3D3D3D` (gray03) | Secondary surface, subtle border |
| `--ui/ui03` | `#ABA999` (offwhite07) | `#858585` (gray06) | Strong border |
| `--ui/ui32` | `#DEDED5` (offwhite085) | `#666666` (gray05) | Strong secondary border/divider |

## Focus tokens

| Token | Light | Dark | Usage |
|-------|-------|------|-------|
| `--interactive/focus01` | `#0056E0` (blue05) | `#D7E3F9` (blue10) | Focus ring (2px border overlay) |
| `--interactive/focus02` | `#D7E3F9` (blue10) | `#0056E0` (blue05) | Inverted focus ring (dark surfaces) |

## Error tokens

| Token | Light | Dark | Usage |
|-------|-------|------|-------|
| `--error/error01` | `#CB2233` *(from Figma)* | — | Error border (2px), error text, required `*` asterisk |

## Typography tokens (from Figma)

| Token | Size | Weight | Line-height | Letter-spacing | Usage |
|-------|------|--------|-------------|----------------|-------|
| `--typography/body01` | 14px | 400 | 20px | -0.06px | Label text, input value text, placeholder |
| `--typography/bodyBold01` | 14px | 600 | 20px | -0.06px | Required asterisk (`*`) |
| `--typography/label01` | 12px | 400 | 16px | 0px | Hint text, error message text |
| `--typography/body02` | 16px | 400 | 24px | 0.0121px | Search input placeholder (large variant) |

## Size dimensions (from Figma)

### Text input heights

| Size prop | Height |
|-----------|--------|
| `large` | 92px |
| `default` (medium) | 84px |
| `small` | 76px |

### Text area heights

| Size prop | Height |
|-----------|--------|
| `large` | 156px |
| `default` (medium) | 124px |
| `small` | 90px |

### Padding

| Component | Padding |
|-----------|---------|
| Text input (all sizes) | `px: 12px`, `py: 10px` |
| Text area | `px: 12px`, `py: 8px` |
| Search input (large) | `px: 16px`, `py: 12px` |

## Border radius

All input variants use `border-radius: 6px`.

_Source: Oxygen MCP + Figma · Extracted 2026-04-29_
