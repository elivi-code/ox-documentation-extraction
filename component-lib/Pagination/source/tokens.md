---
component: Pagination
package: "@8x8/oxygen-pagination"
category: navigation
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Pagination/props]]"
  - "[[Pagination/examples]]"
  - "[[Pagination/accessibility]]"
  - "[[Pagination/Pagination-figma]]"
  - "[[Pagination/Pagination-usage]]"
  - "[[Pagination/Pagination-audit]]"
tags:
  - oxygen
  - component/Pagination
  - role/tokens
  - stage/spec_ready
  - category/navigation
---
# Pagination — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

> **Source note (GAP-003 applied):** Oxygen MCP returned 0 theme tokens for the `pagination` search query (GAP-001 — SOURCE_GAP). Color and typography tokens below are sourced from Figma variable bindings in `Pagination-figma.md`, confirmed via batch alias-chain traversal 2026-05-05.

## Color Tokens

| Token | Light value | Dark value | Element | State |
|-------|-------------|------------|---------|-------|
| `--text/textcolor01` | `#26252a` | `#ffffff` | All text labels ("Rows per page:", "Page", "of N pages", Select input value) | enabled |
| `--ui/ui05` | `#f4f3ee` | `#2f2e32` | Select dropdown background (rows-per-page + page selects) | enabled |
| `--interactive/disabled01` | `#c8c8bd` | `#c2c2c2` | Select dropdown background (rows-per-page + page selects) | disabled |
| `--interactive/disabled04` | `#8d8b7e` | `#858585` | Select input text | disabled |
| `--interactive/focus01` | `#0056e0` | `#d7e3f9` | Focus ring (all interactive controls) | focus — advisory; not yet modelled in Figma variant set |

> Hex values confirmed via batch alias-chain traversal 2026-05-05 (see Pagination-audit.md WARN-002 resolution). `--interactive/focus01` confirmed in batch run but not yet reflected in `Pagination-figma.md`.

## Typography Tokens

| Token | Size | Weight | Line height | Letter spacing | Used for |
|-------|------|--------|-------------|----------------|----------|
| `typography/body01/*` | `14px` | `400` | `20px` | `-0.06px` | All text — default size variant |
| `typography/label01/*` | `12px` | `400` | `16px` | `0px` | All text — small size variant |

> Typography style library names unverified — `figma_get_styles` returned empty (GAP-013 — SOURCE_GAP).

## Hardcoded Values (Not Tokenised)

10 hardcoded pixel values flagged in `Pagination-figma.md` with no token binding (GAP-012 — SOURCE_GAP):

| Value | Location |
|-------|----------|
| `88px` | Select width (rows + page dropdowns), default size |
| `72px` | Select width (rows + page dropdowns), small size |
| `640px` | Container width, > 548px breakpoint |
| `547px` max / `288px` min | Container width, < 548px breakpoint |
| `10px` | previousButton / nextButton padding, default size, > 548px |
| `6px` | previousButton / nextButton padding, small size, > 548px |
| `4px` | previousButton / nextButton padding, small / default size, < 548px |
| `6px` | Border radius, all interactive elements |

## Size Variants

| Size | Prop value | Container height | Typography token |
|------|-----------|-----------------|-----------------|
| Default | _(omit `size` prop)_ | `40px` | `typography/body01/*` |
| Small | `"small"` | `32px` | `typography/label01/*` |

> The `PaginationSize` enum values are inferred from usage docs and Figma — MCP returned the type name without member expansion (GAP-004).

_Source: Figma variable bindings confirmed via batch alias-chain traversal 2026-05-05. Original MCP extraction 2026-05-01. GAP-003 applied by doc-rewrite 2026-06-08._
