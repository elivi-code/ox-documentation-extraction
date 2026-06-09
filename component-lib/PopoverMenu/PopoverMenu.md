---
component: PopoverMenu
status: draft
package: "@8x8/oxygen-popover"
category: overlays_contextual
figma: "https://figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=47175:1414"
variants:
  - mode: light/dark
  - header: true/false
  - footer: true/false
  - scroll: true/false
props:
  - children: ReactElement
  - items: array
  - floatingContent: ReactNode
  - isOpen: boolean
  - setIsOpen: function
  - activeProp: string
  - disabledProp: string
  - isDisabled: boolean
  - placement: Placement
  - portalTargetRef: RefObject
  - maxHeight: number
  - header: ReactNode
  - footer: ReactNode
  - onMenuOpenToggle: function
  - onMenuItemClick: function
  - onUpdate: function
  - onCancel: function
  - testId: string
subcomponents:
  - "[[Divider]]"
  - "[[SectionHeader]]"
  - "[[ListItem]]"
related:
  - "[[Tooltip]]"
  - "[[Modal]]"
  - "[[DropdownButton]]"
  - "[[Button]]"
patterns: []
tokens:
  - "[[token.ui.ui06]]"
  - "[[token.ui.ui01]]"
  - "[[token.ui.shadow01]]"
  - "[[token.text.textcolor01]]"
  - "[[token.text.textcolor02]]"
  - "[[token.text.textcolor09]]"
  - "[[token.ui.ui05]]"
  - "[[token.ui.ui23]]"
  - "[[token.ui.ui22]]"
  - "[[token.actions.action03]]"
  - "[[token.actions.action08]]"
  - "[[token.actions.action09]]"
  - "[[token.typography.bodybold01]]"
  - "[[token.typography.body01]]"
  - "[[token.typography.heading01]]"
  - "[[token.typography.labelbold01]]"
spokes:
  - "[[PopoverMenu.props]]"
  - "[[PopoverMenu.anatomy]]"
  - "[[PopoverMenu.tokens]]"
  - "[[PopoverMenu.usage]]"
  - "[[PopoverMenu.accessibility]]"
  - "[[PopoverMenu.platform]]"
  - "[[PopoverMenu.composition]]"
pipeline_stage: draft
audit_verdict: "NO"
open_conflicts:
  - GAP-001
  - GAP-002
  - GAP-003
tags:
  - oxygen
  - component/PopoverMenu
  - role/hub
  - stage/draft
  - category/overlays_contextual
---

## Overview

`PopoverMenu` displays a floating, dismissible panel anchored to a trigger element. The `@8x8/oxygen-popover` package exports two components: `PopoverMenu` (high-level — manages open state, renders a structured list via `items`) and `Popover` (low-level — fully controlled open state, accepts any `floatingContent`). Use `PopoverMenu` for standard dropdown menus; use `Popover` when you need full control over the floating panel content.

> **Status: draft** — 3 CONFLICTs unresolved (GAP-001: example API naming; GAP-002: footer padding light/dark discrepancy; GAP-003: Apply button contrast in dark mode). Resolve in `PopoverMenu-audit.md` before marking authoritative.

---

## Spokes

- [[PopoverMenu.props]] — 26 props across Popover (11) and PopoverMenu (15), including `items`, `children`, `header`, `footer`, `onMenuItemClick`, `placement`; sub-component props (`Divider`, `SectionHeader`, `ListItemWrapperProps`) absent from MCP (GAP-004)
- [[PopoverMenu.anatomy]] — 3 regions (header, content, footer) with 4 variant axes (`mode`, `header`, `footer`, `scroll`), 8 list item variants, 5 states; screenshot missing (GAP-008)
- [[PopoverMenu.tokens]] — 13+ token bindings sourced from Figma covering background, border, shadow, text, actions, typography; 11 hardcoded values flagged for tokenisation; CONFLICT on footer padding (GAP-002)
- [[PopoverMenu.usage]] — 8 Do/Don't pairs covering component selection, trigger model, dismissal, header/footer use, list item type selection, destructive patterns; editorial — no Figma cards yet (GAP-007)
- [[PopoverMenu.accessibility]] — keyboard, ARIA, focus management; all content inferred from ARIA APG Menu Button pattern — verification required (GAP-006); CONFLICT on Apply button contrast in dark mode (GAP-003)
- [[PopoverMenu.platform]] — no PUI requirements
- [[PopoverMenu.composition]] — composed of Divider, SectionHeader, ListItem sub-components; used alongside DropdownButton; CONFLICT on example API naming (GAP-001)

---

_Source: Oxygen MCP · Figma MCP · figma-console MCP · doc-rewrite 2026-06-08_
