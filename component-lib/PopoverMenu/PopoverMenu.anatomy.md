---
component: PopoverMenu
parent: "[[PopoverMenu]]"
section: anatomy
pipeline_stage: draft
audit_verdict: "NO"
siblings:
  - "[[PopoverMenu]]"
  - "[[PopoverMenu.props]]"
  - "[[PopoverMenu.tokens]]"
  - "[[PopoverMenu.usage]]"
  - "[[PopoverMenu.accessibility]]"
  - "[[PopoverMenu.platform]]"
  - "[[PopoverMenu.composition]]"
tags:
  - oxygen
  - component/PopoverMenu
  - role/anatomy
  - stage/draft
  - category/overlays_contextual
---

## Visual reference

<!-- STUB:GAP-008 source="Re-run figma-extract for PopoverMenu with Desktop Bridge connected to save figma-screenshot-PopoverMenu.png" -->

Figma file: [Design context](https://figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=47175:1414)

---

## Anatomy

The Figma canvas (node `47175:1414`) contains two distinct structural layers:

1. **Popover window** — the floating panel shell (node `48432:43576`)
2. **List item variants** — the menu item components that populate the panel's `Slot`

### Popover window

The container shell with configurable header, scrollable content area, and footer.

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | `_header` | optional slot | Shown when `header=true`; contains title row + search input + bottom divider |
| 1a | frame | `Title` | structural | Flex row; holds title text node + close icon button |
| 1b | frame | `Input` | content | Search text field (label: "Search placeholder") |
| 1c | frame | `Dividers` | structural/decorative | 1px divider line separating header from content |
| 2 | frame | `Content` | fixed sub-component | Always present; wraps the Slot and optional Scrollbar |
| 2a | instance | `Slot` | content element (instance swap) | Placeholder — intended to be swapped with actual list content |
| 2b | frame | `Scrollbar_Mac OS` | optional slot | Shown when `scroll=true`; 12px wide Mac-style scrollbar |
| 3 | frame | `_footer` | optional slot | Shown when `footer=true`; contains top divider + Clear/Cancel/Apply buttons |
| 3a | frame | `Dividers` | structural/decorative | 1px divider line separating content from footer |
| 3b | frame | `Buttons` | structural | Flex row; holds Clear (label button), Cancel (label button), Apply (filled button) |

### Sub-component: List item types

Eight list item variants are defined on the canvas. Each is 296 × 40px (except Collapsible in open state: 296 × 108px).

| # | Type | Name | States | Selection variants |
|---|------|------|--------|--------------------|
| 1 | frame | `List item/Single Action or Select` | rest, hover, active, focus, disabled | true, false |
| 2 | frame | `List item/Destructive` | rest, hover, active, focus, disabled | — |
| 3 | frame | `List item/Checkbox` | rest, hover, active, focus, disabled | true, false, indeterminate |
| 4 | frame | `List item/Radio` | rest, hover, active, focus, disabled | true, false |
| 5 | frame | `List item/Add Item` | rest, hover, active, focus, disabled | — |
| 6 | frame | `List item/Sub Menu` | rest, hover, active, focus, disabled | — |
| 7 | frame | `List item/Collapsible` | rest, hover, active, focus, disabled | open: yes/no |
| 8 | frame | `List item/Remove Item` | rest, hover, active, focus, disabled | — |

### Sub-component: Section header and divider

| # | Type | Name | Variants |
|---|------|------|----------|
| 1 | frame | `Section header and divider/Section header` | type: subtle, bold × mode: light, dark; 312 × 32px |
| 2 | frame | `Section header and divider/Divider` | mode: light, dark; 312 × 9px |

### Sub-component: Empty state and spinner

| # | Type | Name | Notes |
|---|------|------|-------|
| 1 | frame | `Empty state and spinner/Spinner` | 312 × 100px; loading state placeholder |
| 2 | frame | `Empty state and spinner/Empty state` | 312 × 138px; no-results placeholder |

### Atoms

| # | Type | Name | Notes |
|---|------|------|-------|
| 1 | frame | `Options` | Leading visuals (Avatar, Icon, Status) and trailing visuals (Sub Menu, Remove, Add, selection indicators) |
| 2 | frame | `_footer` | Footer atoms: default (buttons) and custom slot types |
| 3 | frame | `_header` | Header atoms: title type and custom slot types |

---

## Component properties

### Variant axes (Popover window — node `48432:43576`)

| Property | Values | Default |
|----------|--------|---------|
| `mode` | `light`, `dark` | `light` |
| `footer` | `true`, `false` | `false` |
| `header` | `true`, `false` | `false` |
| `scroll` | `true`, `false` | `false` |

### Boolean toggles

| Property | Default | Notes |
|----------|---------|-------|
| `header` | false | Shows/hides the `_header` slot (title + search + divider) |
| `footer` | false | Shows/hides the `_footer` slot (divider + Clear/Cancel/Apply buttons) |
| `scroll` | false | Shows/hides the `Scrollbar_Mac OS` inside Content |

### Instance swap slots

| Slot | Accepted types | Default |
|------|---------------|---------|
| `Slot` (inside Content) | Any content — intended for list items, empty state, spinner | Placeholder frame |

<!-- STUB:GAP-009 source="Component not published to Figma library; no variant key map available from figma_get_component_details. Note as known limitation unless Oxygen team publishes the component." -->

---

## Structure & spacing

### Container

| Property | Token | Value | Notes |
|----------|-------|-------|-------|
| Width | — | `320px` | Hardcoded |
| Max width | — | `1064px` | Hardcoded |
| Max height | — | `400px` | Hardcoded |
| Border radius | — | `6px` | Hardcoded |
| Padding horizontal | — | `1px` | Hardcoded |
| Padding vertical | — | `9px` | Hardcoded |
| Overflow | — | `clip` | Hardcoded |

### Internal spacing

| Element | Property | Token | Value | Notes |
|---------|----------|-------|-------|-------|
| Header title row | padding | — | `4px 12px 8px 12px` | Hardcoded |
| Header search input | padding | — | `4px 12px 12px 12px` | Hardcoded |
| Footer buttons (light) | padding | — | `8px 8px 0 8px` | Hardcoded |
| Footer buttons (dark) | padding | — | `8px 12px 0 12px` | ⚠️ Inconsistent with light |
| Gap (footer buttons group) | gap | — | `16px` | Hardcoded |
| Gap (footer button internal) | gap | — | `8px` | Hardcoded |
| Footer button padding | — | — | `8px 12px` | Hardcoded |
| Scrollbar width | — | — | `12px` | Hardcoded |

### Auto-layout

- **Container**: `flex-col`, vertical stack
- **Header**: `flex-col`, vertical stack (title → search → divider)
- **Footer buttons row**: `flex-row`, `justify-end`, `items-center`, `gap-16px`
- **List items**: `296px` wide, `40px` tall (standard); `108px` tall (Collapsible open)

---

## Interaction states

States from list item variant names on the canvas:

| State | Trigger | Notes |
|-------|---------|-------|
| `rest` | Default | Normal resting state |
| `hover` | Pointer over list item | Background tint change |
| `active` | Pointer down / pressed | Pressed visual feedback |
| `focus` | Keyboard navigation (Tab/Arrow) | Focus ring applied |
| `disabled` | `isDisabled=true` on item | Non-interactive; reduced opacity |

---

## Design decisions

> **Popover window (Stable):** Status is Stable. Refer to [How to use slots in Figma](https://oxygen.8x8.com/blog/how-to-use-slots-in-figma) for guidance on swapping the `Slot` placeholder with actual content.

> **Slot:** "This is a placeholder component. Swap me with your custom content by using the component instance swapper."

---

_Source: Figma MCP · figma-console MCP · Extracted 2026-05-08_
