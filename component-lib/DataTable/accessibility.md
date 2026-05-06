# DataTable — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md)

---

## ARIA roles

| Element | Role | Notes |
|---------|------|-------|
| `<Table>` | `table` (implicit via `<table>`) | Must have an accessible name — always pass `ariaLabel` |
| `<TableHeader>` toolbar | `toolbar` (inferred) | Contains action buttons and filter controls |
| `<HeaderCell>` | `columnheader` (implicit via `<th>`) | Sortable headers gain `aria-sort="ascending"` or `"descending"` |
| `<Body>` | `rowgroup` (implicit via `<tbody>`) | — |
| `<BodyRow>` | `row` (implicit via `<tr>`) | Active row should have a visible focus indicator |
| `<Cell>` | `cell` (implicit via `<td>`) | — |
| `<CheckboxCell>` | `checkbox` (via underlying Checkbox) | Header checkbox has `aria-label` for select-all; row checkboxes have `aria-label` for individual rows |
| `<Pagination>` | Composite navigation | Requires `translations` prop for localised button labels |

---

## Required: `ariaLabel` on `<Table>`

The `<table>` element has no implicit accessible name. Always provide `ariaLabel`:

```tsx
<Table tableApi={tableApi} ariaLabel="User account list" />
```

A page with multiple tables must give each a unique label so screen reader users can distinguish between them.

---

## Keyboard interactions

| Key | Action |
|-----|--------|
| `Tab` | Moves focus between interactive elements: header action buttons, sortable column headers, row action buttons, pagination controls |
| `Enter` / `Space` | Activates focused button, sorts a column, checks/unchecks a checkbox |
| `Arrow keys` | Not natively managed — grid navigation is not implemented by default; if needed, implement custom `onKeyDown` on rows |
| `Shift+Tab` | Reverse focus traversal |

### Row click / activation

When `onRowClick` is provided, clicking a row changes `activeRowId`. For keyboard access, rows need to be focusable and respond to `Enter`/`Space`. Verify with your implementation that active rows are reachable by keyboard.

---

## Sorting

When `enableSorting: true` is set on a column:

- The `<HeaderCell>` renders a sort button.
- `aria-sort` is applied to the `<th>` reflecting current sort direction.
- Sort state is communicated to assistive technologies automatically via the underlying `<th aria-sort>` attribute.

---

## Row selection

- **Multi-select (`getSelectColumnDef`):** Renders a checkbox in a dedicated column. The header checkbox controls select-all and has `aria-label`. Row checkboxes have per-row `aria-label` values.
- **Single-select (`getSingleSelectColumnDef`):** Renders a radio-style selector. Only one row is selectable at a time.
- Selected state is communicated via `aria-checked` on checkboxes.

---

## Loading state

When `loading={true}`:

- A skeleton overlay covers the table body.
- `loadingText` should be provided so screen readers announce the loading state (e.g. `loadingText="Loading data..."`).
- Without `loadingText`, loading state is invisible to assistive technologies.

---

## Row status indicator

`getRowStatus` can return `RowStatusType.WARNING` to add a visual indicator to a row. Ensure any status conveyed visually is also communicated to screen readers via text or `aria-label` on the row.

---

## Pagination

- The `translations` prop on `<Pagination>` must include accessible labels for Previous/Next buttons and the rows-per-page selector.
- When `isDisabled={true}`, all pagination controls are disabled and announce their disabled state to assistive technologies.
- Page context ("Page 3 of 10") should be communicated; pass `currentPage` and `totalPages` to `<TableHeader>` for display.

---

## WCAG 2.1 AA checklist

| Criterion | Level | Status | Notes |
|-----------|-------|--------|-------|
| 1.3.1 Info and Relationships | A | ✓ | Semantic `<table>`, `<th>`, `<td>` elements |
| 1.4.3 Contrast (Minimum) | AA | ✓ | Oxygen token values meet contrast requirements |
| 2.1.1 Keyboard | A | Partial | Interactive rows must be keyboard-accessible; verify `onRowClick` rows |
| 2.1.2 No Keyboard Trap | A | ✓ | Standard tab order; no traps in table |
| 2.4.3 Focus Order | A | ✓ | Logical tab order through header → body → pagination |
| 2.4.7 Focus Visible | AA | ✓ | `focus01` / `focus02` tokens applied to interactive elements |
| 4.1.2 Name, Role, Value | A | Partial | `ariaLabel` on `<Table>` is required but not enforced; checkbox/radio cells must have per-row labels |
| 4.1.3 Status Messages | AA | Partial | `loadingText` must be set for loading state to be announced |

---

_Source: Oxygen MCP · Extracted 2026-05-06_
