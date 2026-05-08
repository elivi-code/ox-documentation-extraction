---
component: Pagination
package: "@8x8/oxygen-pagination"
category: navigation
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Pagination/examples]]"
  - "[[Pagination/tokens]]"
  - "[[Pagination/accessibility]]"
  - "[[Pagination/Pagination-figma]]"
  - "[[Pagination/Pagination-usage]]"
  - "[[Pagination/Pagination-audit]]"
tags:
  - oxygen
  - component/Pagination
  - role/props
  - stage/spec_ready
  - category/navigation
---
# Pagination — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```bash
# yarn
yarn add @8x8/oxygen-pagination

# npm
npm install @8x8/oxygen-pagination
```

**Registry prerequisite:** Add to `.npmrc`:
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

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `canGoBack` | `boolean` | ✅ | — | Whether the previous page button is enabled |
| `canGoNext` | `boolean` | ✅ | — | Whether the next page button is enabled |
| `numberOfPages` | `number` | ✅ | — | Total number of pages |
| `pageNumber` | `number` | ✅ | — | Current page number (1-based) |
| `rowsPerPage` | `number` | ✅ | — | Number of rows displayed per page |
| `onPaginationChange` | `(pagination: PaginationState) => void` | ✅ | — | Handler for paginationchange event |
| `translations` | `Translations` | ✅ | — | Localisation strings for all labels (see below) |
| `rowsPerPageOptions` | `number[]` | ❌ | — | Array of available rows-per-page values shown in the dropdown |
| `size` | `PaginationSize` | ❌ | — | Size variant of the component |
| `isDisabled` | `boolean` | ❌ | — | Whether the component is disabled |
| `testId` | `string` | ❌ | — | Test ID for automated testing |

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
  numberOfPages: string; // e.g. "of ${numberOfPages} pages"
  nextPage: string;      // e.g. "Next"
}
```

### `PaginationSize`

Exact values not documented by MCP. Based on usage docs, two sizes exist: **default** and **small**.

## `usePagination` Hook

The `usePagination` hook must be used outside the component to derive the computed props:

```ts
const { canGoBack, canGoNext, numberOfPages, pageNumber, rowsPerPage } =
  usePagination(pagination: PaginationState, totalRecords: number);
```

| Return value | Type | Description |
|---|---|---|
| `canGoBack` | `boolean` | Whether going to previous page is possible |
| `canGoNext` | `boolean` | Whether going to next page is possible |
| `numberOfPages` | `number` | Computed total page count |
| `pageNumber` | `number` | Current page number |
| `rowsPerPage` | `number` | Current rows per page |

_Source: Oxygen MCP · Extracted 2026-05-01_
