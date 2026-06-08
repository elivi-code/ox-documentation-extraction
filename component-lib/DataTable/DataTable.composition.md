---
parent: "[[DataTable]]"
section: composition
---

## Composition

DataTable is a compound family. The canonical structure is `<TableContainer>` → `<TableHeader>` → `<Table>` → optional `<Pagination>`, with column schemas defined via `columnHelper` and data/state supplied by hooks (`useTable`, `useDataRetrieval`, `useSorting`, `useRowSelection`).

### Imports

```tsx
import {
  // Components
  Table, TableContainer, TableHeader, HeaderCell,
  TextCell, PrimaryTextCell, SecondaryTextCell, CheckboxCell,
  Pagination,
  // Action toolbar
  RefreshAction, DownloadAction, ActionItem, ColumnInsertAction,
  // Additional confirmed exports (props undocumented in MCP v2.110.0)
  WarningIndicator, ColumnManagementModal,
  // Hooks
  useTable, useDataRetrieval, useAggregateDataRetrieval, useSorting, useRowSelection,
  // Helpers
  columnHelper, cellDefinitions,
  // Types & constants
  type TableHeaderProps, type FilterDefinitionType, type ActionProps, OPERATOR_TYPES,
} from '@8x8/oxygen-dataTable';
```

> Icons (`PencilIcon`, `LeaveIcon`, `GearIcon`) come from the Oxygen icon package. `Person`, `createPersonColumns`, `usePersonMockApi`, `useMockGetData`, and `paginationTranslations` are user-supplied test fixtures.

<!-- SKIP:GAP-006 manual="Add a createPersonColumns reference implementation in examples (or note it is a user-defined helper) so examples are self-contained. It is used in paginated, sorted, filtered, and row-actions examples but never defined." -->

> **Note (GAP-006):** `createPersonColumns()` is a user-defined helper used across the paginated, sorted, filtered, and row-actions examples but is never defined in the source. It returns an array of `columnHelper.accessor(...)` column definitions (see the Basic table `columns` array for the shape).

### Basic table

Columns defined with `columnHelper.accessor`, data fetched via `useDataRetrieval`, table API created with `useTable`.

```tsx
const columns = [
  columnHelper.accessor(row => row.firstName, {
    id: 'firstName',
    enableSorting: false,
    header: () => <HeaderCell text="First Name" />,
    cell: info => <TextCell primaryText={info.getValue()} />,
    meta: { pinned: false, type: 'large' },
  }),
  // ...lastName (meta.pinned: true, type: 'small'), age, status (wrapText header)
];

const dataRetrieval = useDataRetrieval<Person>({
  getDataAndTotalResults,
  initialDataRetrievalParams: { limit: 10, offset: 0 },
  onDataRetrievalError,
});

const tableApi = useTable({
  data: dataRetrieval.data,
  columns,
  getRowId: row => `${row.firstName}_${row.lastName}`,
});

return (
  <TableContainer>
    <TableHeader actionItems={[<RefreshAction key="refresh" title="Refresh" onClick={() => dataRetrieval.refreshData()} />]} />
    <Table loading={dataRetrieval.loadingData} loadingText="Loading data..." tableApi={tableApi} ariaLabel="User list" />
  </TableContainer>
);
```

### Paginated table

Adds `<Pagination>` below the table, wired to `useDataRetrieval` state; `<TableHeader>` receives page/total metadata.

```tsx
const currentPage = Math.floor(dataRetrieval.offset / dataRetrieval.limit) + 1;
const totalPages = Math.ceil((dataRetrieval.totalResults ?? 0) / dataRetrieval.limit);

<TableContainer>
  <TableHeader
    filter={filter}
    listTotalResults={dataRetrieval.totalResults}
    loadingTotalResults={dataRetrieval.loadingTotalResults}
    loadingData={dataRetrieval.loadingData}
    totalResultsMessage={`${dataRetrieval.totalResults} results`}
    currentPage={currentPage}
    totalPages={totalPages}
  />
  <Table loading={dataRetrieval.loadingData} tableApi={table} ariaLabel="Paginated user list" />
  <Pagination
    rowsPerPageOptions={[6, 10, 25, 40]}
    onPaginationChange={dataRetrieval.onPaginationChange}
    limit={dataRetrieval.limit}
    offset={dataRetrieval.offset}
    totalResults={dataRetrieval.totalResults}
    loadingData={dataRetrieval.loadingData}
    translations={paginationTranslations}
  />
</TableContainer>
```

> See GAP-001 in [[DataTable.props]] — the `limit`/`offset`/`totalResults`/`loadingData` props shown here conflict with the MCP-documented `<Pagination>` interface; `usePagination()` is the likely adapter.

### Sortable table (server-side)

```tsx
const sorting = useSorting({ onSortingChange: dataRetrieval.onSortingChange, sorting: dataRetrieval.sorting });
const table = useTable({
  ...sorting.sortingOptions,
  getRowId: row => `${row.firstName}_${row.lastName}`,
  data: dataRetrieval.data,
  columns: createPersonColumns({ enableSorting: true }),
  state: { ...sorting.sortingState },
});
```

### Row actions

Per-row menus via `getRowActions` returning `ActionProps[]` (each with `label`, `ariaLabel`, `onClick`, `icon`, optional `disabled`):

```tsx
const getRowActions = (row: Person): ActionProps[] => [
  { label: 'Edit', ariaLabel: `Edit ${row.firstName}`, onClick: () => {}, icon: <PencilIcon />, key: 'edit' },
  { label: 'Delete', ariaLabel: `Delete ${row.firstName}`, onClick: () => {}, icon: <LeaveIcon />, key: 'delete' },
  { label: 'View', ariaLabel: `View ${row.firstName}`, onClick: () => {}, icon: <GearIcon />,
    disabled: { isDisabled: row.age > 20, reason: 'Disabled for certain criteria' }, key: 'view' },
];

<Table tableApi={tableApi} getRowActions={getRowActions}
  onRowClick={row => setActiveRowId(activeRowId === row.id ? '' : row.id)}
  activeRowId={activeRowId} ariaLabel="User list with row actions" />
```

### Row selection (multi + single)

Multi-select uses `cellDefinitions.getSelectColumnDef()`, single-select uses `cellDefinitions.getSingleSelectColumnDef()`; both driven by `useRowSelection`.

```tsx
const columns = [
  columnHelper.display(isMultiSelect ? cellDefinitions.getSelectColumnDef() : cellDefinitions.getSingleSelectColumnDef()),
  columnHelper.accessor(row => row.firstName, {
    id: 'firstName', header: () => <HeaderCell text="First Name" />,
    cell: info => <TextCell primaryText={info.getValue()} isInactive />, meta: { pinned: true },
  }),
];
const tableApi = useTable({ ...rowSelection.rowSelectionTableOptions, data, columns, state: { ...rowSelection.rowSelectionTableState } });
```

### Filtering

`filter` prop on `<TableHeader>`, driven by `useDataRetrieval.onFiltersChange`:

```tsx
const filter: TableHeaderProps['filter'] = {
  filters: dataRetrieval.filters || [],
  numActiveFilters,
  filterDefinitions: [{ id: 'age', label: 'Age', operators: [
    { value: OPERATOR_TYPES.LESS_THAN, label: 'Less than' },
    { value: OPERATOR_TYPES.GREATER_THAN, label: 'Greater than' },
  ] }],
  onChange: dataRetrieval.onFiltersChange,
  hasGlobalApplyButton: false,
};
```

### Column resizing, pinning, width

- **Resizing:** `enableColumnResizing` + `columnResizeMode: 'onChange'` on `useTable`, then `meta.flexible: true` per column.
- **Pinning:** `meta.pinned: true` pins a column to the left.
- **Width preset:** `meta.type: 'small' | 'large'` (unset = default width).

### Virtualization

```tsx
<Table enableVirtualization={true} loading={dataRetrieval.loadingData}
  loadingText="Loading data..." tableApi={tableApi} ariaLabel="Virtualized user list" />
```

### Subcomponents & related

Renders the [[Checkbox]] (multi-select column) and [[Radio]] (single-select column) primitives, and composes the [[Pagination]] component in the footer. For empty/error states, pair with [[AlertBanner]]; for heterogeneous or short lists, prefer [[List]].
