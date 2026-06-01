---
parent: "[[Breadcrumbs]]"
section: composition
---

## Subcomponents

| Subcomponent | Role |
|--------------|------|
| `Breadcrumb` | Child item. One per trail level. Passed as `children` of `Breadcrumbs`. Inherits native `<a>` props; mark the last item `isActive` to render it as the non-link current page. See [[Breadcrumbs.props]]. |

A `Breadcrumbs` trail is composed by nesting `Breadcrumb` children:

```jsx
<Breadcrumbs>
  <Breadcrumb href="/">Home</Breadcrumb>
  <Breadcrumb href="/products">Products</Breadcrumb>
  <Breadcrumb isActive>Current Page</Breadcrumb>
</Breadcrumbs>
```

## Slots

| Slot | Accepts | Notes |
|------|---------|-------|
| `separator` prop | any `React.ReactNode` | Replaces the default `/` glyph between items (string, icon, or element). |
| Overflow Menu content | placeholder `Slot` (Figma) | Dropdown shown when the trail collapses and the ellipsis is opened. Design intent unconfirmed — see WARN-003 in [[Breadcrumbs.anatomy]]. |

## Patterns

Breadcrumbs are a **secondary** navigation pattern — they complement, never replace, primary navigation. Common in page-header layouts above the page title for deep hierarchical sites. See [[Breadcrumbs.usage]] for placement and when-to-use guidance.

_Source: [[Breadcrumbs/Breadcrumbs-figma]] · [[Breadcrumbs/examples]] · Extracted 2026-04-30_
