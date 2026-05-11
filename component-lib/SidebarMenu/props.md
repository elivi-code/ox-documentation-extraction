---
component: SidebarMenu
package: "@8x8/oxygen-sidebarMenu"
category: navigation
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
  - audit
siblings:
  - "[[SidebarMenu/examples]]"
  - "[[SidebarMenu/tokens]]"
  - "[[SidebarMenu/accessibility]]"
  - "[[SidebarMenu/SidebarMenu-figma]]"
  - "[[SidebarMenu/SidebarMenu-audit]]"
tags:
  - oxygen
  - component/SidebarMenu
  - role/props
  - stage/blocked
  - category/navigation
---

# SidebarMenu — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```bash
# yarn
$ yarn add @8x8/oxygen-sidebar-menu

# npm
$ npm install @8x8/oxygen-sidebar-menu
```

**Registry prerequisite** — configure `.npmrc` or `.yarnrc.yml` to point `@8x8` scoped packages at the 8x8 Artifactory registry (VPN required):

```
# .npmrc
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```

---

## Package overview

`@8x8/oxygen-sidebar-menu` exports a suite of composable components for building collapsible application sidebars:

| Export | Role |
|---|---|
| `Sidebar` | High-level config-driven entry point. Manages collapse state internally. |
| `SidebarContainer` | Low-level shell used by the declarative approach. Accepts `collapsed` + `position`. |
| `SidebarProvider` | Context provider for sidebar state (used internally). |
| `MenuList` | `<ul>` container for `MenuItem` children; accepts a `footer` flag. |
| `Ul` | Base unstyled list primitive used internally. |
| `MenuItem` | Top-level navigation item with icon, label, badge, and optional sub-items. |
| `SubMenuItem` | Secondary navigation item nested inside a `MenuItem`. |
| `CollapseItem` | Toggle button that collapses/expands the sidebar. |

---

## `Sidebar` props

The config-driven component; preferred for most use cases.

| Prop | Type | Required | Default | Description |
|---|---|---|---|---|
| `items` | `SidebarItemProps[]` | ✓ | — | Full item config array (see `SidebarItemProps` below). |
| `position` | `"left" \| "right"` | | `"left"` | Which side the sidebar is mounted on. |
| `initialCollapsedState` | `boolean` | | `false` | Whether the sidebar starts collapsed. |
| `collapseLabel` | `string` | | — | Label shown on the collapse toggle button when expanded. |
| `expandLabel` | `string` | | — | Label shown on the collapse toggle button when collapsed. |
| `onCollapseChange` | `(collapsed: boolean) => void` | | — | Called when the sidebar collapse state changes. |
| `linkComponent` | `ComponentType<any>` | | — | Custom router link component (e.g. React Router `<Link>`). |
| `linkProp` | `string` | | — | Prop name used to pass the URL to `linkComponent` (e.g. `"to"`). |
| `testId` | `string` | | — | Data attribute for automated testing. |

### `SidebarItemProps` shape

```ts
interface SidebarItemProps {
  label: string;
  icon?: ReactNode;
  link?: string;
  isActive?: boolean;
  isFooter?: boolean;
  hasBadge?: boolean;
  badgeChildren?: ReactNode;
  badgeAriaLabel?: string;
  onTrigger?: (event: MouseEvent<HTMLElement>) => void;
  subItems?: SubItemProps[];
}
```

---

## `MenuItem` props

Used in the declarative (low-level) composition pattern inside `SidebarContainer`.

| Prop | Type | Required | Default | Description |
|---|---|---|---|---|
| `label` | `string` | ✓ | — | Visible text label for the item. |
| `icon` | `ReactNode` | | — | Icon displayed to the left of the label (not formally typed in MCP; observed in examples). |
| `isActive` | `boolean` | | `false` | Marks the item as the currently active route. |
| `onTrigger` | `(event: MouseEvent<HTMLElement>) => void` | | — | Click handler. |
| `link` | `string` | | — | URL associated with the item. |
| `position` | `"left" \| "right"` | | — | Inherited from `SidebarPosition`. |
| `hasBadge` | `boolean` | | `false` | Shows a badge indicator on the item. |
| `badgeChildren` | `ReactNode` | | — | Content inside the badge (e.g. `"99+"`). |
| `badgeAriaLabel` | `string` | | — | Accessible label for the badge. |
| `linkComponent` | `ComponentType<any>` | | — | Custom router link component. |
| `linkProp` | `string` | | — | Prop name for the URL on `linkComponent`. |
| `testId` | `string` | | — | Data attribute for automated testing. |
| `children` | `ReactNode` | | — | `SubMenuItem` children (not formally typed; shown in examples). |

---

## `SubMenuItem` props

Nested inside a `MenuItem`. Props not individually published by the MCP — the following are observed from examples and the `SidebarItemProps` shape:

| Prop | Type | Required | Description |
|---|---|---|---|
| `label` | `string` | ✓ | Visible text label. |
| `isActive` | `boolean` | | Marks the sub-item as active. |
| `onTrigger` | `(event: MouseEvent<HTMLElement>) => void` | | Click handler. |
| `hasBadge` | `boolean` | | Shows badge indicator. |
| `badgeChildren` | `ReactNode` | | Content inside the badge. |
| `badgeAriaLabel` | `string` | | Accessible label for the badge. |
| `aria-label` | `string` | | Additional accessible label (seen in examples). |

---

## `CollapseItem` props

Props not individually published by the MCP — observed from examples:

| Prop | Type | Description |
|---|---|---|
| `label` | `string` | Text shown in the collapse toggle (switches between `collapseLabel`/`expandLabel`). |

---

## `SidebarContainer` props

Props not individually published by the MCP — observed from examples:

| Prop | Type | Description |
|---|---|---|
| `collapsed` | `boolean` | Drives the collapsed visual state. |
| `position` | `"left" \| "right"` | Which side the container is mounted on. |

---

## `MenuList` props

| Prop | Type | Description |
|---|---|---|
| `footer` | `boolean` | When `true`, renders the list in the sidebar footer slot. |

_Source: Oxygen MCP · Extracted 2026-05-07_
