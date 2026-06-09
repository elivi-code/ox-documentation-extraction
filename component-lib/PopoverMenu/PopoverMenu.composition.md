---
component: PopoverMenu
parent: "[[PopoverMenu]]"
section: composition
pipeline_stage: draft
audit_verdict: "NO"
siblings:
  - "[[PopoverMenu]]"
  - "[[PopoverMenu.props]]"
  - "[[PopoverMenu.anatomy]]"
  - "[[PopoverMenu.tokens]]"
  - "[[PopoverMenu.usage]]"
  - "[[PopoverMenu.accessibility]]"
  - "[[PopoverMenu.platform]]"
tags:
  - oxygen
  - component/PopoverMenu
  - role/composition
  - stage/draft
  - category/overlays_contextual
---

## Sub-components

`PopoverMenu` is composed from sub-components defined in the Figma canvas. These are rendered within the `items` array and the panel's `Slot`:

| Sub-component | Type | Composable via `items`? | Notes |
|---|---|---|---|
| `[[Divider]]` | Section separator | Yes (likely via sentinel) | `Section header and divider/Divider`; 312 × 9px; light + dark variants |
| `[[SectionHeader]]` | Group label | Yes (likely via sentinel) | `Section header and divider/Section header`; subtle + bold variants |
| `[[ListItem]]` | Menu item | Yes (via `ListItemWrapperProps`) | 8 variants — see anatomy |

> **SOURCE_GAP (GAP-004):** `Divider`, `SectionHeader`, and `ListItem` props are not registered in the Oxygen MCP. `ListItemWrapperProps` — the type used in `PopoverMenu.items` — is undocumented. The `items` array shapes in examples are illustrative until the MCP surfaces them. See `PopoverMenu.props.md`.

### List item variant matrix

| Variant | Figma name | Selection model | Typical use |
|---|---|---|---|
| Single Action | `List item/Single Action or Select` | None / single | Commands: "Edit", "Duplicate", "Archive" |
| Destructive | `List item/Destructive` | None | Irreversible commands: "Delete", "Sign out" |
| Checkbox | `List item/Checkbox` | Multi-select | Filter facets, tag pickers |
| Radio | `List item/Radio` | Single-select | Sort order, single-value picks |
| Add Item | `List item/Add Item` | Action | Append a new entry |
| Sub Menu | `List item/Sub Menu` | Navigation | Nested child `PopoverMenu` |
| Collapsible | `List item/Collapsible` | Group disclosure | Inline sub-group (108px tall when open) |
| Remove Item | `List item/Remove Item` | Destructive | Remove an entry from a list |

---

## Popover ↔ PopoverMenu relationship

`@8x8/oxygen-popover` exports two components that share a base:

```tsx
import { Popover, PopoverMenu } from '@8x8/oxygen-popover';
```

| | `Popover` | `PopoverMenu` |
|---|---|---|
| Open state | Fully controlled (`isOpen` / `setIsOpen`) | Managed internally |
| Content | Any `floatingContent: ReactNode` | Structured list via `items` |
| Use when | Custom floating panel content | Standard dropdown menu |

`PopoverMenu` extends `Popover` — it replaces `floatingContent`, `isOpen`, and `setIsOpen` with the `items`-driven API.

<!-- CONFLICT:GAP-001 finding="The only MCP-sourced story (Popover.documentation.stories.tsx) renders the canonical example using <Popover items={...}> but the items prop belongs exclusively to PopoverMenu. Popover uses floatingContent/isOpen/setIsOpen. Either the story has a bug (wrong component name) or there is an undocumented API alias. Import and usage snippets cannot be confirmed until this is resolved." HUMAN DECISION REQUIRED -->

> ⚠️ **API naming conflict (GAP-001):** The MCP story (`Popover.documentation.stories.tsx`) renders the example as `<Popover items={...}>` but `items` belongs to `PopoverMenu`. All examples in this documentation use `<PopoverMenu items={...}>` as the correct API. Verify the story source before using the published story as a reference.

---

## Composition with other components

| Component | Relationship | Notes |
|---|---|---|
| `[[DropdownButton]]` | Typical `children` trigger | Provides the styled trigger with dropdown affordance |
| `[[Button]]` | Alternative trigger | Any focusable element can be `children` |
| `[[Tooltip]]` | Peer | Use Tooltip for single-sentence labels; use PopoverMenu for structured lists |
| `[[Modal]]` | Peer | Use Modal for workflow-blocking decisions; use PopoverMenu for dismissible menus |
| `[[Icon]]` | Inside list items via `Options` atom | Leading/trailing visuals within list item variants |

---

## Basic usage — PopoverMenu with DropdownButton

```tsx
import { PopoverMenu } from '@8x8/oxygen-popover';
import { DropdownButton } from '@8x8/oxygen-button';

<PopoverMenu
  items={[
    { key: '1', children: 'List Label 1' },
    { key: '2', children: 'List Label 2' },
    { key: '3', children: 'List Label 3' },
  ]}
>
  <DropdownButton>Dropdown Button</DropdownButton>
</PopoverMenu>
```

## Handling menu events

```tsx
<PopoverMenu
  items={[
    { key: 'edit', children: 'Edit' },
    { key: 'duplicate', children: 'Duplicate' },
    { key: 'delete', children: 'Delete' },
  ]}
  onMenuItemClick={(event) => console.log('Item clicked', event)}
  onMenuOpenToggle={(isOpen) => console.log('Menu is now', isOpen ? 'open' : 'closed')}
  onCancel={() => console.log('Menu dismissed without selection')}
>
  <DropdownButton>Actions</DropdownButton>
</PopoverMenu>
```

## With header and footer

```tsx
<PopoverMenu
  header={<div>Header content</div>}
  footer={<div>Footer content</div>}
  items={[
    { key: '1', children: 'Option 1' },
    { key: '2', children: 'Option 2' },
  ]}
>
  <DropdownButton>Open Menu</DropdownButton>
</PopoverMenu>
```

## Low-level Popover (controlled)

For custom floating content not using the structured list API:

```tsx
import { Popover } from '@8x8/oxygen-popover';
import { useState } from 'react';

const [isOpen, setIsOpen] = useState(false);

<Popover
  isOpen={isOpen}
  setIsOpen={setIsOpen}
  floatingContent={<div>Custom floating content</div>}
>
  <button onClick={() => setIsOpen(!isOpen)}>Open</button>
</Popover>
```

> **Note (WARN-002):** A "Tooltip and Popover working together" section exists in the Figma examples page (frame 88806:12915) but was not extracted. It may contain valuable combined usage patterns for a future update.

---

_Source: Figma MCP · Oxygen MCP examples · Extracted 2026-05-08_
