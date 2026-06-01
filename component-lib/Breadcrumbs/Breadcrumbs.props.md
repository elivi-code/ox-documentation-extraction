---
parent: "[[Breadcrumbs]]"
section: props
---

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

<!-- STUB:GAP-009 source="Inspect @8x8/oxygen-breadcrumbs TypeScript types or source for the BreadcrumbsTheme interface shape; document the theme prop structure (property names, token references, accepted value types) in props.md." -->
> **`theme` prop shape unresolved (GAP-009):** The `theme` prop type is documented only as `object`. Its internal shape (property names, token references, accepted value types) was not returned by the Oxygen MCP and is not documented in any extracted source.

## `Breadcrumb` Props

`Breadcrumb` inherits all props from the native `<a>` element (`href`, `title`, `target`, `onClick`, etc.).

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `isActive` | `boolean` | `false` | — | Marks the item as the current (active) page. Inferred from storybook usage; active items are not rendered as links. |
| `href` | `string` | — | — | Destination URL (native `<a>` prop). |
| `target` | `string` | — | — | Link target (native `<a>` prop). |
| `onClick` | `MouseEventHandler` | — | — | Click handler (native `<a>` prop). |

<!-- SKIP:GAP-008 type=DOC_GAP manual="Verify isActive prop existence, type, default, and behaviour against @8x8/oxygen-breadcrumbs source or published TypeScript types; update props.md." -->
> **`isActive` unverified (GAP-008):** This prop was observed in the storybook example code but was **not** returned by `get-component-props`. Its type (`boolean`), default (`false`), and behaviour (renders as plain text, not a link) are inferred — treat the exact signature as unverified until confirmed against source.

_Source: [[Breadcrumbs/props]] · Oxygen MCP · Extracted 2026-04-30_
