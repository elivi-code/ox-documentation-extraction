---
parent: "[[Card]]"
section: tokens
---

# Card — Tokens

> ⚠️ **DEPRECATED** — `@8x8/oxygen-card` is deprecated. Token documentation preserved for reference.

The Card component uses semantic `ui0*` global theme tokens for borders and background surfaces. These are global tokens, not component-specific.

## Theme tokens

### Light Mode

| Token | Value | Palette Reference | Usage |
|-------|-------|-------------------|-------|
| `ui01` | `#EBEAE1` | `colorPalette.offwhite09` | Primary border color for cards and divider lines; tertiary background; selected-state background for list items |
| `ui02` | `#F4F3EE` | `colorPalette.offwhite10` | Secondary background surface; subtle border for cards and divider lines; hover-state background for list items |
| `ui03` | `#ABA999` | `colorPalette.offwhite07` | Strong color for borders on cards and divider lines |

### Dark Mode

| Token | Value | Palette Reference | Usage |
|-------|-------|-------------------|-------|
| `ui01` | `#666666` | `colorPalette.gray05` | Primary border color for cards and divider lines; tertiary background; selected-state background for list items |
| `ui02` | `#3D3D3D` | `colorPalette.gray03` | Secondary background surface; subtle border for cards and divider lines; hover-state background for list items |
| `ui03` | `#858585` | `colorPalette.gray06` | Strong color for borders on cards and divider lines |

## Color & token bindings (from Figma)

### Card container — Light mode

| State | Property | Variable ID | Resolved value | Probable token |
|-------|----------|-------------|---------------|----------------|
| Rest | Fill (background) | `20136:267` | `#FFFFFF` | Unknown — not matched in `ui01/02/03` |
| Hover | Fill (background) | `20136:263` | `#F4F3EE` | `ui02` (value match) |
| Focus | Fill (background) | `20136:267` | `#FFFFFF` | Unknown — same as Rest |
| Rest | Stroke (border) | `20136:253` | `#EBEAE1` | `ui01` (value match) |
| Hover | Stroke (border) | `20136:253` | `#EBEAE1` | `ui01` (value match) |
| Focus | Stroke (border) | `20136:253` | `#EBEAE1` | `ui01` (value match) |

### Card container — Dark mode

| State | Property | Variable ID | Resolved value | Probable token |
|-------|----------|-------------|---------------|----------------|
| Rest | Fill (background) | `20136:267` | `#171719` | Unknown — not matched in `ui01/02/03` |
| Rest | Stroke (border) | `20136:253` | `#666666` | `ui01` dark (value match) |

<!-- STUB:GAP-005 source="Resolve variable ID 20136:267 to its semantic name via the Figma Desktop Bridge (figma_execute + figma.variables.getVariableByIdAsync) or the Variables REST API. Add the token here." -->
> **SOURCE_GAP (GAP-005)** — The Rest/Focus background fill (variable `20136:267` = `#FFFFFF` Light / `#171719` Dark) matches none of the three `ui0x` tokens (ui01=#EBEAE1, ui02=#F4F3EE, ui03=#ABA999). The semantic token name for the card's default surface is unknown.

<!-- STUB:GAP-006 source="Run figma_execute with figma.variables.getVariableByIdAsync for IDs 20136:253, 20136:263, 20136:267 in the Figma Desktop Bridge to obtain confirmed semantic token names. Update Card-figma and tokens." -->
> **SOURCE_GAP (GAP-006)** — All three token variable IDs (`20136:253`, `20136:263`, `20136:267`) are opaque. The Variables REST API returned 403 (Enterprise plan required). Probable token names are inferred from hex matches only — not authoritative. Resolve via Desktop Bridge.

<!-- STUB:GAP-008 source="Call figma_get_component for nodes 18080:30021 (Dark/Hover) and 18080:30158 (Dark/Focus) to capture their fill token IDs. Update the Dark mode table." -->
> **SOURCE_GAP (GAP-008)** — Dark mode Hover and Focus fill tokens were not fetched. Only Dark/Rest was captured (`#171719` fill, `#666666` border).

## Typography tokens

<!-- STUB:GAP-009 source="Inspect text node 18080:28139 via figma_execute to retrieve its textStyleId or boundVariables for font properties. Update this section." -->
> **SOURCE_GAP (GAP-009)** — The `Widget Name` text node (`18080:28139`) inside the Header returned no `boundVariables` for typography. Text style name, font size, weight, and line height are unavailable.

## Theme prop

All sub-components accept a `theme` override (`Partial<CardTheme>`, or `Partial<StatisticsTheme>` for `Card.Statistics`). The interface shapes are undocumented — see **GAP-004** in [[Card.props]].
