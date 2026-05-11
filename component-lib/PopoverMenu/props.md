---
component: PopoverMenu
package: "@8x8/oxygen-popover"
category: overlays_contextual
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - figma
  - usage
  - audit
siblings:
  - "[[PopoverMenu/examples]]"
  - "[[PopoverMenu/tokens]]"
  - "[[PopoverMenu/accessibility]]"
  - "[[PopoverMenu/PopoverMenu-figma]]"
  - "[[PopoverMenu/PopoverMenu-usage]]"
  - "[[PopoverMenu/PopoverMenu-audit]]"
tags:
  - oxygen
  - component/PopoverMenu
  - role/props
  - stage/blocked
  - category/overlays_contextual
---

# PopoverMenu — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```bash
# Package name not returned by MCP — use the @8x8/oxygen-popover package
yarn add @8x8/oxygen-popover
# or
npm install @8x8/oxygen-popover
```

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
| `activeProp` | `string` | no | _(no description returned by MCP)_ |
| `disabledProp` | `string` | no | _(no description returned by MCP)_ |
| `isDisabled` | `boolean` | no | Whether the component is disabled |
| `placement` | `Placement` | no | Preferred placement of the floating panel relative to the trigger |
| `portalTargetRef` | `React.RefObject<HTMLElement>` | no | Custom portal container for the floating content |
| `maxHeight` | `number` | no | Maximum height of the floating panel in pixels |
| `testId` | `string` | no | `data-testid` value for automated testing |

> **Data gaps:** `activeProp`, `disabledProp`, `placement`, `portalTargetRef`, `maxHeight`, and `floatingContent` have no descriptions in the MCP source.

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
| `activeProp` | `string` | no | _(no description returned by MCP)_ |
| `disabledProp` | `string` | no | _(no description returned by MCP)_ |
| `isDisabled` | `boolean` | no | Whether the component is disabled |
| `placement` | `Placement` | no | Preferred placement of the floating panel |
| `portalTargetRef` | `React.RefObject<HTMLElement>` | no | Custom portal container |
| `maxHeight` | `number` | no | Maximum height of the floating panel in pixels |
| `header` | `ReactNode` | no | Optional content rendered above the item list |
| `footer` | `ReactNode` | no | Optional content rendered below the item list |
| `onMenuOpenToggle` | `(isOpen: boolean) => void` | no | Fires when the menu opens or closes |
| `onMenuItemClick` | `(event: React.MouseEvent<Element> \| React.KeyboardEvent<Element>) => void` | no | Fires when a menu item is clicked or activated via keyboard |
| `onUpdate` | `(arg0: ListItemWrapperProps, arg1: number) => void` | no | Fires when an item's state is updated |
| `onCancel` | `() => void` | no | Fires when the menu is dismissed without selection |
| `testId` | `string` | no | `data-testid` value for automated testing |

---

## Sub-components

The `popover` package also registers `Divider`, `SectionHeader`, and `ListItem` as related components in the search index, but their individual props are not accessible via the MCP (`SOURCE_GAP`). These are likely used internally within the menu list structure or composable within the `items` array.

---

_Source: Oxygen MCP · Extracted 2026-05-08_
