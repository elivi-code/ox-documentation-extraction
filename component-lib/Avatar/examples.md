---
component: Avatar
package: "@8x8/oxygen-avatar"
category: data_display
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Avatar/props]]"
  - "[[Avatar/tokens]]"
  - "[[Avatar/accessibility]]"
  - "[[Avatar/Avatar-figma]]"
  - "[[Avatar/Avatar-audit]]"
tags:
  - oxygen
  - component/Avatar
  - role/examples
  - stage/blocked
  - category/data_display
---
# Avatar — Examples

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md)

---

> **Note:** The Oxygen MCP returned no clean code snippets for this component (`cleanExamples`
> returned 0 results). Examples below are reconstructed from prop definitions, Figma design
> context, and Oxygen usage documentation. Verify against the live Storybook.

---

## Basic usage

```tsx
import { Avatar } from '@8x8/oxygen-avatar';

// Photo avatar
<Avatar src="/path/to/photo.jpg" name="Jane Smith" size="medium" />

// Initials avatar (no photo)
<Avatar name="Jane Smith" size="medium" />

// Icon fallback (no name, no photo)
<Avatar size="medium" />

// Group avatar
<Avatar isGroup size="medium" />
```

---

## Sizes

```tsx
<Avatar name="Jane Smith" size="xsmall" />   {/* 24px — top bar */}
<Avatar name="Jane Smith" size="small" />    {/* 32px — small cards */}
<Avatar name="Jane Smith" size="medium" />   {/* 40px — default */}
<Avatar name="Jane Smith" size="large" />    {/* 48px — wide browsers */}
<Avatar name="Jane Smith" size="xlarge" />   {/* 80px — profile picture update */}

{/* Custom size (disables userStatus and showEditOverlay) */}
<Avatar name="Jane Smith" size={56} />
```

---

## With user status badge

```tsx
import { Avatar } from '@8x8/oxygen-avatar';

<Avatar name="Jane Smith" size="medium" userStatus="Available" />
<Avatar name="Jane Smith" size="medium" userStatus="Busy" />
<Avatar name="Jane Smith" size="medium" userStatus="Away" />
<Avatar name="Jane Smith" size="medium" userStatus="Offline" />
<Avatar name="Jane Smith" size="medium" userStatus="DoNotDisturb" />
<Avatar name="Jane Smith" size="medium" userStatus="OnCall" />
<Avatar name="Jane Smith" size="medium" userStatus="WrapUp" />
```

---

## With status border ring

```tsx
{/* Status colour shown as border around avatar instead of/alongside badge */}
<Avatar
  name="Jane Smith"
  size="medium"
  userStatus="Available"
  hasStatusBorder
/>
```

> When the avatar has focus (`isActive=true`) and a status ring is showing, the **focus ring
> replaces the presence ring** — they do not stack.

---

## Interactive avatar with edit overlay

```tsx
<Avatar
  name="Jane Smith"
  size="xlarge"
  src="/path/to/photo.jpg"
  showEditOverlay
  onEdit={(e) => console.log('edit clicked')}
  onClick={(e) => console.log('avatar clicked')}
/>
```

> `showEditOverlay` is only available for sizes `l`–`3xl`.

---

## Active / focused state

```tsx
<Avatar name="Jane Smith" size="medium" isActive />
```

---

## With border

```tsx
<Avatar name="Jane Smith" size="medium" hasBorder />
```

---

## Custom children

```tsx
import { Avatar } from '@8x8/oxygen-avatar';
import { SomeIcon } from '@8x8/oxygen-icons';

{/* Custom icon as content */}
<Avatar size="medium">
  <SomeIcon />
</Avatar>
```

---

## Controlling initials

```tsx
{/* Default: 2 initials from "Jane Ann Smith" → "JA" */}
<Avatar name="Jane Ann Smith" size="medium" />

{/* 1 initial → "J" */}
<Avatar name="Jane Ann Smith" size="medium" maxInitials={1} />

{/* 3 initials → "JAS" */}
<Avatar name="Jane Ann Smith" size="medium" maxInitials={3} />
```

---

## AvatarStack

```tsx
import { Avatar, AvatarStack } from '@8x8/oxygen-avatar';

{/* Stacked group — props not documented in MCP */}
<AvatarStack>
  <Avatar name="Alice" size="medium" />
  <Avatar name="Bob" size="medium" />
  <Avatar name="Carol" size="medium" />
</AvatarStack>
```

> `AvatarStack` props were not returned by the Oxygen MCP. Check the live Storybook for full API.

---

## Storybook reference

The only example returned by MCP is the documentation story wrapper — not a standalone snippet:

```tsx
export const AvatarDocumentation = args => (
  <>
    <Doc markdown headingIds>{README}</Doc>
    <Doc markdown>{example}</Doc>
    <ComponentSection>
      <Avatar
        {...args}
        onClick={args.onClick ? action('onClick') : undefined}
        size={args.size === CUSTOM_SIZE ? args.customSize : args.size}
      />
    </ComponentSection>
    <Doc markdown>{CHANGELOG}</Doc>
  </>
);
```

---

_Source: Oxygen MCP · Extracted 2026-04-28_
