---
component: Accordion
status: draft
package: "@8x8/oxygen-accordion"
category: layout_overlay
figma: "https://www.figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=44417:100356"
variants:
  - light
  - dark
  - expandTrigger-header
  - expandTrigger-arrow
  - hasFixedHeight
props:
  - children: ReactNode
  - title: string
  - testId: string
  - text: string
  - iconLeft: ReactNode
  - contentAfterTitle: ReactNode
  - id: string
  - isExpanded: boolean
  - forcedHeight: number
  - isContentScrollable: boolean
  - hasPadding: boolean
  - expandTrigger: enum
  - translations: Translations
  - onChange: function
  - shouldCloseOnActiveClick: boolean
subcomponents:
  - "[[AccordionGroup]]"
related:
  - "[[Tabs]]"
  - "[[Icon]]"
  - "[[IconButton]]"
patterns:
  - "[[Form]]"
tokens:
  - "[[token.ui.ui06]]"
  - "[[token.ui.ui05]]"
  - "[[token.ui.ui01]]"
  - "[[token.text.textcolor01]]"
  - "[[token.text.textcolor02]]"
  - "[[token.text.textcolor10]]"
  - "[[token.interactive.disabled04]]"
  - "[[token.interactive.focus01]]"
  - "[[token.typography.bodyBold01]]"
  - "[[token.typography.label01]]"
spokes:
  - "[[Accordion.props]]"
  - "[[Accordion.anatomy]]"
  - "[[Accordion.tokens]]"
  - "[[Accordion.examples]]"
  - "[[Accordion.usage]]"
  - "[[Accordion.accessibility]]"
  - "[[Accordion.platform]]"
  - "[[Accordion.composition]]"
tags:
  - component
  - layout_overlay
  - interactive
---

## Overview

A vertically stacked set of panels where each header toggles visibility of its content area. Use when content is long or when users need to see one section at a time. Supports single-accordion and grouped modes with optional fixed-height and scrollable content.

## Spokes

- [[Accordion.props]] — 15 props including title, isExpanded, expandTrigger, forcedHeight, translations
- [[Accordion.anatomy]] — 5 top-level elements, 6 header atom elements, 4 variant axes, 5 interaction states; 7 component sets in Figma file
- [[Accordion.tokens]] — 10 tokens covering header background, title text, secondary text, focus ring, divider, AI badge; typography tokens for title and secondary text
- [[Accordion.examples]] — 10 examples covering basic group, controlled expansion, icon, arrow trigger, fixed-height, forced height, nesting, no padding, i18n, onChange blocking; all derived (0 Storybook examples from MCP — WARN-001)
- [[Accordion.usage]] — 3 Do/Don't pairs covering title accuracy, content importance, group controls; derived from website (not Figma-sourced — GAP-001)
- [[Accordion.accessibility]] — keyboard, ARIA, focus management; aria-controls not confirmed from source (GAP-016 applied); default translations unknown (GAP-012)
- [[Accordion.platform]] — PUI context unknown; run pui-mcp-extract (GAP-002)
- [[Accordion.composition]] — AccordionGroup container; iconLeft and contentAfterTitle slots; 2-level nesting max; patterns: Form
