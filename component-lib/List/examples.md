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

---

> **Note:** The Oxygen MCP returned 0 clean standalone story examples for this package. The examples above are derived from the documentation story (Storybook `ListDocumentation`) and prop-driven compositions. Additional patterns may be visible in the Figma design — see [`List-figma.md`](List-figma.md).

_Source: Oxygen MCP · Extracted 2026-05-08_
