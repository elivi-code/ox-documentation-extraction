---
parent: "[[Label]]"
section: tokens
---

## Color tokens

| Token | Light | Dark | Element | State |
|-------|-------|------|---------|-------|
| `text/textColor01` | `#26252a` | `#ffffff` | Label text | Default |
| `error/error01` | `#cb2233` | `#f24d5f` | Required asterisk (`*`) | `isRequired` |

> `text/textColor01` references `colorPalette.offwhite02` in light mode and `colorPalette.white` in dark mode.

## Typography tokens

> **GAP-008 resolved 2026-06-08:** Figma is authoritative. `@8x8/oxygen-label` uses `typography/body01` / `typography/bodyBold01` (14px). The MCP-returned `label01` / `labelBold01` (12px) were incorrect global theme matches and do not apply to this component.

| Token | Family | Size | Line height | Weight | Letter spacing | Element |
|-------|--------|------|-------------|--------|----------------|---------|
| `typography/body01` | Inter | 14px | 20px | 400 (Regular) | −0.06px | Label text |
| `typography/bodyBold01` | Inter | 14px | 20px | 600 (SemiBold) | −0.06px | Required asterisk |

## Hardcoded values (no token bindings)

| Property | Value | Element |
|----------|-------|---------|
| `gap` | `4px` | H Stack (label text ↔ Icon Button) |
| `padding` | `2px` (all sides) | Icon Button wrapper |
| `border-radius` | `6px` | Icon Button wrapper |

## Token notes

- `ui/ui06` (`#171719`) appears in the Figma showcase frame only as a dark background surface — it is not a Label component token.
- `label01` / `labelBold01` (12px) were returned by the MCP as theme-level matches but are not consumed by `@8x8/oxygen-label` — confirmed via Figma comparison (GAP-008 resolved).

_Source: Oxygen MCP · Figma MCP · Extracted 2026-05-01 · GAP-009 applied, GAP-008 resolved 2026-06-08_
