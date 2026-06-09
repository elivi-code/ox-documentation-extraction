---
component: Spinner
status: draft
package: "@8x8/oxygen-loaders"
category: feedback_status
figma: "https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=1561:11079"
variants:
  - "light/default"
  - "light/default/inverted"
  - "light/small"
  - "light/small/inverted"
  - "dark/default"
  - "dark/small"
  - "complete/light"
  - "complete/dark"
  - "error/light"
  - "error/dark"
props:
  - size: "number | enum"
  - strokeWidth: number
  - hasAnimation: boolean
  - text: string
  - testId: string
subcomponents: []
related:
  - "[[ProgressBar]]"
  - "[[Skeleton]]"
patterns: []
tokens: []
spokes:
  - "[[Spinner.props]]"
  - "[[Spinner.anatomy]]"
  - "[[Spinner.tokens]]"
  - "[[Spinner.usage]]"
  - "[[Spinner.accessibility]]"
  - "[[Spinner.platform]]"
  - "[[Spinner.composition]]"
tags:
  - oxygen
  - component/Spinner
  - category/feedback_status
---

## Overview

Spinner is a passive, indeterminate loading indicator that renders as a continuously rotating arc with optional supporting text. It signals that a background task is in flight — a page load, section hydration, or inline fetch — and transitions to a separate "Spinner complete" component set (complete / error states) when loading ends. It is non-interactive and not focusable; all accessibility responsibility falls on the label supplied via `text` or `aria-label`.

## Spokes

- [[Spinner.props]] — 5 props including size, strokeWidth, hasAnimation; 2 CONFLICTs (isInverted, large2x) require human resolution
- [[Spinner.anatomy]] — 10 variant combinations across 2 component sets (Spinner + Spinner complete), 4 states; inner spacing data absent (GAP-008)
- [[Spinner.tokens]] — 0 tokens resolved; all bindings blocked by Variables API access (GAP-006, GAP-007, GAP-009)
- [[Spinner.usage]] — 6 Do/Don't pairs covering size selection, supporting text labelling, motion sensitivity, component choice (vs ProgressBar / Skeleton), and stacking; editorial draft (no Figma examples page)
- [[Spinner.accessibility]] — keyboard (not focusable), ARIA (role="status" inferred), WCAG 2.1 AA checklist including 2.3.3
- [[Spinner.platform]] — no PUI requirements
- [[Spinner.composition]] — no subcomponents; component swap pattern for terminal states; commonly paired with [[ProgressBar]] and [[Skeleton]]
