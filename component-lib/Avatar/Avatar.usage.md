---
parent: "[[Avatar]]"
section: usage
component: Avatar
package: "@8x8/oxygen-avatar"
role: spoke
pipeline_stage: rewritten
audit_verdict: "NO"
tags: [oxygen, component/Avatar, role/spoke, spoke/usage]
---

<!-- source: editorial -->

# Avatar — Usage

Avatar is a circular visual representation of a user, room, or other entity. It renders a photo, computed initials, or a fallback icon — in that priority order — and can carry a status badge, presence ring, and edit overlay depending on context and size.

---

## When to use

- Identify a person, room, or entity at a glance in calls, contacts, conversation lists, or participant panels.
- Pair with a `userStatus` badge to show presence (e.g. Available, Busy, Offline) for User-type entities.
- Use [[AvatarStack]] when you need to represent a group of related users with overlap and "+N" overflow.

## When not to use

| Situation | Use instead |
|---|---|
| Decorative illustration or product icon | `<img>` or an Oxygen Icon component |
| Group membership count without specific members | A numeric badge / pill |
| Brand logo or team logo in a non-contact context | `<img>` with appropriate alt text |

---

## Do / Don't

### Pair 1 — Interactive avatars need an accessible name

#### ✅ Do — Wrap clickable avatars in a `<button>` with an `aria-label`

When an Avatar carries an `onClick` or `onEdit` handler it becomes an interactive control. The Avatar component provides no built-in ARIA role or label, so consumers must supply one.

```tsx
<button aria-label="View Jane Smith's profile">
  <Avatar name="Jane Smith" size="medium" />
</button>

<Avatar
  name="Jane Smith"
  size="xlarge"
  showEditOverlay
  onEdit={() => openPhotoUpload()}
  aria-label="Edit profile photo for Jane Smith"
/>
```

#### ❌ Don't — Pass `onClick` without any accessible label or wrapper role

```tsx
<Avatar name="Jane Smith" size="medium" onClick={() => openProfile()} />
```

---

### Pair 2 — Status information must reach screen readers

#### ✅ Do — Include status in `aria-label` or add visually-hidden text when `userStatus` is shown

```tsx
<Avatar name="Jane Smith" userStatus="Busy" aria-label="Jane Smith, Busy" />

<Avatar name="Jane Smith" userStatus="Away">
  <span className="sr-only">Jane Smith — Away</span>
</Avatar>
```

#### ❌ Don't — Show a status badge without communicating its value

```tsx
<Avatar name="Jane Smith" userStatus="Busy" />
```

---

### Pair 3 — Always pass `name`, even when a photo URL is provided

#### ✅ Do — Provide `name` whenever you have it, regardless of `src`

`name` supplies the initials fallback if the image fails to load and is the natural source for an accessible label.

```tsx
<Avatar src="/avatars/jane.jpg" name="Jane Smith" size="medium" />
```

#### ❌ Don't — Omit `name` when a photo URL is available

```tsx
<Avatar src="/avatars/jane.jpg" size="medium" />
```

---

### Pair 4 — Reserve `userStatus` for User-type avatars

#### ✅ Do — Apply `userStatus` only to avatars that represent a real user with presence

```tsx
<Avatar name="Jane Smith" size="medium" userStatus="Available" />
<Avatar name="Sales Room" size="medium" isGroup />
```

#### ❌ Don't — Add `userStatus` to Room, Call Queue, or other non-User entities

```tsx
<Avatar name="Conference Room A" size="medium" userStatus="Available" />
<Avatar name="Support Queue" size="medium" userStatus="Busy" />
```

---

### Pair 5 — `hasStatusBorder` requires a string `userStatus`

#### ✅ Do — Pass a valid `AvatarUserStatus` string when using `hasStatusBorder`

```tsx
<Avatar
  name="Jane Smith"
  size="medium"
  userStatus="Available"
  hasStatusBorder
/>
```

#### ❌ Don't — Combine `hasStatusBorder` with a custom React element `userStatus`

```tsx
<Avatar
  name="Jane Smith"
  size="medium"
  userStatus={<CustomStatusIcon />}
  hasStatusBorder
/>
```

---

### Pair 6 — `showEditOverlay` is only available on `large` and `xlarge`

#### ✅ Do — Use `showEditOverlay` on `large` (48 px) or `xlarge` (80 px) avatars

```tsx
<Avatar
  name="Jane Smith"
  size="xlarge"
  showEditOverlay
  onEdit={() => openPhotoUpload()}
/>
```

> Available only on `large` and `xlarge`. At smaller sizes (`xsmall`, `small`, `medium`) the overlay is silently suppressed.

#### ❌ Don't — Enable `showEditOverlay` on `xsmall`, `small`, or `medium` avatars

```tsx
<Avatar name="Jane Smith" size="small" showEditOverlay onEdit={() => {}} />
<Avatar name="Jane Smith" size="medium" showEditOverlay onEdit={() => {}} />
```

---

### Pair 7 — Use `AvatarStack` for multi-user groups

#### ✅ Do — Wrap related user avatars in `AvatarStack`

```tsx
import { Avatar, AvatarStack } from '@8x8/oxygen-avatar';

<AvatarStack>
  <Avatar name="Alice Zhang" size="medium" />
  <Avatar name="Bob Patel" size="medium" />
  <Avatar name="Carol Kim" size="medium" />
</AvatarStack>
```

#### ❌ Don't — Manually lay out multiple avatars with negative margins or absolute positioning

```tsx
<div style={{ display: 'flex' }}>
  <Avatar name="Alice Zhang" size="medium" style={{ marginRight: '-8px' }} />
  <Avatar name="Bob Patel" size="medium" style={{ marginRight: '-8px' }} />
  <Avatar name="Carol Kim" size="medium" />
</div>
```
