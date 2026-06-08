---
parent: "[[DataTable]]"
section: usage
---

## Usage

<!-- STUB:GAP-017 source="Either (a) request the design team populates the Figma '↳ Table examples' page (53919:26449) with Do/Don't usage cards and re-run figma-extract-usage, or (b) replace the editorial draft once the published Oxygen Table docs page (/components/table/usage) exits its 'In progress' state. Both paths supersede the current derivation-only draft." -->

> **Editorial derivation (GAP-017):** these Do/Don't pairs were authored on 2026-05-12 in derivation-only mode from props, examples, tokens, accessibility, and figma sources. No Figma `↳ Table examples` Do/Don't cards exist and the published Oxygen docs page is an "In progress" placeholder. Treat as provisional until an authoritative source replaces it.

DataTable is the canonical component for **dense, structured, row-oriented data** in 8x8 product surfaces — admin lists, agent rosters, call/event logs, billing records, permission matrices. It is a **compound family**: a `<TableContainer>` wraps a `<TableHeader>` toolbar above a `<Table>` body and an optional `<Pagination>` footer, all driven by hook-managed state (`useTable`, `useDataRetrieval`, `useSorting`, `useRowSelection`, `usePagination`).

## When to use vs. alternatives

Use DataTable when **rows describe entities with three or more comparable attributes** that benefit from columnar alignment, sortability, and bulk operations (selection + row actions) — when users need to scan, sort, filter, or act across many rows at once.

Prefer an alternative when:

- A single entity has many attributes for one record — use a detail layout, not a one-row table.
- Rows are visually heterogeneous (different fields per row, mixed media) — use a List or Card grid.
- The dataset is below ~5 rows with simple key/value pairs — use a definition list or stacked Card.
- Users browse media-heavy items — use a Card grid.
- The data is hierarchical with deep nesting — consider a tree view (no first-class Oxygen tree component today).

## Do and Don't

### 1. Compose the family inside `<TableContainer>`

✅ **Do** render `<TableHeader>`, `<Table>`, and the optional `<Pagination>` inside a single `<TableContainer>`, in that order.

❌ **Don't** mount a bare `<Table>` outside a container, or split the toolbar/pagination across separate layout regions.

**Why.** Every example uses the compound pattern. The container provides layout context the sub-components depend on; splitting the toolbar away breaks the visual relationship between filter state and result count, and breaks the screen-reader narrative.

### 2. Always set `ariaLabel` on `<Table>`

✅ **Do** pass a unique, human-readable `ariaLabel` to every `<Table>` (e.g. `"Active user accounts"`).

❌ **Don't** ship a `<Table>` without `ariaLabel`, and don't reuse the same label on multiple tables in one view.

**Why.** The HTML `<table>` element has no implicit accessible name; without it, multiple unlabelled tables collapse into "table"/"table"/"table" in the rotor. WCAG 2.1 4.1.2 is **Partial** because the API does not enforce the label.

### 3. Use named cell components, not ad-hoc renderers

✅ **Do** use the named cell components inside `columnHelper.accessor` callbacks: `<HeaderCell text="…">` for headers, `<TextCell primaryText={…}>` for text cells, and `cellDefinitions.getSelectColumnDef()` / `getSingleSelectColumnDef()` for selection columns.

❌ **Don't** inline raw `<div>`/`<span>` for the four mapped Figma types, and don't build a custom select column when `cellDefinitions` provides a factory.

**Why.** Named components carry the correct padding, typography (`body01` primary, `label01` secondary), focus styles, and ARIA attributes. Ad-hoc renderers lose Figma parity. For unmapped Figma `type` values (avatar, switch, tag, link, action, trend, sentiment, status), confirm the Oxygen analogue with the design system team first (see GAP-002 in [[DataTable.anatomy]]).

### 4. Always pair `loading` with `loadingText`

✅ **Do** set both `loading` and `loadingText` on `<Table>` whenever data is being fetched.

❌ **Don't** set `loading={true}` without `loadingText`, and don't replace the table with an external spinner during refetch.

**Why.** Without `loadingText`, the loading state is invisible to assistive technologies — the skeleton overlay covers the body but no announcement is made. Replacing the whole table with an external spinner makes the toolbar, filters, and pagination disappear, costing users their place.

### 5. Drive sorting through `useSorting`, not manual state

✅ **Do** manage sort state with `useSorting` and pass `sortingOptions` + `sortingState` to `useTable`. Set `enableSorting: true` per sortable column.

❌ **Don't** maintain your own `useState` for sort column/direction, and don't call `data.sort(...)` client-side before passing it to `useTable`.

**Why.** Sorting is server-side by design. `useSorting` exposes `onSortingChange` that hooks into `useDataRetrieval`, so the next fetch re-queries the API. Client-side sorting only sorts the current page. `aria-sort` on the header is wired automatically when sorting is hook-managed.

### 6. Use the `<TableHeader>` toolbar instead of an ad-hoc external one

✅ **Do** put primary actions, filters, search, and the result count inside `<TableHeader>` via `actionItems`, `filter`, and the `listTotalResults` / `totalResultsMessage` / `currentPage` / `totalPages` props.

❌ **Don't** build a parallel toolbar above `<TableContainer>` for filter chips or result counts when `<TableHeader>` already exposes those slots.

**Why.** The Figma `table action header` exposes nine slots designed to sit on a single row above the data. An external toolbar splits the relationship between filter state and the result count it produces, and forces you to re-implement loading/total coordination.

### 7. Pin the identity column, virtualize at 100+ rows

✅ **Do** set `meta.pinned: true` on the identity column (first text column — name, ID, email) so it stays visible during horizontal scroll, and enable `enableVirtualization={true}` on `<Table>` whenever the dataset can exceed ~100 rows.

❌ **Don't** allow long datasets to render without virtualization, and don't pin more than one or two columns.

**Why.** Pinning the identity column is the documented pattern; without it, horizontal scrolling loses row context. The 100+ row virtualization threshold is given verbatim in the examples. Beyond it, full-DOM tables cause sluggish scrolling on lower-end devices.

## Accessibility checklist (summary)

- `ariaLabel` set on every `<Table>` (pair 2).
- `loadingText` set whenever `loading={true}` (pair 4).
- Sortable headers wired through `useSorting` so `aria-sort` is correct (pair 5).
- Multi-select header has an `aria-label` (default via `getSelectColumnDef()`); row checkboxes carry per-row labels.
- Row status from `getRowStatus` conveyed in text/`aria-label`, not colour alone.
- `focus01` / `focus02` tokens applied to all interactive elements.
- If `onRowClick` is used, verify rows are keyboard-reachable — row navigation is **not** managed by default.

See [[DataTable.accessibility]] for the full reference.
