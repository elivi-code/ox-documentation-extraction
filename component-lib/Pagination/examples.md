---
component: Pagination
package: "@8x8/oxygen-pagination"
category: navigation
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Pagination/props]]"
  - "[[Pagination/tokens]]"
  - "[[Pagination/accessibility]]"
  - "[[Pagination/Pagination-figma]]"
  - "[[Pagination/Pagination-usage]]"
  - "[[Pagination/Pagination-audit]]"
tags:
  - oxygen
  - component/Pagination
  - role/examples
  - stage/spec_ready
  - category/navigation
---
# Pagination — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Overview

Pagination is a component used to navigate through a large set of data divided into multiple pages. It allows users to move forward and backward through content, providing an intuitive way to access paginated information.

**Key pattern:** Always manage pagination state with `useState` and compute derived values with the `usePagination` hook — both outside the `<Pagination>` component.

---

## Basic Usage

```tsx
import React, { useState } from 'react';
import Pagination, {
  usePagination,
  PaginationState,
} from '@8x8/oxygen-pagination';

const MyComponent = ({ totalRecords }: { totalRecords: number }) => {
  const [pagination, setPagination] = useState<PaginationState>({
    pageNumber: 1,
    rowsPerPage: 10,
  });

  const { canGoBack, canGoNext, numberOfPages, pageNumber, rowsPerPage } =
    usePagination(pagination, totalRecords);

  return (
    <Pagination
      canGoBack={canGoBack}
      canGoNext={canGoNext}
      numberOfPages={numberOfPages}
      onPaginationChange={setPagination}
      pageNumber={pageNumber}
      rowsPerPage={rowsPerPage}
      rowsPerPageOptions={[5, 10, 20, 50, 100, 250]}
      translations={{
        rowsPerPage: 'Rows per page:',
        prevPage: 'Prev',
        numberOfPages: `of ${numberOfPages} pages`,
        nextPage: 'Next',
      }}
    />
  );
};
```

---

## Anatomy

1. **Rows per page label** — text label preceding the rows-per-page dropdown
2. **Rows per page dropdown** — lets user choose how many rows display per page
3. **Previous/next buttons** — navigate one page back or forward
4. **Location page dropdown** — lets user jump to a specific page
5. **Total number of pages label** — displays total page count

---

## Sizes

Two size variants are available:

1. **Default** — standard size
2. **Small** — compact size for denser layouts

```tsx
<Pagination
  size="small"
  {/* ... other required props */}
/>
```

---

## When to Use

- When there are too many results to display on one page.
- For tables with more than ten rows.

## When Not to Use

- Do not use pagination if the items or data are not part of the same set.

_Source: Oxygen MCP · Extracted 2026-05-01_
