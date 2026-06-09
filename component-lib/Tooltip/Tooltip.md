---
component: Tooltip
status: draft
version: "@8x8/oxygen-tooltip"
category: overlays_contextual
figma: "https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=1797-0"
variants: [Light, Dark]
props:
  - title: ReactNode
  - children: ReactNode
  - orientation: Orientation
  - delay: number
  - offset: OffsetOptions
  - showOn: string
  - disableInteractive: boolean
  - disableDescribedBy: boolean
  - enableArrow: boolean
  - triggerRef: HTMLElement
  - customCloseHandlers: Handler[]
  - renderContainer: HTMLElement
  - renderContainerId: string
  - includeWrapper: boolean
  - modifiers: object
subcomponents: ["[[_Tip]]"]
related: ["[[Popover]]", "[[Modal]]", "[[StaticTooltip]]"]
patterns: []
tokens:
  - "[[--ui/ui07]]"
  - "[[--text/textcolor04]]"
  - "[[--ui/shadow01]]"
  - "[[--typography/body01/font-size]]"
  - "[[--typography/body01/font-weight]]"
  - "[[--typography/body01/line-height]]"
  - "[[--typography/body01/letter-spacing]]"
  - "[[--typography/body01/font-family]]"
spokes:
  - "[[Tooltip.props]]"
  - "[[Tooltip.anatomy]]"
  - "[[Tooltip.tokens]]"
  - "[[Tooltip.usage]]"
  - "[[Tooltip.accessibility]]"
  - "[[Tooltip.platform]]"
  - "[[Tooltip.composition]]"
tags: [component, overlays_contextual, interactive]
---

## Overview

Tooltip displays contextual information when users hover over or focus on a trigger element. It is a presentational overlay for brief, supplementary hints — plain text only, ≤ 140 characters (English). Pair with a focusable trigger and keep content non-critical; for interactive or load-bearing content escalate to [[Popover]] or [[Modal]].

---

## Spokes

- [[Tooltip.props]] — 15 props including `title`, `orientation`, `delay`; StaticTooltip companion component; inferred code examples
- [[Tooltip.anatomy]] — 3 elements (Content, Text, `_Tip`) across 2 mode variants (Light/Dark), 4 orientation groups with start/end sub-positions
- [[Tooltip.tokens]] — 8 tokens covering background (`--ui/ui07`), text color (`--text/textcolor04`), shadow (`--ui/shadow01`), and body typography (`--typography/body01/*`)
- [[Tooltip.usage]] — 5 Do/Don't pairs covering content length, critical information, interactivity, icon-button labelling, and component selection; Tooltip vs. Popover vs. Modal comparison
- [[Tooltip.accessibility]] — keyboard (Tab / Escape / focus), ARIA (`role="tooltip"`, `aria-describedby`), focus management; WCAG 2.1 AA checklist
- [[Tooltip.platform]] — no PUI requirements
- [[Tooltip.composition]] — contains `[[_Tip]]` arrow atom; layered with `[[Popover]]` on shared triggers; escalation path to `[[Modal]]`
