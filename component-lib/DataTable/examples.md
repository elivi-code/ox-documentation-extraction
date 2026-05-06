# DataTable — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

All examples use the compound component pattern: `<TableContainer>` → `<TableHeader>` → `<Table>` → optional `<Pagination>`.

---

## Basic table

Minimal setup: columns defined with `columnHelper.accessor`, data fetched via `useDataRetrieval`, table API created with `useTable`.

```tsx
export const DataTableBasicComponent: React.FC = () => {
  const [data] = useState(initialData);
  const { getData, getTotalResults } = useMockGetData({
    data,
    shouldSimulateLag: true,
  });
  const getDataAndTotalResults = useAggregateDataRetrieval({
    getData,
    getTotalResults,
  });

  const columns = [
    columnHelper.accessor(row => row.firstName, {
      id: 'firstName',
      enableSorting: false,
      header: () => <HeaderCell text="First Name" />,
      cell: info => <TextCell primaryText={info.getValue()} />,
      meta: { pinned: false, type: 'large' },
    }),
    columnHelper.accessor(row => row.lastName, {
      id: 'lastName',
      enableSorting: false,
      header: () => <HeaderCell text="Last Name" />,
      cell: info => <TextCell primaryText={info.getValue()} />,
      meta: { pinned: true, type: 'small' },
    }),
    columnHelper.accessor(row => row.age, {
      id: 'age',
      enableSorting: false,
      header: () => <HeaderCell text="Age" />,
      cell: info => <TextCell primaryText={info.getValue()} />,
    }),
    columnHelper.accessor(row => row.status, {
      id: 'Status',
      enableSorting: false,
      header: () => (
        <HeaderCell
          text="Status (long text to demonstrate header text wrap)"
          wrapText
        />
      ),
      cell: info => <TextCell primaryText={info.getValue()} />,
    }),
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

  const actionItems = [
    <RefreshAction
      key="refresh"
      title="Refresh"
      onClick={() => dataRetrieval.refreshData()}
    />,
  ];

  return (
    <Page>
      <TableContainer>
        <TableHeader actionItems={actionItems} />
        <Table
          loading={dataRetrieval.loadingData}
          loadingText="Loading data..."
          tableApi={tableApi}
          ariaLabel="User list"
        />
      </TableContainer>
    </Page>
  );
};
```

---

## Paginated table

Adds `<Pagination>` below the table and wires it to `useDataRetrieval` state. `<TableHeader>` also receives page/total metadata.

```tsx
export const DataTablePaginatedComponent: React.FC = () => {
  const { getData, getTotalResults } = usePersonMockApi({
    numData: 26,
    shouldSimulateLag: true,
  });
  const getDataAndTotalResults = useAggregateDataRetrieval({ getData, getTotalResults });
  const columns = createPersonColumns();

  const dataRetrieval = useDataRetrieval<Person>({
    initialDataRetrievalParams: { limit: 6, offset: 0, filters: [] },
    getDataAndTotalResults,
    onDataRetrievalError,
  });

  const numActiveFilters = useMemo(
    () => getActiveFiltersNumber(dataRetrieval.filters || []),
    [dataRetrieval.filters],
  );

  const filterDefinitions = useMemo(
    (): FilterDefinitionType[] => [
      {
        id: 'age',
        label: 'Age',
        operators: [
          { value: OPERATOR_TYPES.LESS_THAN, label: 'Less than' },
          { value: OPERATOR_TYPES.GREATER_THAN, label: 'Greater than' },
        ],
      },
    ],
    [],
  );

  const filter: TableHeaderProps['filter'] = {
    filters: dataRetrieval.filters || [],
    numActiveFilters,
    filterDefinitions,
    onChange: dataRetrieval.onFiltersChange,
  };

  const table = useTable({
    getRowId: row => `${row.firstName}_${row.lastName}`,
    data: dataRetrieval.data,
    columns,
  });

  const currentPage = Math.floor(dataRetrieval.offset / dataRetrieval.limit) + 1;
  const totalPages = Math.ceil((dataRetrieval.totalResults ?? 0) / dataRetrieval.limit);

  return (
    <Page>
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
        <Table
          loading={dataRetrieval.loadingData}
          tableApi={table}
          ariaLabel="Paginated user list"
        />
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
    </Page>
  );
};
```

---

## Sortable table

Server-side sorting via `useSorting`. Pass `sortingOptions` and `sortingState` to `useTable`, and `onSortingChange` / `sorting` to `useSorting`.

```tsx
export const DataTableSortedComponent: React.FC = () => {
  const mockApi = usePersonMockApi({ numData: 5 });
  const getDataAndTotalResults = useAggregateDataRetrieval({ ...mockApi });
  const columns = createPersonColumns({ enableSorting: true });

  const dataRetrieval = useDataRetrieval<Person>({
    initialDataRetrievalParams: { limit: 10, offset: 0 },
    getDataAndTotalResults,
    onDataRetrievalError,
  });

  const sorting = useSorting({
    onSortingChange: dataRetrieval.onSortingChange,
    sorting: dataRetrieval.sorting,
  });

  const table = useTable({
    ...sorting.sortingOptions,
    getRowId: row => `${row.firstName}_${row.lastName}`,
    data: dataRetrieval.data,
    columns,
    state: { ...sorting.sortingState },
  });

  return (
    <Page>
      <TableContainer>
        <Table tableApi={table} ariaLabel="Sortable user list" />
      </TableContainer>
    </Page>
  );
};
```

---

## Table with row actions

Per-row action menus via `getRowActions`. Each action defines `label`, `ariaLabel`, `onClick`, `icon`, and optionally `disabled`.

```tsx
export const DataTableRowActionsComponent: React.FC = () => {
  const [data] = useState(initialData);
  const mockApi = useMockGetData({ data, shouldSimulateLag: true });
  const getDataAndTotalResults = useAggregateDataRetrieval({ ...mockApi });
  const columns = createPersonColumns();

  const dataRetrieval = useDataRetrieval<Person>({
    initialDataRetrievalParams: { limit: 6, offset: 0 },
    getDataAndTotalResults,
    onDataRetrievalError,
  });

  const tableApi = useTable({
    data: dataRetrieval.data,
    columns,
    getRowId: row => `${row.firstName}_${row.lastName}`,
  });

  const getRowActions = (row: Person): ActionProps[] => [
    {
      label: 'Edit',
      ariaLabel: `Edit ${row.firstName} ${row.lastName}`,
      onClick: () => {},
      icon: <PencilIcon />,
      key: 'edit',
      testId: 'edit-action',
    },
    {
      label: 'Delete',
      ariaLabel: `Delete user ${row.firstName}`,
      onClick: () => {},
      icon: <LeaveIcon />,
      key: 'delete',
      testId: 'delete-action',
    },
    {
      label: 'View',
      ariaLabel: `View details for ${row.firstName} ${row.lastName}`,
      onClick: () => {},
      icon: <GearIcon />,
      disabled: { isDisabled: row.age > 20, reason: 'Disabled for certain criteria' },
      key: 'view',
      testId: 'view-action',
    },
  ];

  const [activeRowId, setActiveRowId] = useState('');

  return (
    <Page>
      <TableContainer>
        <TableHeader actionItems={[<RefreshAction key="refresh" title="Refresh" onClick={() => dataRetrieval.refreshData()} />]} />
        <Table
          loading={dataRetrieval.loadingData}
          loadingText="Loading data..."
          tableApi={tableApi}
          getRowActions={getRowActions}
          onRowClick={row => setActiveRowId(activeRowId === row.id ? '' : row.id)}
          activeRowId={activeRowId}
          ariaLabel="User list with row actions"
        />
      </TableContainer>
    </Page>
  );
};
```

---

## Row selection (multi + single)

Multi-select uses `cellDefinitions.getSelectColumnDef()`, single-select uses `cellDefinitions.getSingleSelectColumnDef()`. Both are driven by `useRowSelection`.

```tsx
export const DataTableSelectRowsComponent: React.FC<{ rowSelectionType: 'multi' | 'single' }> = ({
  rowSelectionType,
}) => {
  const [data] = useState(initialData);
  const mockApi = useMockGetData({ data, shouldSimulateLag: true });
  const getDataAndTotalResults = useAggregateDataRetrieval({ ...mockApi });
  const isMultiSelect = rowSelectionType === 'multi';

  const columns = [
    columnHelper.display(
      isMultiSelect
        ? cellDefinitions.getSelectColumnDef()
        : cellDefinitions.getSingleSelectColumnDef(),
    ),
    columnHelper.accessor(row => row.firstName, {
      id: 'firstName',
      enableSorting: false,
      header: () => <HeaderCell text="First Name" />,
      cell: info => <TextCell primaryText={info.getValue()} isInactive />,
      meta: { pinned: true },
    }),
    // ... more columns
  ];

  const rowSelection = useRowSelection({ initialRowSelection: {} });

  const dataRetrieval = useDataRetrieval<Person>({
    initialDataRetrievalParams: { limit: 10, offset: 0 },
    getDataAndTotalResults,
    onDataRetrievalError,
  });

  const tableApi = useTable({
    ...rowSelection.rowSelectionTableOptions,
    data: dataRetrieval.data,
    columns,
    getRowId: row => `${row.firstName}_${row.lastName}`,
    state: { ...rowSelection.rowSelectionTableState },
  });

  return (
    <Page>
      <TableContainer>
        <TableHeader actionItems={[<RefreshAction key="refresh" title="Refresh" onClick={() => dataRetrieval.refreshData()} />]} />
        <Table
          loading={dataRetrieval.loadingData}
          tableApi={tableApi}
          ariaLabel="Selectable user list"
        />
      </TableContainer>
    </Page>
  );
};
```

---

## Filtered table

Filter state managed by `useDataRetrieval`. Pass `filter` prop to `<TableHeader>` with `filterDefinitions`, current `filters`, active count, and `onChange` handler.

```tsx
const filter: TableHeaderProps['filter'] = {
  filters: dataRetrieval.filters || [],
  numActiveFilters,
  filterDefinitions: [
    {
      id: 'age',
      label: 'Age',
      operators: [
        { value: OPERATOR_TYPES.LESS_THAN, label: 'Less than' },
        { value: OPERATOR_TYPES.GREATER_THAN, label: 'Greater than' },
      ],
    },
  ],
  onChange: dataRetrieval.onFiltersChange,
  hasGlobalApplyButton: false,
};

// Pass to TableHeader:
<TableHeader
  actionItems={actionItems}
  filter={filter}
  listTotalResults={dataRetrieval.totalResults}
  loadingTotalResults={dataRetrieval.loadingTotalResults}
  totalResultsMessage={`${dataRetrieval.totalResults} Total filtered results`}
/>
```

---

## Column resizing

Enable via `enableColumnResizing` on `useTable` with `columnResizeMode: 'onChange'`. Mark individual columns as resizable with `meta.flexible: true`.

```tsx
const tableApi = useTable({
  data: dataRetrieval.data,
  columns,
  getRowId: row => `${row.firstName}_${row.lastName}`,
  columnResizeMode: 'onChange',
  enableColumnResizing: true,
});

// Column definition with flexible sizing:
columnHelper.accessor(row => row.firstName, {
  id: 'firstName',
  header: () => <HeaderCell text="First Name" />,
  cell: info => <TextCell primaryText={info.getValue()} />,
  meta: {
    type: 'large',
    flexible: true, // enables resize handle
  },
})
```

---

## Sticky / pinned columns

Set `meta.pinned: true` on column definitions to pin them to the left. Wrap in `<ReducedWidth>` styled component to demonstrate horizontal scrolling.

```tsx
columnHelper.accessor(row => row.lastName, {
  id: 'lastName',
  header: () => <HeaderCell text="Last Name" />,
  cell: info => <TextCell primaryText={info.getValue()} />,
  meta: { pinned: true }, // this column stays fixed while others scroll
})
```

---

## Virtualized table

Enable virtual scrolling for large datasets (100+ rows) via `enableVirtualization` on `<Table>`.

```tsx
<Table
  enableVirtualization={true}
  loading={dataRetrieval.loadingData}
  loadingText="Loading data..."
  tableApi={tableApi}
  ariaLabel="Virtualized user list"
/>
```

---

## Column meta types

`meta.type` controls the default column width:

| Value | Width |
|-------|-------|
| `'small'` | Narrow column |
| `'large'` | Wide column |
| _(unset)_ | Default width |

`meta.flexible: true` makes the column user-resizable (requires `enableColumnResizing` on `useTable`).

---

_Source: Oxygen MCP · Extracted 2026-05-06_
