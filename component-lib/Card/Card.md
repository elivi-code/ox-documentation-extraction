---
component: Card
status: draft
deprecated: true
package: "@8x8/oxygen-card"
category: layout_overlay
figma: "https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=11263:11501"
variants: [Light, Dark]
states: [Rest, Hover, Focus]
props:
  - children: ReactNode
  - testId: string
  - theme: "Partial<CardTheme>"
  - data: "StatisticsItemData[]"
subcomponents: ["[[Header]]", "[[Separator]]", "[[Statistics]]"]
related: []
patterns: []
tokens: ["[[ui01]]", "[[ui02]]", "[[ui03]]"]
spokes:
  - "[[Card.props]]"
  - "[[Card.anatomy]]"
  - "[[Card.tokens]]"
  - "[[Card.usage]]"
  - "[[Card.accessibility]]"
  - "[[Card.platform]]"
  - "[[Card.composition]]"
tags: [component, layout_overlay, deprecated]
---

# Card

> ⚠️ **DEPRECATED** — `@8x8/oxygen-card` is deprecated, including all sub-components (Card, Header, Separator, Statistics). **No replacement is documented.** Do not adopt for new work; existing usage should be on a migration path. For new layouts, compose Oxygen primitives directly with the same surface and border tokens.

## Overview

Card is a presentational layout container that shows a snippet of information leading the user to more. It can hold any content, adapts its size to the design, and by default carries a header and a CTA; the whole card is typically clickable and navigates to a detail view. It composes three sub-components — [[Header]], [[Separator]], and [[Statistics]] — and exposes two variant axes (`Mode`: Light/Dark, `State`: Rest/Hover/Focus). Status is **draft**: the spec carries 11 open SOURCE_GAPs (token names, spacing, type shapes, usage, accessibility) pending upstream resolution.

## Spokes

- [[Card.props]] — 4 props (`children`, `testId`, `theme`, `data`) across 4 sub-components; StatisticsItemData & theme shapes unresolved (GAP-003/004)
- [[Card.anatomy]] — up to 4 elements across 6 variants (2 modes × 3 states); spacing & description missing (GAP-007/010)
- [[Card.tokens]] — 3 global tokens (ui01/02/03) covering border + surface; rest-fill token, opaque IDs, dark hover/focus, typography all open (GAP-005/006/008/009)
- [[Card.usage]] — 4 Do/Don't pairs covering lifecycle, clickable semantics, heading level, CTA defaults (provisional — GAP-001)
- [[Card.accessibility]] — keyboard, ARIA roles, screen-reader, WCAG 2.1 AA; all inferred, unconfirmed (GAP-011)
- [[Card.platform]] — no PUI requirements
- [[Card.composition]] — used with [[Header]], [[Separator]], [[Statistics]]; 3 Storybook-derived examples (GAP-012)
