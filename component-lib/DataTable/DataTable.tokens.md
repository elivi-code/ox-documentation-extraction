---
parent: "[[DataTable]]"
section: tokens
---

## Tokens

### Row state tokens

Theme tokens applied to table rows and cells for interactive states.

| Token | Light | Dark | Usage |
|-------|-------|------|-------|
| `active08` | `#EBEAE1` (offwhite09) | `#525252` (gray04) | Active background for table rows |
| `active10` | `#EBEAE1` (offwhite09) | `#3D3D3D` (gray03) | Background for active-state cells and rows |

### Focus tokens

Applied to interactive elements within the table (sortable header cells, row action buttons, pagination controls).

| Token | Light | Dark | Usage |
|-------|-------|------|-------|
| `focus01` | `#0056E0` (blue05) | `#D7E3F9` (blue10) | Primary focus border color |
| `focus02` | `#D7E3F9` (blue10) | `#0056E0` (blue05) | Inverted focus border color |

### Cell tokens — color

Cell-level color tokens surfaced by the Figma `table cell` component set. Light-mode values resolved via `get_design_context`; dark-mode values are unresolved.

| Element | Token | Light | Dark |
|---------|-------|-------|------|
| Cell background | `--ui/ui06` | `white` | _(unresolved — GAP-008)_ |
| Cell border bottom | `--ui/ui01` | `#ebeae1` | _(unresolved — GAP-008)_ |
| Primary text | `--text/textcolor01` | `#26252a` | _(unresolved — GAP-008)_ |
| Secondary text | `--text/textcolor02` | `#6c6862` | _(unresolved — GAP-008)_ |
| Status bar (error) | `--error/error01` | `#cb2233` | _(unresolved — GAP-008)_ |
| Fixed column divider | `--ui/ui01` | `#ebeae1` | _(unresolved — GAP-008)_ |

### Cell tokens — typography

| Element | Style token | Size | Weight | Line height | Letter spacing |
|---------|-------------|------|--------|-------------|----------------|
| Primary text | `typography/body01` | `14px` | 400 | `20px` | `-0.06px` |
| Secondary text | `typography/label01` | `12px` | 400 | `16px` | `0px` |

<!-- STUB:GAP-008 source="Re-run figma-extract after obtaining Figma Enterprise plan access, or use figma_execute to query the UI-Foundations library (file key iVY5nI8JAxM05Apnnvozzs) variables directly via the plugin console. Alternatively resolve manually by inspecting the dark-mode variant of the table cell in Figma." -->

> **Missing (GAP-008):** dark-mode values for all cell-level tokens are unresolved. The Figma Variables API returned empty results; the UI-Foundations library (`iVY5nI8JAxM05Apnnvozzs`) could not be queried.

<!-- STUB:GAP-009 source="Inspect the dataTable package source for the zebra background token reference, or query the Figma table cell component in dark/zebra mode to identify the variable binding. Depends on GAP-008." -->

> **Missing (GAP-009):** the `zebra` prop alternates row backgrounds using an internal token not exposed via the Oxygen token API. The token name is unknown.

## Notes

- No component-scoped CSS custom properties were found for `dataTable` via the Oxygen token search. The row/focus tokens above are global semantic tokens whose descriptions explicitly reference table rows/cells.
- Pagination sub-component tokens are not separately documented in the MCP for this package. The standalone `@8x8/oxygen-pagination` package may have its own token set — see [[Pagination]].
