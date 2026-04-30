# Breadcrumbs — Props

> **See also:** [examples.md](examples.md) | [tokens.md](tokens.md) | [accessibility.md](accessibility.md)

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-breadcrumbs

# npm
$ npm install @8x8/oxygen-breadcrumbs
```

> **Registry note:** Add `@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/` to `.npmrc` and connect to 8x8 VPN before installing.

## `Breadcrumbs` Props

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `React.ReactNode` | — | ✓ | Breadcrumb items. Use `Breadcrumb` components as children. |
| `maxItems` | `number` | `4` | — | Maximum number of breadcrumbs to display. When exceeded, items will be collapsed. |
| `itemsBeforeCollapse` | `number` | `1` | — | Number of items to show before the ellipsis when collapsed. |
| `itemsAfterCollapse` | `number` | `1` | — | Number of items to show after the ellipsis when collapsed. |
| `separator` | `React.ReactNode` | `'/'` | — | Text or element to display between breadcrumb items. |
| `ariaLabel` | `string` | `'Breadcrumbs'` | — | Aria label for the breadcrumbs navigation element. |
| `collapsedTitle` | `string` | `'Show all links'` | — | Title text shown on the collapsed items button. |
| `theme` | `object` | — | — | Breadcrumb theme object. |

## `Breadcrumb` Props

`Breadcrumb` inherits all props from the native `<a>` element (`href`, `title`, `target`, `onClick`, etc.).

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `isActive` | `boolean` | `false` | — | Marks the item as the current (active) page. Inferred from storybook usage; active items are not rendered as links. |
| `href` | `string` | — | — | Destination URL (native `<a>` prop). |
| `target` | `string` | — | — | Link target (native `<a>` prop). |
| `onClick` | `MouseEventHandler` | — | — | Click handler (native `<a>` prop). |

> **Note on `isActive`:** This prop was observed in the storybook example code but was not returned by `get-component-props`. Treat its exact signature as unverified.

_Source: Oxygen MCP · Extracted 2026-04-30_
