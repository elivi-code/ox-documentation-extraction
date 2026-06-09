---
parent: "[[Pagination]]"
section: props
---

## Installation

```bash
# yarn
yarn add @8x8/oxygen-pagination

# npm
npm install @8x8/oxygen-pagination
```

**Registry prerequisite** — add to `.npmrc`:
```
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```
Or `.yarnrc.yml`:
```yaml
npmScopes:
  8x8:
    npmRegistryServer: "https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/"
nodeLinker: node-modules
```
> VPN connection to 8x8 required to access the private Artifactory registry.

## Import

```tsx
import Pagination, { usePagination, PaginationState } from '@8x8/oxygen-pagination';
```

## Props

<!-- GAP-005: descriptions for canGoBack, canGoNext, numberOfPages, pageNumber, rowsPerPage, rowsPerPageOptions, and size are inferred from usage documentation and Figma — not verbatim from OX MCP (empty strings returned). Human review recommended before publishing. -->

| Prop | Type | Required | Default | Description | Accepts |
|------|------|----------|---------|-------------|---------|
| `canGoBack` | `boolean` | ✅ | — | Whether the previous page button is enabled | — |
| `canGoNext` | `boolean` | ✅ | — | Whether the next page button is enabled | — |
| `numberOfPages` | `number` | ✅ | — | Total number of pages | — |
| `pageNumber` | `number` | ✅ | — | Current page number (1-based) | — |
| `rowsPerPage` | `number` | ✅ | — | Number of rows displayed per page | — |
| `onPaginationChange` | `(pagination: PaginationState) => void` | ✅ | — | Handler for pagination state change | — |
| `translations` | `Translations` | ✅ | — | Localisation strings for all labels | — |
| `rowsPerPageOptions` | `number[]` | ❌ | — | Available rows-per-page values in the dropdown; omit to hide the rows-per-page section | — |
| `size` | `PaginationSize` | ❌ | `"default"` | Size variant of the component | — |
| `isDisabled` | `boolean` | ❌ | `false` | Whether the entire component is disabled | — |
| `testId` | `string` | ❌ | — | Test ID for automated testing | — |

## Type Definitions

### `PaginationState`

```ts
interface PaginationState {
  pageNumber: number;
  rowsPerPage: number;
}
```

### `Translations`

```ts
interface Translations {
  rowsPerPage: string;   // e.g. "Rows per page:"
  prevPage: string;      // e.g. "Prev"
  numberOfPages: string; // e.g. `of ${numberOfPages} pages`; pass "" to hide
  nextPage: string;      // e.g. "Next"
}
```

### `PaginationSize`

<!-- STUB:GAP-004 source="Look up PaginationSize enum in @8x8/oxygen-pagination package source to confirm exact string values — OX MCP returned type name without member expansion" -->

Confirmed values (inferred from usage docs + Figma variant axis — not from MCP source): **`"default"`** and **`"small"`**.

## `usePagination` Hook

The `usePagination` hook derives computed props from consumer-owned state. **Always call it outside the `<Pagination>` element.**

```ts
const { canGoBack, canGoNext, numberOfPages, pageNumber, rowsPerPage } =
  usePagination(pagination: PaginationState, totalRecords: number);
```

| Return value | Type | Description |
|---|---|---|
| `canGoBack` | `boolean` | Whether navigating to the previous page is possible |
| `canGoNext` | `boolean` | Whether navigating to the next page is possible |
| `numberOfPages` | `number` | Computed total page count (`Math.ceil(totalRecords / rowsPerPage)`) |
| `pageNumber` | `number` | Current page number (pass-through from state) |
| `rowsPerPage` | `number` | Current rows per page (pass-through from state) |
