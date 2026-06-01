---
component: Breadcrumbs
package: "@8x8/oxygen-breadcrumbs"
category: navigation
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Breadcrumbs/props]]"
  - "[[Breadcrumbs/examples]]"
  - "[[Breadcrumbs/accessibility]]"
  - "[[Breadcrumbs/Breadcrumbs-figma]]"
  - "[[Breadcrumbs/Breadcrumbs-usage]]"
  - "[[Breadcrumbs/Breadcrumbs-pui]]"
  - "[[Breadcrumbs/Breadcrumbs-audit]]"
tags:
  - oxygen
  - component/Breadcrumbs
  - role/tokens
  - stage/spec_ready
  - category/navigation
---
# Breadcrumbs — Tokens

> **See also:** [props.md](props.md) | [examples.md](examples.md) | [accessibility.md](accessibility.md) | [Breadcrumbs-figma.md](Breadcrumbs-figma.md) | [Breadcrumbs-usage.md](Breadcrumbs-usage.md)

## Theme tokens

`get-theme-tokens` returned no results for the query `"breadcrumb"`. No Oxygen theme tokens are currently mapped to this component in the MCP.

The `Breadcrumbs` component accepts a `theme` prop (type `object`) for direct theming, but its shape is not documented by the MCP.

## Figma-extracted token bindings

> **Confidence: Figma design context (not MCP-registered).** The token names below were read from CSS variable references in the Figma design context (file `5YihJ5WuDvnvrlrRMC4sBp`, node `21927:40413`), migrated from [Breadcrumbs-figma.md](Breadcrumbs-figma.md) `## Color & token bindings` / `## Text styles`. They are **design intent**, not confirmed entries in the `@8x8/oxygen-tokens` registry (`get-theme-tokens` returned 0 results — see GAP-001). Only **rest-state** bindings were resolved; hover/active/focus tokens remain unresolved (GAP-003). Verify against `@8x8/oxygen-tokens` before use in implementation.

### Color tokens

| Token | Collection | Light | Dark | Element(s) |
|-------|------------|-------|------|------------|
| `--actions/action08` | actions | `#0056e0` | `#99bbf3` | Link label (`_Text link breadcrumb`, rest); ellipsis button (`_Text link elipsis`, rest) |
| `--interactive/active07` | interactive | `#0045b3` | `#0056e0` | Ellipsis button — menu open / active |
| `--text/textcolor01` | text | `#26252a` | `white` | `/` separator; current-page label |
| `--ui/ui01` | ui | `#ebeae1` | — (hardcoded `#666` in dark) | Overflow Menu border (light mode only) |

> **Hardcoded (no token binding) — Overflow Menu container:** background `white` / `#171719`; box-shadow `rgba(41,41,41,0.25)` / `#141414`; border-radius `6px`; width `160px`; padding-y `9px`. See [Breadcrumbs-figma.md](Breadcrumbs-figma.md) `## Token coverage`.

### Typography tokens

| Token | Size | Weight | Line height | Letter spacing | Element(s) |
|-------|------|--------|-------------|----------------|------------|
| `--typography/body01/*` | 14 px | 400 | 20 px | −0.06 px | All text (links, separator, current page) |

## Known visual states

The following states are documented in the design but their token mappings are unresolved:

| State | Description |
|-------|-------------|
| Rest | Default appearance of a breadcrumb link |
| Hover | Visual feedback when the cursor is over a link |
| Active | The current page item (`isActive`), rendered as plain text |
| Focus | Keyboard-focus ring on a focusable breadcrumb link |

> **SOURCE_GAP:** Token definitions for breadcrumb link colours, separator colour, and focus ring are not exposed via the Oxygen MCP. Check the component's source stylesheet or raise with the Oxygen team.

_Source: Oxygen MCP · Extracted 2026-04-30_
