---
parent: "[[Pagination]]"
section: composition
---

## Sub-components

Pagination uses these sub-components structurally (fixed, not swappable via instance slots):

| Sub-component | Instance count | Role |
|---------------|---------------|------|
| `[[Select]]` | 2 | Rows-per-page dropdown (slot 1) + page selector dropdown (slot 2) |
| Icon button (previousButton) | 1 | `arrow-left-long` icon; padding and size vary with `size` prop and breakpoint |
| Icon button (nextButton) | 1 | `arrow-right-long` icon; padding and size vary with `size` prop and breakpoint |

The `[[Select]]` sub-component is used twice with different widths: `88px` (default size) / `72px` (small size) — these are hardcoded values, not token-bound.

## Commonly Used Inside

| Component / Pattern | Role |
|--------------------|------|
| `[[DataTable]]` | Most common host; the rows-per-page choice changes the DataTable's visible row count. Pagination sits below the table body. |

## Related Components

| Component | Relationship |
|-----------|-------------|
| `[[Breadcrumbs]]` | Related by docs page. Pagination moves through the *same* dataset; Breadcrumbs navigate *up* a hierarchy. Do not substitute. |
| `[[Select]]` | Used internally as sub-component. If the dataset needs filtering *above* the table, use `Select` outside Pagination, not inside it. |
| `[[Button]]` | Page-level actions ("Add", "Export") sit outside Pagination, not in the same row. |
