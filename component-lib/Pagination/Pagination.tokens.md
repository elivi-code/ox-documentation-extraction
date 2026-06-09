---
parent: "[[Pagination]]"
section: tokens
---

<!-- source: figma-only -->

> Token data is sourced from Figma variable bindings confirmed via batch alias-chain traversal 2026-05-05. OX MCP returned 0 theme tokens for the `pagination` search query (GAP-001).

## Color Tokens

| Token | Light value | Dark value | Element | State |
|-------|-------------|------------|---------|-------|
| `--text/textcolor01` | `#26252a` | `#ffffff` | All text labels ("Rows per page:", "Page", "of N pages", Select input value) | enabled |
| `--ui/ui05` | `#f4f3ee` | `#2f2e32` | Select dropdown background (rows-per-page + page selects) | enabled |
| `--interactive/disabled01` | `#c8c8bd` | `#c2c2c2` | Select dropdown background (rows-per-page + page selects) | disabled |
| `--interactive/disabled04` | `#8d8b7e` | `#858585` | Select input text | disabled |
| `--interactive/focus01` | `#0056e0` | `#d7e3f9` | Focus ring (all interactive controls) | focus — advisory; not yet modelled in Figma variant set |

> All hex values confirmed via batch alias-chain traversal 2026-05-05. `--interactive/focus01` confirmed in batch run; not yet reflected in `source/Pagination-figma.md`.

## Typography Tokens

| Token | Size | Weight | Line height | Letter spacing | Used for |
|-------|------|--------|-------------|----------------|----------|
| `typography/body01/*` | `14px` | `400` | `20px` | `-0.06px` | All text — default size variant |
| `typography/label01/*` | `12px` | `400` | `16px` | `0px` | All text — small size variant |

<!-- STUB:GAP-013 source="Verify typography token names (typography/body01/*, typography/label01/*) against the Oxygen design system style library when Figma API access improves — figma_get_styles returned 0 styles" -->

## Hardcoded Values (Not Tokenised)

<!-- STUB:GAP-012 source="Design system team to evaluate whether Select widths (88px/72px), container widths (640px/547px/288px), button paddings (10px/6px/4px), and border-radius (6px) should be tokenised" -->

10 hardcoded pixel values with no token binding:

| Value | Location |
|-------|----------|
| `88px` | Select width (rows + page dropdowns), default size |
| `72px` | Select width (rows + page dropdowns), small size |
| `640px` | Container width, > 548px breakpoint |
| `547px` max / `288px` min | Container width, < 548px breakpoint |
| `10px` | previousButton / nextButton padding, default size, > 548px |
| `6px` | previousButton / nextButton padding, small size, > 548px |
| `4px` | previousButton / nextButton padding, < 548px |
| `6px` | Border radius, all interactive elements |

## Size Variants

| Size | Prop value | Container height | Typography |
|------|-----------|-----------------|------------|
| Default | _(omit `size`)_ | `40px` | `typography/body01/*` — 14px/20px lh |
| Small | `"small"` | `32px` | `typography/label01/*` — 12px/16px lh |

## OX MCP Token Gap

<!-- STUB:GAP-001 source="Run get-theme-tokens with alternative search terms (e.g. 'select', 'ui05', 'interactive') or check if Pagination inherits tokens from Select/Button components upstream — OX MCP returned 0 results for 'pagination' search" -->

<!-- STUB:GAP-002 source="Re-run figma-extract with Figma Desktop Bridge plugin active to obtain complete variable collection via the Variables API — tokens confirmed via batch alias-chain traversal 2026-05-05 as an alternative; API gap remains open" -->
