---
component: Tabs
status: partial
category: layout_overlay
package: "@8x8/oxygen-tabs"
figma: "https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=85651-78740"
variants:
  - rest
  - hover
  - selected
  - disabled
props:
  - children: ReactNode
  - color: enum
  - forwardedRef: "object | func"
  - value: any
  - isActive: boolean
  - isDisabled: boolean
  - isStretched: boolean
  - onClick: function
  - testId: string
subcomponents:
  - "[[Icon]]"
  - "[[Badge]]"
  - "[[IconButton]]"
related:
  - "[[SegmentedControl]]"
  - "[[Radio]]"
  - "[[Select]]"
  - "[[Accordion]]"
patterns: []
tokens:
  - "[[ui/ui01]]"
  - "[[actions/action01]]"
  - "[[text/textColor01]]"
  - "[[text/textColor02]]"
  - "[[interactive/disabled02]]"
  - "[[icon/icon01]]"
  - "[[interactive/focus01]]"
  - "[[notification/notification01]]"
  - "[[typography/body01]]"
  - "[[typography/bodyBold01]]"
  - "[[typography/labelBold01]]"
spokes:
  - "[[Tabs.props]]"
  - "[[Tabs.anatomy]]"
  - "[[Tabs.tokens]]"
  - "[[Tabs.usage]]"
  - "[[Tabs.accessibility]]"
  - "[[Tabs.platform]]"
  - "[[Tabs.composition]]"
pipeline_stage: doc_rewrite
audit_verdict: YES
tags:
  - oxygen
  - component/Tabs
  - role/hub
  - stage/doc_rewrite
  - category/layout_overlay
---

## Overview

Tabs switches the user between sibling content sections within a single page. It is a **controlled** component — the consuming application owns which tab is active (`isActive` prop) and handles selection via `onClick`. When the container narrows, tabs collapse right-to-left into a disclosure popover (`tabsDisclosure`), always keeping the active tab visible; at extreme narrowing, the single remaining tab becomes a popover trigger itself (`hasDropdown`).

## Spokes

- [[Tabs.props]] — 11 props across `<Tabs>` (children, color, forwardedRef) and `<Tab>` (children, color, value, isActive, isDisabled, isStretched, onClick, testId); color default undocumented (GAP-008); isStretched description inferred (GAP-007)
- [[Tabs.anatomy]] — 4 variants (rest, hover, selected, disabled) across 3 Figma components (`tabs` COMPONENT_SET, `tabsDisclosure`, `.Tabs Popover`); 5 states; screenshots pending (GAP-004); selectIcon icon name pending (GAP-006)
- [[Tabs.tokens]] — 10 color tokens + 3 typography tokens covering border (ui/ui01, actions/action01, text/textColor01, interactive/disabled02), text (textColor01/02, disabled02), icon, focus ring, notification badge; no OX token namespace
- [[Tabs.usage]] — 7 Do/Don't pairs covering: sibling-page use vs. navigation/wizard, controlled state + unique values, tab count + overflow, icon/badge intent, isStretched row-level consistency, onClick purity, ARIA contract + arrow-key roving focus; editorial draft pending Figma cards (GAP-003)
- [[Tabs.accessibility]] — keyboard (Tab/Shift+Tab/Enter/Space/Escape confirmed; Left/Right arrow unconfirmed — WARN-002), ARIA roles recommended but not verified in OX baseline, focus management; WCAG 1.4.1 ✅ (2px underline + bold weight = two non-color indicators)
- [[Tabs.platform]] — no PUI requirements; `@8x8/pui-use-navigation` rejected as general shell hook, not Tabs-specific
- [[Tabs.composition]] — structured as `<Tabs>` > N × `<Tab>` > optional [[Icon]] / [[Badge]]; `tabsDisclosure` (built on [[IconButton]]) + `.Tabs Popover` rendered automatically by the container on overflow; used in settings panes, record detail views, analytics dimension switching
