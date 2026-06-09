---
component: List
package: "@8x8/oxygen-list"
category: data_display
role: examples
role_description: "Code usage examples from basic to advanced patterns"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
siblings:
  - "[[List/props]]"
  - "[[List/tokens]]"
  - "[[List/accessibility]]"
  - "[[List/List-figma]]"
  - "[[List/List-pui]]"
  - "[[List/List-audit]]"
tags:
  - oxygen
  - component/List
  - role/examples
  - stage/blocked
  - category/data_display
---

# List — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Basic list

```tsx
import { List, ListItem } from '@8x8/oxygen-list';

<List>
  <ListItem>Item 1</ListItem>
  <ListItem>Item 2</ListItem>
  <ListItem isDisabled>Item 3 - is disabled</ListItem>
  <ListItem isActive>Item 4 - is active</ListItem>
</List>
```

## Ordered list

```tsx
<List isOrdered>
  <ListItem>First</ListItem>
  <ListItem>Second</ListItem>
  <ListItem>Third</ListItem>
</List>
```

## Group list

```tsx
<List isGroup>
  <ListItem>Group item A</ListItem>
  <ListItem>Group item B</ListItem>
  <ListItem>Group item C</ListItem>
</List>
```

## List with background

```tsx
<List withBackground>
  <ListItem>Item with background</ListItem>
  <ListItem isActive>Active item with background</ListItem>
</List>
```

## Clickable items

```tsx
<List>
  <ListItem onClick={(e) => console.log('clicked', e)}>Clickable item</ListItem>
  <ListItem onClick={(e) => console.log('clicked', e)} isDisabled>
    Disabled clickable item
  </ListItem>
</List>
```

## Single-line text truncation

Use `shouldWrapText={false}` to clip item text to one line: <!-- GAP-013 applied -->

```tsx
<List>
  <ListItem shouldWrapText={false}>
    This very long item label will be clipped to a single line rather than wrapping
  </ListItem>
</List>
```

## Theme override

The `theme` prop is provided by the Oxygen theme provider via `@8x8/oxygen-config` and `@8x8/oxygen-constants`. Override only when using `List` outside a standard Oxygen setup:

```tsx
import { List, ListItem } from '@8x8/oxygen-list';
import { buildListTheme } from '@8x8/oxygen-config';

<List theme={buildListTheme({ /* custom token overrides */ })}>
  <ListItem>Custom-themed item</ListItem>
</List>
```

---

> **Note:** The Oxygen MCP returned 0 clean standalone story examples for this package. The examples above are derived from the documentation story (Storybook `ListDocumentation`) and prop-driven compositions. Additional patterns may be visible in the Figma design — see [`List-figma.md`](List-figma.md).

_Source: Oxygen MCP · Extracted 2026-05-08_
