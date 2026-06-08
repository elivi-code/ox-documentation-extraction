---
parent: "[[DataTable]]"
section: props
---

## Props

DataTable is a compound component family. All sub-components are exported from the `dataTable` package and composed together. Props are documented per sub-component below.

### `<Table>`

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

<!-- SKIP:GAP-004 manual="Table props beyond children/zebra (loading, tableApi, ariaLabel, onRowClick, getRowActions, getRowStatus, enableVirtualization, activeRowId, loadingText) are inferred from Storybook examples, not returned by the MCP (which returned only 2 props). Consumers should check @8x8/oxygen-dataTable TypeScript types for the complete interface, including generics Table<T>/Row<T>." -->

### `<TableContainer>`

Wrapper that provides layout context for the table family. Wrap all table sub-components inside it. No documented props; accepts standard HTML container attributes.

### `<TableHeader>`

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

#### Filter shape (`TableHeaderProps['filter']`)

```ts
{
  filters: FilterType[];
  numActiveFilters: number;
  filterDefinitions: FilterDefinitionType[];
  onChange: (filters: FilterType[]) => void;
  hasGlobalApplyButton?: boolean;
}
```

### `<HeaderCell>`

Cell component for column headers. Used inside `columnHelper.accessor` header callbacks.

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `text` | `string` | — | — | Column header label |
| `wrapText` | `boolean` | — | — | Allows the header text to wrap (up to 3 lines, then scrollable) |

### `<Pagination>`

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

<!-- CONFLICT:GAP-001 finding="MCP-returned Pagination props (canGoBack, canGoNext, numberOfPages, pageNumber, rowsPerPage) are mutually exclusive with example-observed props (limit, offset, totalResults, loadingData). props.md documents both sets simultaneously without resolving which is the public API." HUMAN DECISION REQUIRED -->

> **Unresolved (GAP-001):** In `DataTablePaginatedComponent` examples, `<Pagination>` also receives `limit`, `offset`, `totalResults`, and `loadingData` — likely mapped from `useDataRetrieval` state via a `usePagination()` helper. The canonical public interface (table above vs. these example-observed props) has not been confirmed.

### `<Body>` / `<BodyRow>` / `<Cell>`

Body container, individual data row, and individual data cell respectively. No documented public props — managed internally by the `tableApi`. Cell content is provided via `columnHelper.accessor` cell callbacks.

### `<CheckboxCell>`

Checkbox cell for row selection. Not typically used directly — instead accessed via `cellDefinitions.getSelectColumnDef()` (multi-select) or `cellDefinitions.getSingleSelectColumnDef()` (single-select).

```tsx
// Multi-select
columnHelper.display(cellDefinitions.getSelectColumnDef())
// Single-select
columnHelper.display(cellDefinitions.getSingleSelectColumnDef())
```

No documented public props beyond what `columnHelper.display()` accepts.

<!-- STUB:GAP-003 source="All 20 components in the dataTable MCP package return propsCount: 0 (v2.110.0). Named-cell props cannot be resolved from MCP. Obtain from @8x8/oxygen-dataTable TypeScript types in the package source, or from Storybook stories for TextCell/PrimaryTextCell/SecondaryTextCell. Depends on GAP-002 resolution for unmapped cell types." -->

### Named cell components

`TextCell`, `PrimaryTextCell`, and `SecondaryTextCell` are confirmed exports of `@8x8/oxygen-dataTable` (MCP v2.110.0). All appear inside `columnHelper.accessor` cell callbacks. Example-observed props: `primaryText` (all three), `isInactive` (TextCell). Full prop tables cannot be retrieved from the MCP — `propsCount: 0` for every component in this package. Source the complete interface from the package TypeScript types.

### `<WarningIndicator>`

Confirmed export of `@8x8/oxygen-dataTable` (MCP v2.110.0). Visual warning indicator for a table row. No props documented by MCP. Usage pattern not present in extracted examples — likely consumed internally or via `getRowStatus`.

### `<ColumnManagementModal>`

Confirmed export of `@8x8/oxygen-dataTable` (MCP v2.110.0). Modal for managing column visibility. No props documented by MCP. Usage pattern not present in extracted examples.

### `<HeaderRow>` / `<HeaderCellWrapper>`

Confirmed exports of `@8x8/oxygen-dataTable` (MCP v2.110.0). Internal composability primitives used by the column-header rendering pipeline. No public props documented; not intended for direct use.

### `<ActionItem>` / `<ColumnInsertAction>`

Confirmed exports of `@8x8/oxygen-dataTable` (MCP v2.110.0). Used in `actionItems` on `<TableHeader>` alongside `<RefreshAction>` and `<DownloadAction>`. `<ColumnInsertAction>` is a pre-built action for inserting a column. No props documented by MCP.

## Related hooks

| Hook | Purpose |
|------|---------|
| `useTable(options)` | Creates the `tableApi` object passed to `<Table>` |
| `useDataRetrieval(options)` | Manages async data fetching, pagination state, filters, sorting |
| `useAggregateDataRetrieval(options)` | Combines `getData` + `getTotalResults` into a single retrieval function |
| `useSorting(options)` | Manages sort state; passes `sortingOptions` / `sortingState` to `useTable` |
| `useRowSelection(options)` | Manages row selection state for multi/single select |
| `usePagination(options)` | Creates a `<Pagination>` element wired to `useDataRetrieval` state |
| `columnHelper` | TanStack Table column helper for defining column schemas |
| `cellDefinitions` | Pre-built cell definitions (select column, etc.) |
