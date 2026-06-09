---
component: SlideOut
status: draft
package: "@8x8/oxygen-slide-out"
category: layout_overlay
figma: null
variants: []
props:
  - children: ReactNode
  - isVisible: boolean
  - isResizable: boolean
  - hasAnimation: boolean
  - defaultWidth: number
  - minWidth: number
  - maxWidth: number
  - className: string
  - testId: string
  - onResize: function
subcomponents: []
related: ["[[Modal]]", "[[Drawer]]", "[[Tooltip]]"]
patterns: []
tokens: []
spokes:
  - "[[SlideOut.props]]"
  - "[[SlideOut.anatomy]]"
  - "[[SlideOut.tokens]]"
  - "[[SlideOut.usage]]"
  - "[[SlideOut.accessibility]]"
  - "[[SlideOut.platform]]"
  - "[[SlideOut.composition]]"
pipeline_stage: spec_ready
audit_verdict: PARTIAL
tags:
  - component
  - layout_overlay
  - interactive
  - oxygen
---

## Overview

`SlideOut` (`@8x8/oxygen-slide-out`) is a controlled side panel that slides in over the trailing edge of the page. Unlike a Modal it does not block the underlying UI; unlike a Drawer it is opened on specific user intent and dismissed rather than serving as persistent navigation. The component is deliberately thin — it manages visibility and an optional resize handle, and delegates dismissal, focus management, and accessible labelling entirely to the consuming application.

> **Status: draft** — GAP-001 (no Figma design) is a permanent blocker for the figma_fidelity dimension; GAP-008 (0 tokens from MCP) blocks the tokens dimension. Five of seven dimensions are covered. See [[SlideOut.anatomy]] and [[SlideOut.tokens]] for STUB markers.

## Spokes

- [[SlideOut.props]] — 9 props including `children`, `isVisible`, `isResizable`; `onResize` observed in Storybook but absent from registry (GAP-005)
- [[SlideOut.anatomy]] — no Figma design exists; anatomy inferred from props and examples (GAP-001 blocker)
- [[SlideOut.tokens]] — 0 tokens from MCP; visual token bindings unknown (GAP-008)
- [[SlideOut.usage]] — 7 Do/Don't pairs covering component selection, controlled state, ARIA role, dismissal wiring, `aria-hidden`, resize conditions, content scoping (editorial — GAP-002/WARN-002)
- [[SlideOut.accessibility]] — keyboard, ARIA, focus management; all inferred — no confirmed MCP source data (GAP-009)
- [[SlideOut.platform]] — no PUI requirements
- [[SlideOut.composition]] — no subcomponents; header/footer/close composed inside `children`; related to [[Modal]], [[Drawer]], [[Tooltip]]
