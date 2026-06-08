---
parent: "[[DataTable]]"
section: accessibility
---

## Accessibility

### ARIA roles

| Element | Role | Notes |
|---------|------|-------|
| `<Table>` | `table` (implicit via `<table>`) | Must have an accessible name — always pass `ariaLabel` |
| `<TableHeader>` toolbar | `toolbar` (inferred) | Contains action buttons and filter controls |
| `<HeaderCell>` | `columnheader` (implicit via `<th>`) | Sortable headers gain `aria-sort="ascending"`/`"descending"` |
| `<Body>` | `rowgroup` (implicit via `<tbody>`) | — |
| `<BodyRow>` | `row` (implicit via `<tr>`) | Active row should have a visible focus indicator |
| `<Cell>` | `cell` (implicit via `<td>`) | — |
| `<CheckboxCell>` | `checkbox` (via underlying Checkbox) | Header checkbox has select-all `aria-label`; row checkboxes have per-row `aria-label` |
| `<Pagination>` | Composite navigation | Requires `translations` prop for localised button labels |

### Required: `ariaLabel` on `<Table>`

The `<table>` element has no implicit accessible name. Always provide `ariaLabel`:

```tsx
<Table tableApi={tableApi} ariaLabel="User account list" />
```

A page with multiple tables must give each a unique label.

### Keyboard interactions

| Key | Action |
|-----|--------|
| `Tab` | Moves focus between interactive elements: header action buttons, sortable column headers, row action buttons, pagination controls |
| `Enter` / `Space` | Activates focused button, sorts a column, checks/unchecks a checkbox |
| `Arrow keys` | Not natively managed — grid navigation is not implemented by default; implement custom `onKeyDown` on rows if needed |
| `Shift+Tab` | Reverse focus traversal |

When `onRowClick` is provided, clicking a row changes `activeRowId`. For keyboard access, rows must be focusable and respond to `Enter`/`Space` — verify in your implementation.

### Sorting

When `enableSorting: true` is set on a column: `<HeaderCell>` renders a sort button, `aria-sort` is applied to the `<th>` reflecting current direction, and sort state is communicated to assistive technologies automatically.

### Row selection

- **Multi-select (`getSelectColumnDef`):** checkbox in a dedicated column; header checkbox controls select-all with `aria-label`; row checkboxes have per-row `aria-label`.
- **Single-select (`getSingleSelectColumnDef`):** radio-style selector; one row at a time.
- Selected state communicated via `aria-checked`.

### Loading state

When `loading={true}`: a skeleton overlay covers the table body. `loadingText` should be provided so screen readers announce the loading state. Without it, loading state is invisible to assistive technologies.

### Row status indicator

`getRowStatus` can return `RowStatusType.WARNING` to add a visual indicator. Ensure any status conveyed visually is also communicated via text or `aria-label` on the row.

### Pagination

- `translations` must include accessible labels for Previous/Next buttons and the rows-per-page selector.
- When `isDisabled={true}`, all controls announce their disabled state.
- Page context ("Page 3 of 10") should be communicated; pass `currentPage` and `totalPages` to `<TableHeader>`.

### WCAG 2.1 AA checklist

| Criterion | Level | Status | Notes |
|-----------|-------|--------|-------|
| 1.3.1 Info and Relationships | A | ✓ | Semantic `<table>`, `<th>`, `<td>` |
| 1.4.3 Contrast (Minimum) | AA | ✓ | Oxygen token values meet contrast |
| 2.1.1 Keyboard | A | Partial | Interactive rows must be keyboard-accessible; verify `onRowClick` rows |
| 2.1.2 No Keyboard Trap | A | ✓ | Standard tab order; no traps |
| 2.4.3 Focus Order | A | ✓ | Logical order header → body → pagination |
| 2.4.7 Focus Visible | AA | ✓ | `focus01`/`focus02` tokens applied |
| 4.1.2 Name, Role, Value | A | Partial | `ariaLabel` required but not enforced; checkbox/radio cells need per-row labels |
| 4.1.3 Status Messages | AA | Partial | `loadingText` must be set for loading state to be announced |

### Virtualization and screen readers

<!-- SKIP:GAP-015 manual="Add a 'Virtualization and screen readers' section documenting whether the virtualization implementation provides aria-rowcount/aria-rowindex on the table element, and whether off-screen rows are accessible. When enableVirtualization=true, only rendered rows exist in the DOM — screen readers may not navigate to off-screen rows without additional ARIA live region or virtualizer configuration." -->

> **Undocumented (GAP-015):** when `enableVirtualization={true}`, only rendered rows exist in the DOM. Whether the implementation exposes `aria-rowcount`/`aria-rowindex` so off-screen rows remain navigable is not confirmed.

### Live regions for data updates

<!-- SKIP:GAP-016 manual="Document whether useDataRetrieval triggers any live region updates when data changes (new rows loaded, filter results changed, sort applied), and recommend wrapping totalResultsMessage in an aria-live='polite' region if not already present." -->

> **Undocumented (GAP-016):** live-region behaviour for dynamic data updates is not documented. Server-side fetched tables typically need `aria-live` announcements for result-count changes; consider wrapping `totalResultsMessage` in an `aria-live="polite"` region.

### From Figma annotations

<!-- STUB:GAP-012 source="Request the designer adds accessibility annotations to the Figma component sets (at minimum: table cell, table header, table action header) — ARIA role, focus order, keyboard interactions." -->

> **Missing (GAP-012):** no accessibility annotations exist on any Figma component set (ARIA role, focus order, keyboard interactions all absent). The reference above is sourced from the Oxygen MCP, not Figma.
