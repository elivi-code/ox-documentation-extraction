---
component: List
status: draft
category: data_display
figma: "https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=47175-1414"
variants:
  - Single Action or Select
  - Destructive
  - Checkbox
  - Radio
  - Add Item
  - Sub Menu
  - Collapsible
  - Remove Item
props:
  - children: ReactNode
  - isGroup: boolean
  - isOrdered: boolean
  - withBackground: boolean
  - theme: ListTheme
  - title: string
  - isDisabled: boolean
  - isActive: boolean
  - shouldWrapText: boolean
  - onClick: function
subcomponents:
  - "[[Icon]]"
  - "[[Avatar]]"
related: []
patterns: []
tokens:
  - "[[token.ui.ui06]]"
  - "[[token.ui.ui02]]"
  - "[[token.ui.ui01]]"
  - "[[token.text.textColor01]]"
  - "[[token.text.textColor02]]"
  - "[[token.icon.icon01]]"
  - "[[token.bulletList01]]"
spokes:
  - "[[List.props]]"
  - "[[List.anatomy]]"
  - "[[List.tokens]]"
  - "[[List.usage]]"
  - "[[List.accessibility]]"
  - "[[List.platform]]"
  - "[[List.composition]]"
tags:
  - component
  - data_display
  - interactive
---

## Overview

`List` and `ListItem` (`@8x8/oxygen-list`) render semantic `<ul>`/`<ol>` structures with eight visual `ListItem` variant types: Single Action or Select, Destructive, Checkbox, Radio, Add Item, Sub Menu, Collapsible, and Remove Item. Selection state is communicated by trailing icon visibility only — no background colour change occurs for `selected?=true`. The `isActive` prop marks the current item; `isDisabled` prevents interaction.

## Spokes

- [[List.props]] — 11 props across `List` (5: children, isGroup, isOrdered, withBackground, theme) and `ListItem` (6: children, title, isDisabled, isActive, shouldWrapText, onClick)
- [[List.anatomy]] — 8 Figma variant types across 5 states (hover, active, focus, disabled, selected); 40 px standard height, 108 px Collapsible open; swappable leading visual (Icon/Avatar/Status)
- [[List.tokens]] — 7 tokens covering background (ui01/ui02/ui06), text (textColor01/textColor02), icon (icon01), typography (bulletList01); 1 CONFLICT on ui01 description requires human resolution
- [[List.usage]] — no Do/Don't guidance available (no Figma examples page exists for List)
- [[List.accessibility]] — keyboard (Tab, Enter/Space), ARIA (ul/ol/li semantics), focus; all content inferred — verify isActive/isDisabled ARIA attributes against DOM
- [[List.platform]] — no PUI requirements
- [[List.composition]] — swappable leading visual slot (Icon/Avatar/Status); 8 Figma variant patterns; code-level composition approach unconfirmed
