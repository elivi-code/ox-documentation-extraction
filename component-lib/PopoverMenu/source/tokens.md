---
component: PopoverMenu
package: "@8x8/oxygen-popover"
category: overlays_contextual
role: tokens
role_description: "Design token bindings — colors, spacing, typography per component state"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
siblings:
  - "[[PopoverMenu/props]]"
  - "[[PopoverMenu/examples]]"
  - "[[PopoverMenu/accessibility]]"
  - "[[PopoverMenu/PopoverMenu-figma]]"
  - "[[PopoverMenu/PopoverMenu-usage]]"
  - "[[PopoverMenu/PopoverMenu-audit]]"
tags:
  - oxygen
  - component/PopoverMenu
  - role/tokens
  - stage/blocked
  - category/overlays_contextual
---

# PopoverMenu — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

## Theme tokens

> **SOURCE_GAP (GAP-005):** The Oxygen MCP returned **no theme tokens** for the `popover` component family (`totalMatches: 0`). All tokens below are sourced from Figma design context (`PopoverMenu-figma.md`) — semantic descriptions and collection names are absent pending resolution via the UI-Foundations library (file key `iVY5nI8JAxM05Apnnvozzs`).

### Container (Popover window)

| Token | Element | Light value | Dark value |
|---|---|---|---|
| `--ui/ui06` | Background | `white` | `#171719` |
| `--ui/ui01` | Border | `#ebeae1` | `#666` |
| `--ui/shadow01` | Box shadow | `rgba(41,41,41,0.25)` 6px 0px 2px | `#141414` 8px 2px 2px |

### Header

| Token | Element | Light value | Dark value |
|---|---|---|---|
| `--text/textcolor01` | Title text | `#26252a` | `white` |
| `--typography/bodybold01/*` | Title typography | Inter Semi Bold, 14px / 20px lh | — |
| `--ui/ui05` | Search field background | `#f4f3ee` | `#2f2e32` |
| `--text/textcolor02` | Search placeholder text | `#6c6862` | `#c2c2c2` |
| `--typography/body01/*` | Search placeholder typography | Inter Regular, 14px / 20px lh | — |
| `--ui/ui01` | Header divider | `#ebeae1` | `#666` |

### Content slot

| Token | Element | Light value | Dark value |
|---|---|---|---|
| `--ui/ui23` | Slot background | `#e7e3ff` | `#3c2f8e` |
| `--ui/ui22` | Slot border | `#0056e0` | `#ccddf9` |
| `--typography/heading01/*` | Slot heading typography | Inter Semi Bold, 20px / 28px lh | — |

### Footer

| Token | Element | Light value | Dark value |
|---|---|---|---|
| `--ui/ui06` | Footer background | `white` | `#171719` |
| `--ui/ui01` | Footer divider | `#ebeae1` | `#666` |
| `--actions/action03` | Clear button text | `#cb2233` | `#d83848` |
| `--actions/action08` | Cancel button text | `#0056e0` | `#99bbf3` |
| `--actions/action09` | Apply button background | `#0056e0` | `#4687ed` |
| `--text/textcolor09` | Apply button text | `white` | `black` ⚠️ |
| `--typography/labelbold01/*` | Button typography | Inter Semi Bold, 12px / 16px lh | — |

> ⚠️ `--text/textcolor09` resolves to `black` in dark mode on `--actions/action09` (`#4687ed`) — contrast ratio approximately 3.4:1, below WCAG AA 4.5:1. See GAP-003 in `PopoverMenu-audit.md`.

---

## Hardcoded values (not tokenised)

> **SOURCE_GAP (GAP-011):** The following values are hardcoded in Figma with no token binding. Flagged for tokenisation by the Oxygen design team.

| Element | Property | Value |
|---|---|---|
| Container | border-radius | `6px` |
| Container | width | `320px` |
| Container | max-height | `400px` |
| Container | max-width | `1064px` |
| Container | padding | `1px 9px` |
| Header title row | padding | `4px 12px 8px 12px` |
| Header search input | padding | `4px 12px 12px 12px` |
| Footer buttons (light) | padding | `8px 8px 0 8px` |
| Footer buttons (dark) | padding | `8px 12px 0 12px` ⚠️ |
| Scrollbar thumb | background | `#c1c1c1` |
| Scrollbar track | background | `#fafafa` |

---

## Variants and sizes

No variant or size tokens were returned by the MCP. The `PopoverMenu` does not expose a `size` or `variant` prop — the panel dimensions are controlled via:

- `maxHeight` (numeric prop, pixels)
- `placement` (positional, not dimensional)

There are no documented color variants or size tokens at this time (`SOURCE_GAP`).

---

_Source: Oxygen MCP · Extracted 2026-05-08_
