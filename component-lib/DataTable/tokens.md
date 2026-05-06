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

## Notes

- No component-scoped CSS custom properties were found for `dataTable` via the Oxygen token search. The tokens above are the global semantic tokens whose descriptions explicitly reference table rows/cells.
- The `zebra` prop on `<Table>` alternates row backgrounds using an internal token not exposed in the theme token API.
- Pagination sub-component tokens are not separately documented in the MCP for this package. The standalone `@8x8/oxygen-pagination` package may have its own token set — see [component-lib/Pagination/tokens.md](../Pagination/tokens.md).

---

_Source: Oxygen MCP · Extracted 2026-05-06_
