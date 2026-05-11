---
component: PopoverMenu
package: "@8x8/oxygen-popover"
category: overlays_contextual
role: examples
role_description: "Code usage examples from basic to advanced patterns"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
siblings:
  - "[[PopoverMenu/props]]"
  - "[[PopoverMenu/tokens]]"
  - "[[PopoverMenu/accessibility]]"
  - "[[PopoverMenu/PopoverMenu-figma]]"
  - "[[PopoverMenu/PopoverMenu-usage]]"
  - "[[PopoverMenu/PopoverMenu-audit]]"
tags:
  - oxygen
  - component/PopoverMenu
  - role/examples
  - stage/blocked
  - category/overlays_contextual
---

# PopoverMenu — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Basic PopoverMenu with DropdownButton

The canonical usage: a `DropdownButton` trigger paired with a `PopoverMenu` that renders a list of items.

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

> **Note:** The MCP story file (`Popover.documentation.stories.tsx`) renders this example under the component name `<Popover items={...}>` rather than `<PopoverMenu items={...}>`. The `items` prop belongs to `PopoverMenu`'s API — `Popover` uses `floatingContent`/`isOpen`/`setIsOpen` instead. This may reflect a naming inconsistency in the story or an API alias; flag as `DOC_GAP` in audit.

---

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

> **Data gap:** No additional examples were returned by the MCP. The above controlled pattern is inferred from the `Popover` props API. Only 1 story exists in the package (`Popover.documentation.stories.tsx`).

---

## Handling menu events

```tsx
import { PopoverMenu } from '@8x8/oxygen-popover';
import { DropdownButton } from '@8x8/oxygen-button';

<PopoverMenu
  items={[
    { key: 'edit', children: 'Edit' },
    { key: 'duplicate', children: 'Duplicate' },
    { key: 'delete', children: 'Delete' },
  ]}
  onMenuItemClick={(event) => {
    console.log('Item clicked', event);
  }}
  onMenuOpenToggle={(isOpen) => {
    console.log('Menu is now', isOpen ? 'open' : 'closed');
  }}
  onCancel={() => {
    console.log('Menu dismissed without selection');
  }}
>
  <DropdownButton>Actions</DropdownButton>
</PopoverMenu>
```

---

## With header and footer

```tsx
import { PopoverMenu } from '@8x8/oxygen-popover';
import { DropdownButton } from '@8x8/oxygen-button';

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

> **Data gap:** No MCP examples for `header`/`footer` props. Pattern inferred from prop types.

---

_Source: Oxygen MCP · Extracted 2026-05-08_
