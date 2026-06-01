---
component: Button
package: "@8x8/oxygen-button"
category: interaction
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Button/props]]"
  - "[[Button/tokens]]"
  - "[[Button/accessibility]]"
  - "[[Button/Button-figma]]"
  - "[[Button/Button-usage]]"
  - "[[Button/Button-audit]]"
tags:
  - oxygen
  - component/Button
  - role/examples
  - stage/blocked
  - category/interaction
---
# Button — Examples

> **See also:** [Props](props.md) · [Tokens](tokens.md) · [Accessibility](accessibility.md) · [Usage](Button-usage.md)

## Basic Usage

```tsx
import Button from '@8x8/oxygen-button';

<Button>Click me</Button>
```

---

## Variants

```tsx
import Button from '@8x8/oxygen-button';

// Default (primary)
<Button>Click me</Button>
<Button isActive>Click me</Button>
<Button isDisabled>Click me</Button>

// Primary
<Button variant="primary">Click me</Button>
<Button variant="primary" isActive>Click me</Button>
<Button variant="primary" isDisabled>Click me</Button>

// Secondary
<Button variant="secondary">Click me</Button>
<Button variant="secondary" isActive>Click me</Button>
<Button variant="secondary" isDisabled>Click me</Button>

// Tertiary (control action — use with isCircular)
<Button variant="tertiary">Click me</Button>
<Button variant="tertiary" isActive>Click me</Button>
<Button variant="tertiary" isDisabled>Click me</Button>

// Tertiary Reversed (use on dark/inverted backgrounds)
<Button variant="tertiaryReversed">Click me</Button>
<Button variant="tertiaryReversed" isActive>Click me</Button>
<Button variant="tertiaryReversed" isDisabled>Click me</Button>

// Text (low-priority actions)
<Button variant="text">Click me</Button>
<Button variant="text" isActive>Click me</Button>
<Button variant="text" isDisabled>Click me</Button>

// Success (call controls)
<Button variant="success">Click me</Button>
<Button variant="success" isActive>Click me</Button>
<Button variant="success" isDisabled>Click me</Button>
```

---

## Sizes

```tsx
import Button from '@8x8/oxygen-button';

// Default (medium)
<Button>Click me</Button>

// Medium (explicit)
<Button size="medium">Click me</Button>

// Small
<Button size="small">Click me</Button>

// Large (recommended for touch targets)
<Button size="large">Click me</Button>

// Big (extra large)
<Button size="big">Click me</Button>
```

---

## With Icons

```tsx
import Button from '@8x8/oxygen-button';
import { PlusIcon, LoginIcon } from '@8x8/oxygen-icon';

// No icon
<Button>Click me</Button>

// Icon left
<Button iconLeft={<PlusIcon />}>Click me</Button>

// Icon right
<Button iconRight={<LoginIcon />}>Click me</Button>
```

---

## Destructive State

```tsx
import Button from '@8x8/oxygen-button';
import { PlusIcon, LoginIcon } from '@8x8/oxygen-icon';

// Primary destructive
<Button variant="primary" isDestructive>Click me</Button>
<Button variant="primary" isDestructive isActive>Click me</Button>
<Button variant="primary" isDestructive isDisabled>Click me</Button>

// Secondary destructive
<Button variant="secondary" isDestructive>Click me</Button>
<Button variant="secondary" isDestructive isActive>Click me</Button>
<Button variant="secondary" isDestructive isDisabled>Click me</Button>

// Text destructive
<Button variant="text" isDestructive>Click me</Button>
<Button variant="text" isDestructive isActive>Click me</Button>
<Button variant="text" isDestructive isDisabled>Click me</Button>

// Icon + destructive
<Button isDestructive iconLeft={<PlusIcon />} />
<Button isDestructive isActive iconLeft={<PlusIcon />} />
<Button isDestructive isDisabled iconLeft={<PlusIcon />} />
<Button isDestructive iconRight={<LoginIcon />} />
<Button isDestructive isActive iconRight={<LoginIcon />} />
<Button isDestructive isDisabled iconRight={<LoginIcon />} />

<Button variant="text" isDestructive isActive iconLeft={<PlusIcon />} />
<Button variant="text" isDestructive isDisabled iconLeft={<PlusIcon />} />
<Button variant="text" isDestructive iconRight={<LoginIcon />} />
<Button variant="text" isDestructive isActive iconRight={<LoginIcon />} />
<Button variant="text" isDestructive isDisabled iconRight={<LoginIcon />} />
```

---

## Circular (Control) Buttons

```tsx
import Button from '@8x8/oxygen-button';
import { AddReactionIcon, MicSlashIcon, PhoneIcon, HangupIcon } from '@8x8/oxygen-icon';

// Default circular
<Button isCircular><AddReactionIcon /></Button>
<Button isCircular isActive><AddReactionIcon /></Button>
<Button isCircular isDisabled><AddReactionIcon /></Button>

// Primary circular
<Button variant="primary" isCircular><AddReactionIcon /></Button>
<Button variant="primary" isCircular isActive><AddReactionIcon /></Button>
<Button variant="primary" isCircular isDisabled><AddReactionIcon /></Button>

// Secondary circular
<Button variant="secondary" isCircular><AddReactionIcon /></Button>
<Button variant="secondary" isCircular isActive><AddReactionIcon /></Button>
<Button variant="secondary" isCircular isDisabled><AddReactionIcon /></Button>

// Tertiary circular (mute/unmute)
<Button variant="tertiary" isCircular><MicSlashIcon /></Button>
<Button variant="tertiary" isCircular isActive><MicSlashIcon /></Button>
<Button variant="tertiary" isCircular isDisabled><MicSlashIcon /></Button>

// Tertiary Reversed circular (inverted background)
<Button variant="tertiaryReversed" isCircular><MicSlashIcon /></Button>
<Button variant="tertiaryReversed" isCircular isActive><MicSlashIcon /></Button>
<Button variant="tertiaryReversed" isCircular isDisabled><MicSlashIcon /></Button>

// Success circular (answer call)
<Button variant="success" isCircular><PhoneIcon /></Button>
<Button variant="success" isCircular isActive><PhoneIcon /></Button>
<Button variant="success" isCircular isDisabled><PhoneIcon /></Button>

// Destructive circular (hang up)
<Button variant="destructive" isCircular><HangupIcon /></Button>
<Button variant="destructive" isCircular isActive><HangupIcon /></Button>
<Button variant="destructive" isCircular isDisabled><HangupIcon /></Button>
```

---

## Accessibility — Disabled in Forms

> A disabled Button is still focusable but does not fire form submission.

```tsx
<form onSubmit={() => alert('submit')}>
  <label htmlFor="fname">First name:</label>
  <input type="text" id="fname" name="fname" value="John" />
  <label htmlFor="lname">Last name:</label>
  <input type="text" id="lname" name="lname" value="Doe" />
  <Button type="submit" isDisabled>
    Submit
  </Button>
</form>
```

---

## ButtonGroup

```tsx
import Button, { ButtonGroup } from '@8x8/oxygen-button';

// Default group
<ButtonGroup>
  <Button>Button 1</Button>
  <Button variant="secondary">Button 2</Button>
  <Button variant="destructive">Button 3</Button>
</ButtonGroup>

// Center aligned
<ButtonGroup align="center">
  <Button>Button 1</Button>
  <Button variant="secondary">Button 2</Button>
  <Button variant="destructive">Button 3</Button>
</ButtonGroup>

// Left aligned
<ButtonGroup align="left">
  <Button>Button 1</Button>
  <Button variant="secondary">Button 2</Button>
  <Button variant="destructive">Button 3</Button>
</ButtonGroup>

// Right aligned
<ButtonGroup align="right">
  <Button>Button 1</Button>
  <Button variant="secondary">Button 2</Button>
  <Button variant="destructive">Button 3</Button>
</ButtonGroup>

// Large spacing
<ButtonGroup spacing="large">
  <Button>Button 1</Button>
  <Button variant="secondary">Button 2</Button>
  <Button variant="destructive">Button 3</Button>
</ButtonGroup>

// Small spacing with small buttons
<ButtonGroup spacing="small">
  <Button size="small">Button 1</Button>
  <Button size="small" variant="secondary">Button 2</Button>
  <Button size="small" variant="destructive">Button 3</Button>
</ButtonGroup>
```

---

## DropdownButton

```tsx
import { DropdownButton } from '@8x8/oxygen-button';

// No label
<DropdownButton />

// With label
<DropdownButton>Call to action</DropdownButton>

// Full width
<DropdownButton fullWidth>Dropdown Button</DropdownButton>

// Active state
<DropdownButton isActive>Dropdown Button</DropdownButton>

// Disabled state
<DropdownButton isDisabled>Dropdown Button</DropdownButton>

// Sizes
<DropdownButton>Dropdown Button</DropdownButton>
<DropdownButton size="medium">Dropdown Button</DropdownButton>
<DropdownButton size="large">Dropdown Button</DropdownButton>
<DropdownButton size="small">Dropdown Button</DropdownButton>
```

---

## IconButton

```tsx
import { IconButton, iconButtonSize } from '@8x8/oxygen-button';
import { AddReactionIcon } from '@8x8/oxygen-icon';
import Tooltip from '@8x8/oxygen-tooltip';

// Basic usage
<IconButton>
  <AddReactionIcon />
</IconButton>

// Inverted (dark background)
<IconButton isInverted>
  <AddReactionIcon />
</IconButton>

// Custom size (any IconButtonSize enum member, e.g. mediumIconM)
<IconButton size={iconButtonSize.mediumIconM}>
  <AddReactionIcon />
</IconButton>

// Larger icon
<IconButton>
  <AddReactionIcon size={100} />
</IconButton>

// With Tooltip (recommended for accessibility)
<Tooltip title="Here comes some more detailed description">
  <IconButton>
    <AddReactionIcon />
  </IconButton>
</Tooltip>
```

---

_Source: Oxygen MCP · Extracted 2026-04-28_
