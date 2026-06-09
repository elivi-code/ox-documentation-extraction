---
component: PopoverMenu
parent: "[[PopoverMenu]]"
section: props
pipeline_stage: draft
audit_verdict: "NO"
siblings:
  - "[[PopoverMenu]]"
  - "[[PopoverMenu.anatomy]]"
  - "[[PopoverMenu.tokens]]"
  - "[[PopoverMenu.usage]]"
  - "[[PopoverMenu.accessibility]]"
  - "[[PopoverMenu.platform]]"
  - "[[PopoverMenu.composition]]"
tags:
  - oxygen
  - component/PopoverMenu
  - role/props
  - stage/draft
  - category/overlays_contextual
---

## Installation

```bash
yarn add @8x8/oxygen-popover
# or
npm install @8x8/oxygen-popover
```

<!-- SKIP:GAP-015 manual="Package version not available from MCP or local source; retrieve from npm registry before publishing" -->

## Overview

The `@8x8/oxygen-popover` package exports two distinct components:

| Component | Role |
|---|---|
| `Popover` | Low-level primitive — fully controlled open state; accepts any `floatingContent` |
| `PopoverMenu` | High-level menu wrapper — manages open state internally; renders a structured list via `items` |

Use `PopoverMenu` for standard dropdown menus. Use `Popover` when you need full control over the floating panel content.

---

## Popover

```tsx
import { Popover } from '@8x8/oxygen-popover';
```

### Props

| Prop | Type | Required | Description |
|---|---|---|---|
| `children` | `React.ReactElement` | yes | Trigger element that anchors the popover |
| `floatingContent` | `ReactNode` | yes | Content rendered inside the floating panel |
| `isOpen` | `boolean` | yes | Whether the popover is open |
| `setIsOpen` | `(isOpen: boolean) => void` | yes | Callback to update open state |
| `activeProp` | `string` | no | Name of the prop on the child element used to set active state |
| `disabledProp` | `string` | no | Name of the prop on the child element used to set disabled state |
| `isDisabled` | `boolean` | no | Whether the component is disabled |
| `placement` | `Placement` | no | Preferred placement of the floating panel relative to the trigger |
| `portalTargetRef` | `React.RefObject<HTMLElement>` | no | Custom portal container for the floating content |
| `maxHeight` | `number` | no | Maximum height of the floating panel in pixels |
| `testId` | `string` | no | `data-testid` value for automated testing |

> **Placement type:** `'top' | 'top-start' | 'top-end' | 'bottom' | 'bottom-start' | 'bottom-end' | 'left' | 'left-start' | 'left-end' | 'right' | 'right-start' | 'right-end'` (standard floating-ui placement values — verify against implementation)

> **Source note:** Descriptions for `activeProp`, `disabledProp`, `placement`, `portalTargetRef`, `maxHeight`, and `floatingContent` are inferred — not MCP-sourced.

---

## PopoverMenu

```tsx
import { PopoverMenu } from '@8x8/oxygen-popover';
```

### Props

Inherits all base props from `Popover` **except** `floatingContent`, `isOpen`, and `setIsOpen` — those are replaced by the `items`-driven API and internal open-state management.

| Prop | Type | Required | Description |
|---|---|---|---|
| `children` | `React.ReactElement` | yes | Trigger element (typically a `DropdownButton`) |
| `items` | `(ListItemWrapperProps \| (ReactNode \| ListItemWrapperProps[]))[]` | yes | Array of menu items or grouped item arrays |
| `activeProp` | `string` | no | Name of the prop on the child element used to set active state |
| `disabledProp` | `string` | no | Name of the prop on the child element used to set disabled state |
| `isDisabled` | `boolean` | no | Whether the component is disabled |
| `placement` | `Placement` | no | Preferred placement of the floating panel relative to the trigger |
| `portalTargetRef` | `React.RefObject<HTMLElement>` | no | Custom portal container |
| `maxHeight` | `number` | no | Maximum height of the floating panel in pixels |
| `header` | `ReactNode` | no | Optional content rendered above the item list |
| `footer` | `ReactNode` | no | Optional content rendered below the item list |
| `onMenuOpenToggle` | `(isOpen: boolean) => void` | no | Fires when the menu opens or closes |
| `onMenuItemClick` | `(event: React.MouseEvent<Element> \| React.KeyboardEvent<Element>) => void` | no | Fires when a menu item is clicked or activated via keyboard |
| `onUpdate` | `(arg0: ListItemWrapperProps, arg1: number) => void` | no | Fires when an item's state is updated |
| `onCancel` | `() => void` | no | Fires when the menu is dismissed without selection |
| `testId` | `string` | no | `data-testid` value for automated testing |

> **WARN-001:** `onUpdate` callback's second argument (`arg1: number`) has no description — semantics (index? count?) unclear. Clarify before publishing.

---

## Sub-components

The `popover` package also registers `Divider`, `SectionHeader`, and `ListItem` as related components in the search index, but their individual props are not accessible via the MCP.

<!-- STUB:GAP-004 source="Request Oxygen MCP team to register Divider, SectionHeader, and ListItemWrapperProps props for the popover package" -->

---

_Source: Oxygen MCP · Extracted 2026-05-08 · GAP-013, GAP-014 applied by doc-rewrite_
