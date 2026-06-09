---
component: Tooltip
package: "@8x8/oxygen-tooltip"
category: overlays_contextual
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Tooltip/props]]"
  - "[[Tooltip/examples]]"
  - "[[Tooltip/accessibility]]"
  - "[[Tooltip/Tooltip-figma]]"
  - "[[Tooltip/Tooltip-usage]]"
  - "[[Tooltip/Tooltip-pui]]"
  - "[[Tooltip/Tooltip-audit]]"
tags:
  - oxygen
  - component/Tooltip
  - role/tokens
  - stage/blocked
  - category/overlays_contextual
---
# Tooltip — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

## Theme tokens

The Oxygen MCP returned **no tooltip-specific theme tokens** (0 matches for `tooltip`).

Tooltip visual styles are likely defined as internal component styles rather than exposed design tokens. To inspect the actual CSS variables, refer to the Figma token library or the component source in `@8x8/oxygen-tooltip`.

## Size constraints (from usage docs)

| Property | Value |
|----------|-------|
| Min width | `40px` |
| Max width | `320px` |

## Behaviour constants

| Property | Value |
|----------|-------|
| Default show delay | `300ms` (`delay` prop default) |
| Hide delay | None (hides immediately on cursor leave) |
| Max content length | 140 characters (English) |

## Orientation × arrow

| Prop | Effect |
|------|--------|
| `orientation` | Controls which side the tooltip appears on relative to its trigger |
| `enableArrow` | Adds a directional pointer on the tooltip container |
| `offset` / `modifiers` | Fine-tune distance and alignment |

---

> **SOURCE_GAP:** No CSS custom properties or design token names are exposed for Tooltip in the Oxygen MCP. Tokens (background, text colour, border-radius, shadow) need to be verified in Figma or component source.

---

_Source: Oxygen MCP · Extracted 2026-05-05_
