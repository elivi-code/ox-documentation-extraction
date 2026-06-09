---
component: SidebarMenu
status: draft
package: "@8x8/oxygen-sidebar-menu"
category: navigation
figma: "https://www.figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=62897:18973"
variants:
  - Config-driven
  - Declarative
  - Light mode
  - Dark mode
  - Expanded
  - Collapsed
props:
  - items: "SidebarItemProps[]"
  - position: enum
  - initialCollapsedState: boolean
  - collapseLabel: string
  - expandLabel: string
  - onCollapseChange: function
  - linkComponent: ComponentType
  - linkProp: string
  - testId: string
subcomponents:
  - "[[MenuItem]]"
  - "[[SubMenuItem]]"
  - "[[MenuList]]"
  - "[[SidebarContainer]]"
  - "[[CollapseItem]]"
related: []
patterns: []
tokens:
  - "[[token.ui25]]"
  - "[[token.hover12]]"
  - "[[token.active12]]"
  - "[[token.hover13]]"
spokes:
  - "[[SidebarMenu.props]]"
  - "[[SidebarMenu.anatomy]]"
  - "[[SidebarMenu.tokens]]"
  - "[[SidebarMenu.usage]]"
  - "[[SidebarMenu.accessibility]]"
  - "[[SidebarMenu.platform]]"
  - "[[SidebarMenu.composition]]"
tags:
  - oxygen
  - component/SidebarMenu
  - role/hub
  - stage/draft
  - category/navigation
---

## Overview

`SidebarMenu` is the primary persistent navigation shell for 8x8 applications. It ships two API surfaces: a config-driven `<Sidebar>` that manages collapse state internally via `initialCollapsedState`/`onCollapseChange`, and a declarative pattern composing `SidebarContainer` + `MenuList` + `MenuItem` + `SubMenuItem` + `CollapseItem` for full external state control. Both surfaces support icons, badges, sub-menus, a footer slot, and router integration via `linkComponent`/`linkProp`.

## Spokes

- [[SidebarMenu.props]] — 34 props across 6 exports including `items` (SidebarItemProps[]), `initialCollapsedState`, `linkComponent`
- [[SidebarMenu.anatomy]] — 11 elements across 2 component sets; expanded/collapsed variants; 5 sub-item states (Rest, Hover, Selected, Focus, Disabled)
- [[SidebarMenu.tokens]] — 7 tokens: 4 semantic (ui25, hover12, active12, hover13), 3 Figma primitive (label text, muted text, badge fill)
- [[SidebarMenu.usage]] — 6 Do/Don't pairs covering default collapse state, badge dot vs count, badge accessibility, footer slot, active state, collapse toggle labels
- [[SidebarMenu.accessibility]] — keyboard (Tab, Shift+Tab, Enter/Space), ARIA (nav landmark, listitem, aria-current, badgeAriaLabel), focus; 8 WCAG 2.1 AA criteria
- [[SidebarMenu.platform]] — no PUI requirements
- [[SidebarMenu.composition]] — subcomponents MenuItem, SubMenuItem, MenuList, SidebarContainer, CollapseItem; 3 patterns: config-driven, declarative, router integration
