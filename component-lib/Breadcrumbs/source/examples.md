---
component: Breadcrumbs
package: "@8x8/oxygen-breadcrumbs"
category: navigation
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Breadcrumbs/props]]"
  - "[[Breadcrumbs/tokens]]"
  - "[[Breadcrumbs/accessibility]]"
  - "[[Breadcrumbs/Breadcrumbs-figma]]"
  - "[[Breadcrumbs/Breadcrumbs-usage]]"
  - "[[Breadcrumbs/Breadcrumbs-pui]]"
  - "[[Breadcrumbs/Breadcrumbs-audit]]"
tags:
  - oxygen
  - component/Breadcrumbs
  - role/examples
  - stage/spec_ready
  - category/navigation
---
# Breadcrumbs — Examples

> **See also:** [props.md](props.md) | [tokens.md](tokens.md) | [accessibility.md](accessibility.md) | [Breadcrumbs-figma.md](Breadcrumbs-figma.md) | [Breadcrumbs-usage.md](Breadcrumbs-usage.md)

## Basic usage

```jsx
import { Breadcrumbs, Breadcrumb } from '@8x8/oxygen-breadcrumbs';

<Breadcrumbs>
  <Breadcrumb href="/">Home</Breadcrumb>
  <Breadcrumb href="/products">Products</Breadcrumb>
  <Breadcrumb href="/products/widgets">Widgets</Breadcrumb>
  <Breadcrumb isActive>Current Page</Breadcrumb>
</Breadcrumbs>
```

The last item should use `isActive` — it renders as plain text, not a link, and represents the user's current location.

## Custom separator

```jsx
<Breadcrumbs separator=">">
  <Breadcrumb href="/">Home</Breadcrumb>
  <Breadcrumb href="/products">Products</Breadcrumb>
  <Breadcrumb isActive>Current Page</Breadcrumb>
</Breadcrumbs>
```

The `separator` prop accepts any `React.ReactNode` — a string, an icon component, or any element.

## Collapsed overflow (many items)

```jsx
<Breadcrumbs
  maxItems={4}
  itemsBeforeCollapse={1}
  itemsAfterCollapse={2}
>
  <Breadcrumb href="/">Home</Breadcrumb>
  <Breadcrumb href="/a">Level A</Breadcrumb>
  <Breadcrumb href="/a/b">Level B</Breadcrumb>
  <Breadcrumb href="/a/b/c">Level C</Breadcrumb>
  <Breadcrumb href="/a/b/c/d">Level D</Breadcrumb>
  <Breadcrumb isActive>Current Page</Breadcrumb>
</Breadcrumbs>
```

When the number of `Breadcrumb` children exceeds `maxItems`, the component auto-collapses and shows an ellipsis (`…`). `itemsBeforeCollapse` and `itemsAfterCollapse` control how many items remain visible on each side. Clicking the ellipsis expands the full trail.

## Custom collapsed button label

```jsx
<Breadcrumbs collapsedTitle="Expand navigation">
  <Breadcrumb href="/">Home</Breadcrumb>
  <Breadcrumb href="/a">Section A</Breadcrumb>
  <Breadcrumb href="/a/b">Section B</Breadcrumb>
  <Breadcrumb href="/a/b/c">Section C</Breadcrumb>
  <Breadcrumb href="/a/b/c/d">Section D</Breadcrumb>
  <Breadcrumb isActive>Current Page</Breadcrumb>
</Breadcrumbs>
```

`collapsedTitle` sets the accessible title on the ellipsis button. Override the default `'Show all links'` to localise or provide more context.

> **Note:** `get-component-examples` returned 0 clean snippets. The examples above are derived from the storybook documentation story and documented behaviour. Verify against the live Storybook before using in production.

_Source: Oxygen MCP · Extracted 2026-04-30_
