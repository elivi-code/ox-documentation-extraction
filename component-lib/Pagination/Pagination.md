---
component: Pagination
status: draft
category: navigation
figma: "https://figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=55766:411"
variants:
  - default
  - small
  - disabled
  - light
  - dark
props:
  - canGoBack: boolean
  - canGoNext: boolean
  - numberOfPages: number
  - pageNumber: number
  - rowsPerPage: number
  - onPaginationChange: function
  - translations: object
  - rowsPerPageOptions: "number[]"
  - size: enum
  - isDisabled: boolean
  - testId: string
subcomponents:
  - "[[Select]]"
related:
  - "[[Breadcrumbs]]"
  - "[[Button]]"
patterns:
  - "[[DataTable]]"
tokens:
  - "[[token.text.textcolor01]]"
  - "[[token.ui.ui05]]"
  - "[[token.interactive.disabled01]]"
  - "[[token.interactive.disabled04]]"
  - "[[token.interactive.focus01]]"
  - "[[token.typography.body01]]"
  - "[[token.typography.label01]]"
spokes:
  - "[[Pagination.props]]"
  - "[[Pagination.anatomy]]"
  - "[[Pagination.tokens]]"
  - "[[Pagination.usage]]"
  - "[[Pagination.accessibility]]"
  - "[[Pagination.platform]]"
  - "[[Pagination.composition]]"
tags:
  - component
  - navigation
  - interactive
---

## Overview

Pagination lets users move through a large dataset split across multiple pages. It renders a horizontal control with a rows-per-page selector on the left, page navigation (previous · current page · count · next) on the right, and a compact mode that drops the rows-per-page region below 548px container width. Always manage state with `useState` and derive computed props with the `usePagination` hook — both outside the `<Pagination>` element.

## Spokes

- [[Pagination.props]] — 11 props including canGoBack, canGoNext, translations (required ×7), rowsPerPageOptions, size, isDisabled; plus usePagination hook
- [[Pagination.anatomy]] — 10 elements across 4 variant axes (mode, size, isDisabled, breakpoint), 2 modelled states (Default, Disabled); 3 source gaps (states, a11y annotations, component details)
- [[Pagination.tokens]] — 7 tokens covering text color (textcolor01), dropdown background (ui05), disabled states (disabled01, disabled04), focus ring (focus01), typography (body01, label01); confirmed via batch alias-chain traversal 2026-05-05
- [[Pagination.usage]] — 7 Do/Don't pairs covering dataset scoping, row count threshold, known/unknown page type, responsive layout, localisation, keyboard focus, rowsPerPageOptions
- [[Pagination.accessibility]] — keyboard, ARIA, focus (all inferred — WARN-001; spot-check against rendered DOM before publishing)
- [[Pagination.platform]] — no PUI requirements
- [[Pagination.composition]] — sub-components Select (×2) + icon buttons; commonly used inside DataTable; related to Breadcrumbs, Button
