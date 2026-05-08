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

## Theme Tokens

The Oxygen MCP returned **no theme tokens** matching the `pagination` search query. No token data is available from this source.

> **Audit note:** This is a potential `SOURCE_GAP` — either the Pagination component does not expose named theme tokens, or they are defined under a different namespace (e.g. inherited from Button or Select tokens used internally). A Figma variable inspection or codebase search may surface token names.

## Size Variants

| Size | Prop value | Notes |
|------|-----------|-------|
| Default | _(omit `size` prop)_ | Standard size |
| Small | `"small"` | Compact layout |

> **Note:** The `PaginationSize` type values were not fully documented by the MCP. The above is inferred from the usage documentation which describes exactly two sizes.

_Source: Oxygen MCP · Extracted 2026-05-01_
