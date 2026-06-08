---
component: DataTable
package: "@8x8/oxygen-dataTable"
category: data_display
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[DataTable/props]]"
  - "[[DataTable/examples]]"
  - "[[DataTable/accessibility]]"
  - "[[DataTable/DataTable-figma]]"
  - "[[DataTable/DataTable-audit]]"
tags:
  - oxygen
  - component/DataTable
  - role/tokens
  - stage/blocked
  - category/data_display
---
# DataTable — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

---

## Row state tokens

These theme tokens are applied to table rows and cells for interactive states.

### Light mode

| Token | Value | Reference | Usage |
|-------|-------|-----------|-------|
| `active08` | `#EBEAE1` | `colorPalette.offwhite09` | Active background for table rows and dialpad numbers |
| `active10` | `#EBEAE1` | `colorPalette.offwhite09` | Background for active state table cells and rows |

### Dark mode

| Token | Value | Reference | Usage |
|-------|-------|-----------|-------|
| `active08` | `#525252` | `colorPalette.gray04` | Active background for table rows and dialpad numbers |
| `active10` | `#3D3D3D` | `colorPalette.gray03` | Background for active state table cells and rows |

---

## Focus tokens

Applied to interactive elements within the table (e.g. sortable header cells, row action buttons, pagination controls).

### Light mode

| Token | Value | Reference | Usage |
|-------|-------|-----------|-------|
| `focus01` | `#0056E0` | `colorPalette.blue05` | Primary focus border color for interactive elements |
| `focus02` | `#D7E3F9` | `colorPalette.blue10` | Inverted focus border color |

### Dark mode

| Token | Value | Reference | Usage |
|-------|-------|-----------|-------|
| `focus01` | `#D7E3F9` | `colorPalette.blue10` | Primary focus border color for interactive elements |
| `focus02` | `#0056E0` | `colorPalette.blue05` | Inverted focus border color |

---

## Cell tokens

Cell-level color and typography tokens surfaced by the Figma `table cell` component set (see [DataTable-figma.md](DataTable-figma.md) → *Color & token bindings*). Light-mode values were resolved via `get_design_context`; dark-mode values could not be extracted (the Variables API returned no results for this file — the tokens live in the UI-Foundations library).

### Color (cell)

| Element | Token | Light value | Dark value |
|---------|-------|-------------|------------|
| Cell background | `--ui/ui06` | `white` | _(unresolved — see GAP-008)_ |
| Cell border bottom | `--ui/ui01` | `#ebeae1` | _(unresolved — see GAP-008)_ |
| Primary text | `--text/textcolor01` | `#26252a` | _(unresolved — see GAP-008)_ |
| Secondary text | `--text/textcolor02` | `#6c6862` | _(unresolved — see GAP-008)_ |
| Status bar (error) | `--error/error01` | `#cb2233` | _(unresolved — see GAP-008)_ |
| Fixed column divider | `--ui/ui01` | `#ebeae1` | _(unresolved — see GAP-008)_ |

### Typography (cell)

| Element | Style token | Size | Weight | Line height | Letter spacing |
|---------|-------------|------|--------|-------------|----------------|
| Primary text | `typography/body01` | `14px` | 400 | `20px` | `-0.06px` |
| Secondary text | `typography/label01` | `12px` | 400 | `16px` | `0px` |

---

## Notes

- No component-scoped CSS custom properties were found for `dataTable` via the Oxygen token search. The tokens above are the global semantic tokens whose descriptions explicitly reference table rows/cells.
- The `zebra` prop on `<Table>` alternates row backgrounds using an internal token not exposed in the theme token API.
- Pagination sub-component tokens are not separately documented in the MCP for this package. The standalone `@8x8/oxygen-pagination` package may have its own token set — see [component-lib/Pagination/tokens.md](../Pagination/tokens.md).

---

_Source: Oxygen MCP · Extracted 2026-05-06_
