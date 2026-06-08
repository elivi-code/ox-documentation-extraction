---
parent: "[[Input]]"
section: tokens
tags: [oxygen, component/Input, role/tokens]
---

<!-- source: figma-only for dark-mode token values — resolved 2026-05-05 via figma_execute alias-chain traversal; tokens.md still shows stale "*(dark value not captured)*" entries -->

## Color tokens

All values from `Input-figma.md` (post-2026-05-05 resolution). Dark values in `tokens.md` source file are stale — use the table below.

<!-- STUB:GAP-010 source="Update tokens.md textColor02 dark value to #C2C2C2 (confirmed in Input-figma.md 2026-05-05)" -->
<!-- STUB:GAP-011 source="Update tokens.md error01 dark value to #F24D5F (confirmed in Input-figma.md 2026-05-05)" -->

### Background

| Token | CSS var | Light | Dark | Applied to |
|---|---|---|---|---|
| `ui05` | `--ui/ui05` | `#F4F3EE` | `#2F2E32` | Field background — Rest, Focus, Filled, Read Only states |
| `hover06` | `--hover/hover06` | `#EBEAE1` | `#666666` | Field background — Hover state |
| `interactive/disabled01` | `--interactive/disabled01` | `#C8C8BD` | `#C2C2C2` | Field background — Disabled state |

### Interactive

| Token | CSS var | Light | Dark | Applied to |
|---|---|---|---|---|
| `interactive/focus01` | `--interactive/focus01` | `#0056E0` | `#D7E3F9` | Focus ring/border on field (Rest→Focus, Error→Focus) |

### Text

| Token | CSS var | Light | Dark | Applied to |
|---|---|---|---|---|
| `text/textColor01` | `--text/textColor01` | `#26252A` | `#FFFFFF` | Label text, filled value text |
| `text/textColor02` | `--text/textColor02` | `#6C6862` | `#C2C2C2` | Placeholder text, helper/hint text |

### Error

| Token | CSS var | Light | Dark | Applied to |
|---|---|---|---|---|
| `error/error01` | `--error/error01` | `#CB2233` | `#F24D5F` | Required `*`, error border, error message text |

---

## Typography tokens

| Token | Size | Weight | Line-height | Letter-spacing | Used for |
|---|---|---|---|---|---|
| `typography/body01` | 14 px | 400 | 20 px | −0.06 px | Label text |
| `typography/bodyBold01` | 14 px | 600 | 20 px | −0.06 px | Required `*` |
| `typography/body02` | 16 px | 400 | 24 px | 0.0121 px | Input text, placeholder |
| `typography/label01` | 12 px | 400 | 16 px | 0 px | Helper/hint text |

Font family: `Inter` (Regular and Semi Bold).

---

## Spacing (hardcoded — no token bindings found)

| Property | Value | Applied to |
|---|---|---|
| `padding-x` | 16 px | All field containers |
| `padding-y` | 12 px | All field containers |
| `border-radius` | 6 px | All field containers |
| Label-to-field gap | 4 px | Root vertical gap |
| Icon-to-input gap | 8 px | Search input `Text Field` only |
| Inner text area height | 88 px (Large) | Text area inner textarea |

> Variables API was unavailable during extraction; these hardcoded values may map to spacing tokens. Re-extract when Desktop Bridge is connected to verify.

---

## Size variant heights (no tokens — fixed pixel values)

| OX size | Text input | Text area | Search input |
|---|---|---|---|
| `small` | 76 px | 90 px | 76 px |
| `medium` | 84 px | 124 px | 84 px |
| `large` | 92 px | 156 px | 92 px |

---

## Token wikilinks

[[token.ui.ui05]] · [[token.hover.hover06]] · [[token.interactive.disabled01]] · [[token.interactive.focus01]] · [[token.text.textColor01]] · [[token.text.textColor02]] · [[token.error.error01]] · [[token.typography.body01]] · [[token.typography.bodyBold01]] · [[token.typography.body02]] · [[token.typography.label01]]
