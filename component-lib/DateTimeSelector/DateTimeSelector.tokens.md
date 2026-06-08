---
parent: "[[DateTimeSelector]]"
section: tokens
---

<!-- STUB:GAP-002 source="Run figma_get_variables on UI-Foundations library file (iVY5nI8JAxM05Apnnvozzs) filtering for token names in source/DateTimeSelector-figma.md color table. Update with confirmed semantic token names from the variables panel." -->

## Tokens from Figma (CSS-derived)

> CSS-derived from Figma design context (`get_design_context`). Pending confirmation against UI-Foundations variable panel (`iVY5nI8JAxM05Apnnvozzs`). See GAP-002.

### Color tokens

| Token | Element | State | Hex (observed) |
|-------|---------|-------|----------------|
| `--ui/ui05` | Dropdown background | Rest, Focus, Error | `#f4f3ee` |
| `--text/textcolor01` | Label text, Filled value text | All | `#26252a` |
| `--text/textcolor02` | Placeholder text, Hint text | Rest, Focus | `#6c6862` |
| `--error/error01` | Required `*`, Error border, Error message | Error | `#cb2233` |
| `--interactive/focus01` | Focus ring | Focus | `#0056e0` |

> Hover and Disabled state token values not confirmed — see GAP-008.

### Typography tokens

| Token | Element | Size | Weight | Line height | Letter spacing |
|-------|---------|------|--------|-------------|----------------|
| `body01` | Label | 14px | 400 | 20px | −0.06px |
| `bodybold01` | Required asterisk | 14px | 600 | 20px | −0.06px |
| `body02` | Placeholder / value | 16px | 400 | 24px | +0.0121px |
| `label01` | Hint text, Error text | 12px | 400 | 16px | 0px |

### Hardcoded values (no token binding)

| Property | Value |
|----------|-------|
| Dropdown width | 320px |
| Dropdown border radius | 6px |
| Container gap | 4px |
| Text / icon gap | 8px |
| Error border width | 2px |
| Icon Button border radius | 6px |
| Icon Button padding | 2px |

## Visual states reference

| State | Token coverage |
|-------|----------------|
| Rest | `--ui/ui05` surface; `--text/textcolor01` label; `--text/textcolor02` placeholder |
| Hover | Unconfirmed (see GAP-008) |
| Focus | `--interactive/focus01` focus ring |
| Disabled | Unconfirmed (see GAP-008) |
| Error | `--error/error01` border + icon + message; `--ui/ui05` background |
| Filled | `--text/textcolor01` value text (likely; see GAP-002) |
