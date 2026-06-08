---
component: DataTable
package: "@8x8/oxygen-dataTable"
published_package_name: "@8x8/oxygen-table"
category: data_display
role: usage
role_description: "Usage guidelines — Do/Don't editorial guidance, derived from extracted MCP/Figma artifacts (no Figma Do/Don't cards and no published docs page)"
pipeline_stage: editorial
pipeline_note: "Authored editorially on 2026-05-12. The Figma `↳ DataTable examples` page contains no Do/Don't card frames, so `figma-extract-usage` cannot run. The published Oxygen docs page at https://oxygen.8x8.com/components/table/usage is an 'In progress' placeholder (fetched 2026-05-12 via Claude_in_Chrome MCP, last updated 4/10/2026 on the docs site). Do/Don't pairs are derived from props.md, examples.md, tokens.md, accessibility.md, and DataTable-figma.md. Re-run /doc-audit DataTable after creation. Replace pairs with figma-extract-usage output if a Figma examples page is ever populated, or transcribe verbatim once the published Table docs page is published."
source_type: editorial
audit_verdict: null
siblings:
  - "[[DataTable/props]]"
  - "[[DataTable/examples]]"
  - "[[DataTable/tokens]]"
  - "[[DataTable/accessibility]]"
  - "[[DataTable/DataTable-figma]]"
  - "[[DataTable/DataTable-audit]]"
tags:
  - oxygen
  - component/DataTable
  - role/usage
  - stage/editorial
  - category/data_display
---
<!-- SOURCE: editorial — derived from extracted MCP/Figma artifacts. Published Oxygen docs page (/components/table/usage) is an "In progress" placeholder; no Figma "↳ DataTable examples" page with Do/Don't cards exists. -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run -->
<!-- PUBLISHED DOCS PAGE: in-progress placeholder — fetched 2026-05-12 via Claude_in_Chrome MCP -->
<!-- GROUNDING: full — props.md, examples.md, tokens.md, accessibility.md, DataTable-figma.md, DataTable-audit.md -->
<!-- DRAFTED: 2026-05-12 -->
<!-- MODE: derivation-only -->
<!-- PAIRS: 7 (derived from extracted artifacts cross-validated against the compound-component pattern in examples.md and the anatomy in DataTable-figma.md) -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output if/when a Figma "↳ DataTable examples" page is created with Do/Don't cards, or transcribe verbatim once the published Table docs page goes live. -->

# DataTable — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [DataTable-figma.md](./DataTable-figma.md)

> **Editorial guidance — derived from extracted artifacts.** Neither a Figma `↳ DataTable examples` page with Do/Don't cards nor a published Oxygen docs page exists today. The published page at `https://oxygen.8x8.com/components/table/usage` is an "In progress" placeholder (fetched 2026-05-12). Pairs below are derived from [props.md](./props.md), [examples.md](./examples.md), [tokens.md](./tokens.md), [accessibility.md](./accessibility.md), and [DataTable-figma.md](./DataTable-figma.md), cross-validated against the audit findings in [DataTable-audit.md](./DataTable-audit.md). Replace with `figma-extract-usage` output if a Figma examples page is ever created with Do/Don't cards.

DataTable is the canonical component for **dense, structured, row-oriented data** in 8x8 product surfaces — admin lists, agent rosters, call/event logs, billing records, permission matrices, and any view that benefits from sortable columns, filtering, row selection, row actions, and pagination working together. It is a **compound family**, not a single component: a `<TableContainer>` wraps a `<TableHeader>` toolbar above a `<Table>` body and an optional `<Pagination>` footer, all driven by hook-managed state (`useTable`, `useDataRetrieval`, `useSorting`, `useRowSelection`, `usePagination`). See [props.md:36](./props.md) and [examples.md:27](./examples.md).

---

## ⚠️ Open audit conflicts

Two conflicts in [DataTable-audit.md](./DataTable-audit.md) are unresolved at the time of writing. They **do not block** the editorial guidance below, but they constrain what you can confidently say about pagination wiring and cell-type selection.

- **GAP-001 — Pagination interface duality.** MCP-returned `<Pagination>` props (`canGoBack`, `canGoNext`, `numberOfPages`, `pageNumber`, `rowsPerPage`) and example-observed props (`limit`, `offset`, `totalResults`, `loadingData`) are documented side-by-side in [props.md:121](./props.md) without resolving which is the public API. The most plausible reading is that `usePagination()` is an adapter that maps `useDataRetrieval` state (`limit/offset/...`) onto the canonical Pagination prop shape (`pageNumber/canGoBack/...`). Treat the canonical shape as authoritative for direct usage; let `usePagination()` handle the mapping when wiring to `useDataRetrieval`. Pairs below avoid recommending a specific Pagination prop set.
- **GAP-002 — Figma `type` variant ↔ Oxygen cell components.** The Figma `table cell` component set carries an 18-value `type` variant (`default`, `checkbox`, `radio`, `avatar`, `switch`, `text input`, `select input`, `icons`, `tag`, `link`, `action`, `trend`, `trend filled`, `status`, `sentiment`, `error filled`, `empty state`, `skeleton`) — see [DataTable-figma.md:120](./DataTable-figma.md). Oxygen code does not expose a `type` prop on `<Cell>`; instead, examples use named cell components (`TextCell`, `PrimaryTextCell`, `SecondaryTextCell`, `CheckboxCell`) and `cellDefinitions.*ColumnDef()` factories via `columnHelper.accessor`/`columnHelper.display` callbacks ([examples.md:51](./examples.md), [examples.md:336](./examples.md)). The full mapping is undefined; only `default`, `checkbox`, `radio`, and `skeleton` have unambiguous Oxygen analogues. Pairs below cover the four mapped types; for unmapped types (avatar, switch, tag, link, action, trend, sentiment, status) confirm with the design system team before shipping a custom cell renderer.

A third inconsistency is worth noting but is editorial-only: the published Oxygen docs intro table at `/components/intro` lists the package as `@8x8/oxygen-table`, while [props.md:3](./props.md) and the MCP report it as `@8x8/oxygen-dataTable`. Use whichever name the in-repo `package.json` resolves to in your application; this doc retains `@8x8/oxygen-dataTable` to match the MCP extraction.

---

## Anatomy

The DataTable family composes **10 Figma component sets** that map onto a small set of React sub-components ([DataTable-figma.md:53](./DataTable-figma.md)):

1. **`<TableContainer>`** — outermost wrapper. Provides layout context for everything inside ([props.md:73](./props.md)).
2. **`<TableHeader>` toolbar** — `table action header` in Figma ([DataTable-figma.md:89](./DataTable-figma.md)). Top region containing optional title, primary action, alert count, icon buttons, search, filter, favourites toggle, and the result count (`totalResultsMessage`, `currentPage` of `totalPages`). Renders above `<Table>`. See [props.md:81](./props.md).
3. **Column headers** — `<HeaderCell>` rendered inside `columnHelper.accessor` header callbacks ([props.md:110](./props.md), [examples.md:51](./examples.md)). Optional `wrapText` allows up to three wrapped lines; sortable headers gain `aria-sort` automatically ([accessibility.md:71](./accessibility.md)).
4. **Start controls cell** — left-side selection/drag column ([DataTable-figma.md:163](./DataTable-figma.md)). Renders via `cellDefinitions.getSelectColumnDef()` (multi-select) or `cellDefinitions.getSingleSelectColumnDef()` (single-select) ([props.md:161](./props.md), [examples.md:336](./examples.md)).
5. **Data cells** — `<Cell>` populated by `columnHelper.accessor` cell callbacks. The named cell components (`TextCell`, `PrimaryTextCell`, `SecondaryTextCell`, plus the upcoming mapped components for the Figma `type` variants) live inside these callbacks. Status bar (4 px left-edge indicator), icon slot, primary text, secondary text, and pinned-column dividers are anatomy slots exposed by the Figma component but managed via `meta` and `getRowStatus` in code ([DataTable-figma.md:67](./DataTable-figma.md)).
6. **Rows** — `<BodyRow>` inside `<Body>`. Hover surfaces the `table row hover` overlay with inline action buttons or icon buttons ([DataTable-figma.md:206](./DataTable-figma.md)). Active rows highlight using the `active08`/`active10` tokens ([tokens.md:30](./tokens.md)) and require a visible focus indicator ([accessibility.md:37](./accessibility.md)).
7. **End controls cell** — right-side row-action column ([DataTable-figma.md:186](./DataTable-figma.md)). Rendered via the `getRowActions` callback on `<Table>`; types include overflow (`…`), inline buttons, remove, or collapse triggers ([props.md:65](./props.md), [examples.md:271](./examples.md)).
8. **Pagination footer** — `<Pagination>` rendered inside `<TableContainer>` below `<Table>` ([props.md:121](./props.md)). Wired to `useDataRetrieval` state, typically through `usePagination()` (see GAP-001 above).
9. **Loading state** — opt-in via `loading` + `loadingText` on `<Table>`. Renders a skeleton overlay; `loadingText` is required for screen-reader announcement ([props.md:62](./props.md), [accessibility.md:90](./accessibility.md)).
10. **Empty / error state** — surfaced via `onDataRetrievalError` from `useDataRetrieval` plus the Figma `empty state` cell type. There is no dedicated empty-state slot in the API; render an inline alert via [AlertBanner](../AlertBanner/) or a full-width `<Cell type="empty state">` placeholder.

---

## Variants and capabilities

The component family supports the variants below; each is wired up via a hook or prop on the relevant sub-component, not a top-level `variant` prop.

| Capability | How it's enabled | Source |
|---|---|---|
| Sorting (server-side) | `useSorting` hook + `enableSorting: true` per column | [examples.md:209](./examples.md) |
| Filtering | `filter` prop on `<TableHeader>` driven by `useDataRetrieval.onFiltersChange` | [examples.md:386](./examples.md) |
| Pagination | `<Pagination>` inside `<TableContainer>` + `useDataRetrieval` (often through `usePagination()`) | [examples.md:122](./examples.md) |
| Multi-row selection | `cellDefinitions.getSelectColumnDef()` + `useRowSelection` | [examples.md:336](./examples.md) |
| Single-row selection | `cellDefinitions.getSingleSelectColumnDef()` + `useRowSelection` | [examples.md:338](./examples.md) |
| Row actions | `getRowActions(row)` on `<Table>` returning `ActionProps[]` | [examples.md:271](./examples.md) |
| Row click activation | `onRowClick` + `activeRowId` on `<Table>` | [examples.md:309](./examples.md) |
| Row status indicator | `getRowStatus(row)` returning `RowStatusType` | [props.md:66](./props.md), [accessibility.md:99](./accessibility.md) |
| Column resizing | `columnResizeMode: 'onChange'` + `enableColumnResizing` on `useTable`, `meta.flexible: true` per column | [examples.md:421](./examples.md) |
| Sticky / pinned columns | `meta.pinned: true` per column | [examples.md:449](./examples.md) |
| Column width preset | `meta.type: 'small' \| 'large'` | [examples.md:478](./examples.md) |
| Header wrap | `wrapText` on `<HeaderCell>` | [props.md:117](./props.md) |
| Loading skeleton | `loading={true}` + `loadingText` on `<Table>` | [examples.md:107](./examples.md), [accessibility.md:90](./accessibility.md) |
| Zebra striping | `zebra` on `<Table>` | [props.md:60](./props.md) |
| Virtual scrolling | `enableVirtualization={true}` on `<Table>` | [examples.md:464](./examples.md) |
| Compact density | Figma `isCompact?` axis on `table cell` | [DataTable-figma.md:121](./DataTable-figma.md) (code prop not yet documented — see GAP in audit) |

---

## When to use vs. alternatives

Use DataTable when **rows describe entities with three or more comparable attributes** that benefit from columnar alignment, sortability, and bulk operations (selection + row actions). Use it when users need to scan, sort, filter, or act across many rows at once.

Prefer an alternative when:

- A single entity has many attributes presented for a single record — use a detail layout, not a one-row table.
- Rows are visually heterogeneous (different fields per row, mixed media) — use a List or Card grid.
- The dataset is below ~5 rows with simple key/value pairs — use a definition list or stacked Card.
- Users need to browse media-heavy items — use a Card grid.
- The data is hierarchical with deep nesting — consider a tree view (Oxygen has no first-class tree component today; consult the design system team).

---

## Do and Don't

> **Format note.** Each pair below states the recommendation (✅ Do), the failure mode it prevents (❌ Don't), and a **Why** that cites the extracted source.

### 1. Compose the family inside `<TableContainer>`

✅ **Do** render `<TableHeader>`, `<Table>`, and the optional `<Pagination>` inside a single `<TableContainer>`, in that order.

❌ **Don't** mount a bare `<Table>` outside a container, or split the toolbar/pagination across separate layout regions of the page.

**Why.** Every example in [examples.md:27](./examples.md) uses the compound pattern `<TableContainer>` → `<TableHeader>` → `<Table>` → `<Pagination>`. The container provides layout context the sub-components depend on; the basic example at [examples.md:101–113](./examples.md) and the paginated example at [examples.md:174–201](./examples.md) follow this structure verbatim. Splitting the toolbar away from the table breaks the visual relationship between filter state and result count, and breaks the screen-reader narrative ("Filters · 31 results · table of users").

---

### 2. Always set `ariaLabel` on `<Table>`

✅ **Do** pass a unique, human-readable `ariaLabel` to every `<Table>` (e.g. `"Active user accounts"`, `"Billing invoices"`).

❌ **Don't** ship a `<Table>` without `ariaLabel`, and don't reuse the same label on multiple tables in the same view.

**Why.** The HTML `<table>` element has no implicit accessible name. [accessibility.md:44–52](./accessibility.md) flags `ariaLabel` as required: without it, screen-reader users cannot tell what the table contains, and a page with multiple unlabelled tables collapses into "table" / "table" / "table" in the rotor. WCAG 2.1 4.1.2 (Name, Role, Value) is listed as **Partial** in [accessibility.md:123](./accessibility.md) precisely because the API does not enforce the label.

---

### 3. Use named cell components, not ad-hoc renderers

✅ **Do** use the named cell components inside `columnHelper.accessor` callbacks: `<HeaderCell text="…">` for headers, `<TextCell primaryText={…}>` (or `PrimaryTextCell` / `SecondaryTextCell`) for text cells, and `cellDefinitions.getSelectColumnDef()` / `getSingleSelectColumnDef()` for selection columns.

❌ **Don't** inline raw `<div>` / `<span>` / custom HTML inside `cell:` callbacks for the four mapped Figma types (`default` → `TextCell`, `checkbox` → `CheckboxCell` via `getSelectColumnDef`, `radio` → via `getSingleSelectColumnDef`, `skeleton` → handled by `loading={true}`). Don't build a custom select column when `cellDefinitions` provides a factory.

**Why.** [examples.md:51–78](./examples.md) and [examples.md:336–349](./examples.md) show the named components being used in every documented pattern. The named components carry the correct padding, typography (`body01` for primary, `label01` for secondary — [DataTable-figma.md:304](./DataTable-figma.md)), focus styles, and ARIA attributes. Ad-hoc renderers lose Figma parity with the `table cell` component set's slots ([DataTable-figma.md:67](./DataTable-figma.md)) and break the visual rhythm of the row. For Figma cell `type` values **outside** the four mapped ones (avatar, switch, tag, link, action, trend, sentiment, status — see GAP-002 in [DataTable-audit.md](./DataTable-audit.md)), confirm the Oxygen analogue with the design system team before writing a custom cell.

---

### 4. Always pair `loading` with `loadingText`

✅ **Do** set both `loading` and `loadingText` on `<Table>` whenever data is being fetched: `<Table loading={dataRetrieval.loadingData} loadingText="Loading users…" tableApi={tableApi} ariaLabel="User list" />`.

❌ **Don't** set `loading={true}` without `loadingText`, and don't replace the table with an external spinner during refetch.

**Why.** [accessibility.md:90–95](./accessibility.md) states that without `loadingText`, the loading state is **invisible to assistive technologies** — the visual skeleton overlay covers the table body but no announcement is made. The basic example wires both props together ([examples.md:105–108](./examples.md)) and the row-actions example does the same ([examples.md:305–308](./examples.md)). Replacing the whole table with an external spinner during refetch makes the toolbar, filters, and pagination momentarily disappear, costing users their place.

---

### 5. Drive sorting through `useSorting`, not manual state

✅ **Do** manage sort state with the `useSorting` hook and pass `sortingOptions` + `sortingState` to `useTable`. Set `enableSorting: true` per sortable column.

❌ **Don't** maintain your own `useState` for the sort column and direction, and don't call `data.sort(...)` on the client before passing it to `useTable`.

**Why.** Sorting is **server-side** by design ([examples.md:208–243](./examples.md)). `useSorting` exposes `onSortingChange` that hooks into `useDataRetrieval.onSortingChange`, so the next fetch re-queries the API with the new sort. Sorting client-side after fetch only sorts the **current page** — users paging through expect "Name ascending" to span the entire dataset, not the visible 6 rows. The `aria-sort` attribute on the column header is also wired automatically by `<HeaderCell>` when sorting is hook-managed ([accessibility.md:71–77](./accessibility.md)).

---

### 6. Use the `<TableHeader>` toolbar instead of an ad-hoc external one

✅ **Do** put primary actions, filters, search, and the result count inside `<TableHeader>` via `actionItems`, `filter`, and the `listTotalResults` / `totalResultsMessage` / `currentPage` / `totalPages` props.

❌ **Don't** build a parallel toolbar above `<TableContainer>` for filter chips or result counts when `<TableHeader>` already exposes those slots.

**Why.** The Figma `table action header` ([DataTable-figma.md:89](./DataTable-figma.md)) exposes nine slots — title, action, alerts, iconButtons, search, filter, favourites, results, resultsText — designed to sit on a single row above the data. The paginated example at [examples.md:175–184](./examples.md) wires `filter`, `listTotalResults`, `loadingTotalResults`, `loadingData`, `totalResultsMessage`, `currentPage`, and `totalPages` directly into `<TableHeader>`. Mounting an external toolbar splits the visual relationship between filter state and the result count it produces, and forces you to re-implement loading and total-results coordination.

---

### 7. Pin the identity column, virtualize at 100+ rows

✅ **Do** set `meta.pinned: true` on the column that identifies the row (typically the first text column — name, ID, email) so it stays visible during horizontal scroll, and enable `enableVirtualization={true}` on `<Table>` whenever the dataset can exceed ~100 rows.

❌ **Don't** allow long datasets to render without virtualization, and don't pin more than one or two columns (every pinned column reduces the scroll area for everything else).

**Why.** Pinning the identity column is the documented pattern in [examples.md:449–455](./examples.md): "Set `meta.pinned: true` on column definitions to pin them to the left." Without it, users scrolling horizontally to read distant columns lose their row context. The virtualization threshold of 100+ rows is given verbatim in [examples.md:460–462](./examples.md): "Enable virtual scrolling for large datasets (100+ rows) via `enableVirtualization`." Beyond that threshold, full-DOM tables cause sluggish scrolling and noticeable jank on lower-end devices.

---

## Accessibility checklist (summary)

Before shipping, verify against [accessibility.md:113](./accessibility.md):

- `ariaLabel` set on every `<Table>` (pair 2).
- `loadingText` set whenever `loading={true}` (pair 4).
- Sortable headers wired through `useSorting` so `aria-sort` is correct (pair 5).
- Multi-select header has an `aria-label` (it does by default via `cellDefinitions.getSelectColumnDef()`); row checkboxes carry per-row `aria-label` values.
- Row status indicators from `getRowStatus` are also conveyed in text or via row-level `aria-label`, not by colour alone ([accessibility.md:101](./accessibility.md)).
- `focus01` / `focus02` tokens applied to all interactive elements (sortable headers, row actions, pagination controls) — light/dark token values in [tokens.md:53](./tokens.md).
- If `onRowClick` is used, verify rows are keyboard-reachable and respond to Enter/Space — the row navigation is **not** managed by default ([accessibility.md:60](./accessibility.md)).

---

## Related

- [Pagination](../Pagination/) — used inside `<TableContainer>`; has its own component-scoped guidance.
- [Checkbox](../Checkbox/) — basis for the multi-select column (`cellDefinitions.getSelectColumnDef()`).
- [Radio](../) — basis for single-select columns (component not yet extracted; see `components-to-extract.md`).
- [AlertBanner](../AlertBanner/) — recommended for empty / error / partial-data states above or in place of the table.
- [List](../List/) — alternative when rows are heterogeneous or fewer than ~5 entries.

---

_Drafted 2026-05-12. Replace with `figma-extract-usage` output if/when a Figma "↳ DataTable examples" page is populated with Do/Don't cards, or with transcribed published-docs content when `https://oxygen.8x8.com/components/table/usage` exits its "In progress" placeholder state._
