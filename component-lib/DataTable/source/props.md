---
component: DataTable
package: "@8x8/oxygen-dataTable"
category: data_display
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - figma
  - audit
siblings:
  - "[[DataTable/examples]]"
  - "[[DataTable/tokens]]"
  - "[[DataTable/accessibility]]"
  - "[[DataTable/DataTable-figma]]"
  - "[[DataTable/DataTable-audit]]"
tags:
  - oxygen
  - component/DataTable
  - role/props
  - stage/blocked
  - category/data_display
---
# DataTable — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

Package: `dataTable` · Category: `data-display`

The DataTable is a compound component family. All sub-components are exported from the same package and are used together to compose a full data table.

---

## Installation

```
# .npmrc
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```

> **Note:** 8x8 VPN required. Use `get-project-setup` tool for complete setup instructions.

---

## `<Table>`

The root table element. Wraps `<Body>` and the column structure. Typically driven by a `useTable()` hook result.

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `children` | `ReactNode` | ✓ | — | Component content (used in composition mode) |
| `tableApi` | `Table<T>` | — | — | Table API object returned by `useTable()` hook |
| `ariaLabel` | `string` | — | — | Accessible label for the table (`aria-label`) |
| `zebra` | `boolean` | — | `false` | Alternate background color on every other row |
| `loading` | `boolean` | — | — | Shows a loading skeleton over table body |
| `loadingText` | `string` | — | — | Screen-reader text announced during loading state |
| `activeRowId` | `string` | — | — | ID of the currently active/selected row |
| `onRowClick` | `(row: Row<T>) => void` | — | — | Callback fired when a row is clicked |
| `getRowActions` | `(row: T) => ActionProps[]` | — | — | Returns per-row action items shown in a hover menu |
| `getRowStatus` | `(row: T) => RowStatusType \| undefined` | — | — | Returns a status indicator for a row (e.g. `RowStatusType.WARNING`) |
| `enableVirtualization` | `boolean` | — | — | Enables virtual scrolling for large datasets |

> **Note:** `children` and `tableApi` represent two usage modes. In practice, `tableApi` (driven by `useTable()`) is the standard approach.

---

## `<TableContainer>`

Wrapper that provides layout context for the table family. Wrap all table sub-components inside it.

No documented props. Accepts standard HTML container attributes.

---

## `<TableHeader>`

Toolbar rendered above the table. Contains action buttons, filter controls, and result count.

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `actionItems` | `ReactNode[]` | — | — | Toolbar action buttons (e.g. `<RefreshAction>`, `<DownloadAction>`) |
| `filter` | `TableHeaderProps['filter']` | — | — | Filter configuration object (see Filter shape below) |
| `listTotalResults` | `number` | — | — | Total record count to display |
| `loadingTotalResults` | `boolean` | — | — | Whether the total count is still loading |
| `loadingData` | `boolean` | — | — | Whether table data is loading |
| `totalResultsMessage` | `string` | — | — | Human-readable label for the total count (e.g. `"26 results"`) |
| `currentPage` | `number` | — | — | Current page number (for paginated tables) |
| `totalPages` | `number` | — | — | Total pages (for paginated tables) |

### Filter shape (`TableHeaderProps['filter']`)

```ts
{
  filters: FilterType[];
  numActiveFilters: number;
  filterDefinitions: FilterDefinitionType[];
  onChange: (filters: FilterType[]) => void;
  hasGlobalApplyButton?: boolean;
}
```

---

## `<HeaderCell>`

Cell component for column headers. Used inside `columnHelper.accessor` header callbacks.

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `text` | `string` | — | — | Column header label |
| `wrapText` | `boolean` | — | — | Allows the header text to wrap (up to 3 lines, then scrollable) |

---

## `<Pagination>`

Pagination controls rendered below the table. Used inside `<TableContainer>`.

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `canGoBack` | `boolean` | ✓ | — | Whether the previous-page button is enabled |
| `canGoNext` | `boolean` | ✓ | — | Whether the next-page button is enabled |
| `numberOfPages` | `number` | ✓ | — | Total page count |
| `pageNumber` | `number` | ✓ | — | Current page number (1-based) |
| `rowsPerPage` | `number` | ✓ | — | Rows shown per page |
| `onPaginationChange` | `(pagination: PaginationState) => void` | ✓ | — | Callback when page or rows-per-page changes |
| `translations` | `Translations` | ✓ | — | Localisation strings for labels/ARIA |
| `rowsPerPageOptions` | `number[]` | — | — | Options for the rows-per-page selector |
| `size` | `PaginationSize` | — | — | Visual size variant |
| `isDisabled` | `boolean` | — | — | Disables all pagination controls |
| `testId` | `string` | — | — | Test ID for automated testing |

> **Note:** In `DataTablePaginatedComponent` examples, Pagination also receives `limit`, `offset`, `totalResults`, and `loadingData` props — these are likely passed via a `usePagination()` helper hook that maps `useDataRetrieval` state to the Pagination prop shape.

---

## `<Body>`

Table body container. Renders `<BodyRow>` elements. No documented public props — managed internally by the `tableApi`.

---

## `<BodyRow>`

Individual data row inside `<Body>`. No documented public props — managed internally by the `tableApi`.

---

## `<Cell>`

Individual data cell inside `<BodyRow>`. No documented public props — cell content is provided via `columnHelper.accessor` cell callbacks.

---

## `<CheckboxCell>`

Checkbox cell for row selection. Not typically used directly — instead accessed via `cellDefinitions.getSelectColumnDef()` (multi-select) or `cellDefinitions.getSingleSelectColumnDef()` (single-select).

```tsx
// Multi-select
columnHelper.display(cellDefinitions.getSelectColumnDef())

// Single-select
columnHelper.display(cellDefinitions.getSingleSelectColumnDef())
```

No documented public props beyond what `columnHelper.display()` accepts.

---

## `<WarningIndicator>`

Visual warning indicator for a table row. Discovered in the `dataTable` MCP component list (v2.110.0). No props documented by MCP (`propsCount: 0`). Usage pattern not present in extracted examples.

---

## `<ColumnManagementModal>`

Modal for managing column visibility. Discovered in the `dataTable` MCP component list (v2.110.0). No props documented by MCP. Usage pattern not present in extracted examples.

---

## `<HeaderRow>`

Row element inside the table header area. Discovered in the `dataTable` MCP component list (v2.110.0). No props documented by MCP. Likely an internal sub-component used by `<TableHeader>` or `columnHelper`.

---

## `<HeaderCellWrapper>`

Wrapper for `<HeaderCell>`. Discovered in the `dataTable` MCP component list (v2.110.0). No props documented by MCP. Likely an internal composability primitive.

---

## `<ActionItem>`

A single action item for the table toolbar. Discovered in the `dataTable` MCP component list (v2.110.0). No props documented by MCP. See also `<RefreshAction>`, `<DownloadAction>`, `<ColumnInsertAction>` for pre-built action variants.

---

## `<ColumnInsertAction>`

Pre-built toolbar action for inserting a column. Discovered in the `dataTable` MCP component list (v2.110.0). No props documented by MCP. Used in `actionItems` on `<TableHeader>`.

---

## Related hooks

These hooks are part of the `dataTable` package and work with the components above:

| Hook | Purpose |
|------|---------|
| `useTable(options)` | Creates the `tableApi` object passed to `<Table>` |
| `useDataRetrieval(options)` | Manages async data fetching, pagination state, filters, sorting |
| `useAggregateDataRetrieval(options)` | Combines `getData` + `getTotalResults` into a single retrieval function |
| `useSorting(options)` | Manages sort state and passes `sortingOptions` / `sortingState` to `useTable` |
| `useRowSelection(options)` | Manages row selection state for multi/single select |
| `usePagination(options)` | Creates a `<Pagination>` element wired to `useDataRetrieval` state |
| `columnHelper` | TanStack Table column helper for defining column schemas |
| `cellDefinitions` | Pre-built cell definitions (select column, etc.) |

---

_Source: Oxygen MCP · Extracted 2026-05-06_
