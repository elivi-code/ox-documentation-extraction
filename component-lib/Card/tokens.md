---
component: Card
package: "@8x8/oxygen-card"
category: layout_overlay
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Card/props]]"
  - "[[Card/examples]]"
  - "[[Card/accessibility]]"
  - "[[Card/Card-figma]]"
  - "[[Card/Card-audit]]"
tags:
  - oxygen
  - component/Card
  - role/tokens
  - stage/spec_ready
  - category/layout_overlay
---
# Card — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

> ⚠️ **DEPRECATED** — `@8x8/oxygen-card` is deprecated. Token documentation preserved for reference.

## Theme Tokens

The Card component uses semantic `ui0*` tokens for borders and background surfaces. These are global theme tokens, not component-specific tokens.

### Light Mode

| Token | Value | Palette Reference | Usage |
|-------|-------|-------------------|-------|
| `ui01` | `#EBEAE1` | `colorPalette.offwhite09` | Primary border color for cards and divider lines; tertiary background color; selected state background for list items |
| `ui02` | `#F4F3EE` | `colorPalette.offwhite10` | Secondary background surface; subtle border for cards and divider lines; hover state background for list items |
| `ui03` | `#ABA999` | `colorPalette.offwhite07` | Strong color for borders on cards and divider lines |

### Dark Mode

| Token | Value | Palette Reference | Usage |
|-------|-------|-------------------|-------|
| `ui01` | `#666666` | `colorPalette.gray05` | Primary border color for cards and divider lines; tertiary background color; selected state background for list items |
| `ui02` | `#3D3D3D` | `colorPalette.gray03` | Secondary background surface; subtle border for cards and divider lines; hover state background for list items |
| `ui03` | `#858585` | `colorPalette.gray06` | Strong color for borders on cards and divider lines |

## Theme Prop

All sub-components (`Card`, `Header`, `Separator`) accept a `theme: Partial<CardTheme>` prop. `Statistics` accepts `theme: Partial<StatisticsTheme>`.

> **DOC\_GAP** — The `CardTheme` and `StatisticsTheme` interface shapes were not returned by the MCP. The specific CSS properties each theme object exposes are unknown from available sources.

---

_Source: Oxygen MCP · Extracted 2026-05-05_
