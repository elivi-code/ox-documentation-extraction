---
component: DataTable
status: draft
package: "@8x8/oxygen-dataTable"
category: data_display
figma: "https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=2433:0"
variants: [Basic, Paginated, Sortable, Filtered, "Multi-select", "Single-select", "Row actions", Virtualized]
props:
  - children: ReactNode
  - tableApi: "Table<T>"
  - ariaLabel: string
  - zebra: boolean
  - loading: boolean
  - loadingText: string
  - activeRowId: string
  - onRowClick: function
  - getRowActions: function
  - getRowStatus: function
  - enableVirtualization: boolean
subcomponents: ["[[TableContainer]]", "[[TableHeader]]", "[[HeaderCell]]", "[[Table]]", "[[Cell]]", "[[TextCell]]", "[[PrimaryTextCell]]", "[[SecondaryTextCell]]", "[[CheckboxCell]]", "[[Pagination]]", "[[WarningIndicator]]", "[[ColumnManagementModal]]"]
related: ["[[Checkbox]]", "[[Radio]]", "[[AlertBanner]]", "[[List]]"]
patterns: []
tokens: ["[[token.active08]]", "[[token.active10]]", "[[token.focus01]]", "[[token.focus02]]", "[[token.ui06]]", "[[token.ui01]]", "[[token.textcolor01]]", "[[token.textcolor02]]", "[[token.error01]]", "[[token.typography.body01]]", "[[token.typography.label01]]"]
spokes:
  - "[[DataTable.props]]"
  - "[[DataTable.anatomy]]"
  - "[[DataTable.tokens]]"
  - "[[DataTable.usage]]"
  - "[[DataTable.accessibility]]"
  - "[[DataTable.platform]]"
  - "[[DataTable.composition]]"
tags: [component, data_display, table, draft]
---

## Overview

DataTable is the canonical component for dense, structured, row-oriented data — admin lists, rosters, logs, billing records. It is a **compound family**, not a single component: `<TableContainer>` wraps a `<TableHeader>` toolbar above a `<Table>` body and an optional `<Pagination>` footer, all driven by hook-managed state (`useTable`, `useDataRetrieval`, `useSorting`, `useRowSelection`, `usePagination`). The `variants` listed are composition configurations from the examples, not a single `variant` prop.

> **Status: draft.** Two CONFLICTs remain unresolved — GAP-001 (Pagination public API) in [[DataTable.props]] and GAP-002 (Figma `type` ↔ cell component mapping) in [[DataTable.anatomy]] — plus major SOURCE_GAPs on dark-mode tokens and Figma annotations. See [DataTable-audit.md](DataTable-audit.md).

## Spokes

- [[DataTable.props]] — 20 MCP-confirmed exports; Table (11 props), TableHeader, HeaderCell, Pagination documented; CONFLICT GAP-001 on Pagination interface; named-cell props SOURCE_GAP (propsCount:0 across all components in MCP v2.110.0)
- [[DataTable.anatomy]] — 10 Figma component sets; `table cell` with an 18-value `type` axis; 5 interaction states; CONFLICT GAP-002 on type↔component mapping
- [[DataTable.tokens]] — row-state, focus, and cell color/typography tokens; dark-mode values unresolved (GAP-008), zebra token unknown (GAP-009)
- [[DataTable.usage]] — 7 Do/Don't pairs covering composition, ariaLabel, named cells, loading, sorting, toolbar, pinning/virtualization (editorial derivation, GAP-017)
- [[DataTable.accessibility]] — keyboard, ARIA roles, WCAG 2.1 AA checklist, selection/loading; Figma a11y annotations missing (GAP-012)
- [[DataTable.platform]] — no PUI file; relevance unconfirmed (GAP-018)
- [[DataTable.composition]] — compound patterns: basic, paginated, sortable, row actions, selection, filtering, resizing, pinning, virtualization
