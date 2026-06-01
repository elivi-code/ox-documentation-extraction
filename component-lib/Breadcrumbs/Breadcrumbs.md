---
component: Breadcrumbs
status: draft
package: "@8x8/oxygen-breadcrumbs"
category: navigation
figma: "https://www.figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=21927:40413"
usage_provenance: editorial
variants:
  - light
  - dark
  - collapsed
  - overflow-menu
props:
  - children: ReactNode
  - maxItems: number
  - itemsBeforeCollapse: number
  - itemsAfterCollapse: number
  - separator: ReactNode
  - ariaLabel: string
  - collapsedTitle: string
  - theme: object
  - isActive: boolean
  - href: string
  - target: string
  - onClick: function
subcomponents:
  - "[[Breadcrumb]]"
related:
  - "[[Icon]]"
patterns:
  - "[[PageHeader]]"
tokens:
  - "[[token.actions.action08]]"
  - "[[token.interactive.active07]]"
  - "[[token.text.textcolor01]]"
  - "[[token.ui.ui01]]"
  - "[[token.typography.body01]]"
spokes:
  - "[[Breadcrumbs.props]]"
  - "[[Breadcrumbs.anatomy]]"
  - "[[Breadcrumbs.tokens]]"
  - "[[Breadcrumbs.usage]]"
  - "[[Breadcrumbs.accessibility]]"
  - "[[Breadcrumbs.platform]]"
  - "[[Breadcrumbs.composition]]"
tags:
  - component
  - navigation
  - interactive
---

## Overview

A secondary navigation pattern that shows the user's location within a hierarchical site structure. The trail starts at Home (or the highest parent) and ends at the current page, which is rendered as plain text rather than a link. Long trails auto-collapse behind an ellipsis with an overflow menu. Compose with `Breadcrumb` children.

## Spokes

- [[Breadcrumbs.props]] — 12 props (8 `Breadcrumbs` + 4 `Breadcrumb`) including children, maxItems, separator, ariaLabel; `isActive` unverified (GAP-008), `theme` shape unresolved (GAP-009)
- [[Breadcrumbs.anatomy]] — 7 top-level elements, 2 sub-component atoms, 3 variant axes (mode / collapse? / ↪ menu?), 5 interaction states; 6 component sets in Figma
- [[Breadcrumbs.tokens]] — 4 color tokens + body01 typography; rest-state only, from Figma design context not the MCP registry (GAP-001); hover/active/focus unresolved (GAP-003)
- [[Breadcrumbs.usage]] — 6 Do/Don't pairs covering label clarity, current-page handling, single-line placement, auto-collapse, localisation, secondary-nav fit; editorial provenance (GAP-012)
- [[Breadcrumbs.accessibility]] — keyboard, ARIA (nav / ol / a / aria-current / button), focus; roles inferred not DOM-verified (WARN-001); no Figma a11y annotations (GAP-006)
- [[Breadcrumbs.platform]] — no PUI requirements (engineer-confirmed)
- [[Breadcrumbs.composition]] — `Breadcrumb` children; separator + overflow-menu slots; complements primary navigation
