---
component: Avatar
package: "@8x8/oxygen-avatar"
category: data_display
role: usage
role_description: "Usage guidelines — editorially authored from extracted artifacts; no Figma examples page exists"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from extracted artifacts — NOT from Figma Do/Don't frames. Re-run doc-audit after creation; replace pairs with figma-extract-usage output when a Figma examples page exists."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Avatar/props]]"
  - "[[Avatar/examples]]"
  - "[[Avatar/tokens]]"
  - "[[Avatar/accessibility]]"
  - "[[Avatar/Avatar-figma]]"
  - "[[Avatar/Avatar-audit]]"
tags:
  - oxygen
  - component/Avatar
  - role/usage
  - stage/editorial
  - category/data_display
---
<!-- SKILL: usage-advisor -->
<!-- COMPONENT: Avatar -->
<!-- DRAFTED: 2026-05-11 -->
<!-- MODE: open -->
<!-- GROUNDING: full — props.md, examples.md, Avatar-figma.md, accessibility.md, tokens.md, Avatar-audit.md -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma examples page is created -->
<!-- PAIRS: 7 -->

# Avatar — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [Avatar-figma.md](./Avatar-figma.md)

> **Editorial guidance — not Figma-sourced.** No `↳ Avatar examples` Figma page exists, so
> `figma-extract-usage` cannot run. The Do/Don't pairs below are inferred from `props.md`,
> `examples.md`, `accessibility.md`, and `Avatar-figma.md`. Treat as provisional until a designer
> reviews them. Replace with `figma-extract-usage` output when a Figma examples page is created.

Avatar is a circular visual representation of a user, room, or other entity. It renders a photo,
computed initials, or a fallback icon — in that priority order — and can carry a status badge,
presence ring, and edit overlay depending on context and size.

---

## When to use

- Identify a person, room, or entity at a glance in calls, contacts, conversation lists, or participant panels.
- Pair with a `userStatus` badge to show presence (e.g. Available, Busy, Offline) for User-type entities.
- Use `AvatarStack` when you need to represent a group of related users with overlap and "+N" overflow.

## When not to use

| Situation | Use instead |
|-----------|-------------|
| Decorative illustration or product icon | `<img>` or an Oxygen Icon component |
| Group membership count without specific members | A numeric badge / pill |
| Brand logo or team logo in a non-contact context | `<img>` with appropriate alt text |

---

## Do / Don't

<!-- SCREENSHOTS UNAVAILABLE — no Figma examples page exists for Avatar -->

### Pair 1 — Interactive avatars need an accessible name

#### ✅ Do — Wrap clickable avatars in a `<button>` with an `aria-label`

> When an Avatar carries an `onClick` or `onEdit` handler it becomes an interactive control.
> The Avatar component provides no built-in ARIA role or label, so consumers must supply one.
> Use a native `<button>` (or `role="button"` + `aria-label`) so keyboard users and screen reader
> users can discover and activate the control.

```tsx
<button aria-label="View Jane Smith's profile">
  <Avatar name="Jane Smith" size="medium" />
</button>

{/* Edit overlay: label the specific action */}
<Avatar
  name="Jane Smith"
  size="xlarge"
  showEditOverlay
  onEdit={() => openPhotoUpload()}
  aria-label="Edit profile photo for Jane Smith"
/>
```

**Grounded in:** `accessibility.md` lines 62–69 (interactive ARIA guidance) · WCAG 4.1.2 (`accessibility.md` line 129)

#### ❌ Don't — Pass `onClick` without any accessible label or wrapper role

> An avatar with an `onClick` handler but no accessible name is invisible to screen readers and
> unreachable for keyboard-only users. Visual cues (cursor: pointer, hover highlight) are
> insufficient — the role and name must be in the DOM.

```tsx
{/* Missing: no role, no aria-label, no button wrapper */}
<Avatar name="Jane Smith" size="medium" onClick={() => openProfile()} />
```

---

### Pair 2 — Status information must reach screen readers

#### ✅ Do — Include status in `aria-label` or add visually-hidden text when `userStatus` is shown

> The status badge conveys its meaning through colour and an icon. Both are invisible to assistive
> technology by default. Include the status value in the avatar's accessible name, or use
> visually-hidden text alongside the component.

```tsx
{/* Option 1: embed status in aria-label */}
<Avatar name="Jane Smith" userStatus="Busy" aria-label="Jane Smith, Busy" />

{/* Option 2: sr-only sibling (when aria-label would be too long) */}
<Avatar name="Jane Smith" userStatus="Away">
  <span className="sr-only">Jane Smith — Away</span>
</Avatar>
```

**Grounded in:** `accessibility.md` lines 100–113 (status/presence accessibility) · WCAG 1.3.1 (`accessibility.md` line 122)

#### ❌ Don't — Show a status badge without communicating its value to assistive technology

> Colour-only or icon-only status information fails WCAG 1.3.1 (Info and Relationships). A screen
> reader user navigating a contact list will hear "Jane Smith" with no indication that she is busy
> or unavailable.

```tsx
{/* Status visible but not announced */}
<Avatar name="Jane Smith" userStatus="Busy" />
```

---

### Pair 3 — Always pass `name`, even when a photo URL is provided

#### ✅ Do — Provide `name` whenever you have it, regardless of whether `src` is also set

> `name` serves two purposes beyond showing initials: it supplies the text used in the initials
> fallback if the image fails to load, and it is the natural source for any accessible label on the
> avatar. Omitting it means a broken image silently degrades to a generic icon with no identification.

```tsx
{/* Correct — name is always provided */}
<Avatar src="/avatars/jane.jpg" name="Jane Smith" size="medium" />
```

**Grounded in:** `props.md` line 70 (`name` computes initials) · `props.md` lines 114–121 (content fallback chain: photo → initials → icon) · `accessibility.md` WCAG 1.1.1 (line 121)

#### ❌ Don't — Omit `name` when a photo URL is available

> If `src` is set but `name` is not, a broken or slow-loading image falls back directly to the
> generic icon — with no initials and no accessible text to identify the person.

```tsx
{/* No name — broken image shows a generic icon, no initials fallback */}
<Avatar src="/avatars/jane.jpg" size="medium" />
```

---

### Pair 4 — Reserve `userStatus` for User-type avatars

#### ✅ Do — Apply `userStatus` only to avatars that represent a real user with presence

> Presence (Available, Busy, On Call, etc.) is meaningful for individual users. The Avatar
> component supports multiple entity types — User, Room, Auto Attendant, Call Queue, Ring Group,
> Channel, SMS Group — and only the User type has a Status variant in the Figma component set.

```tsx
{/* Correct — User avatar with presence status */}
<Avatar name="Jane Smith" size="medium" userStatus="Available" />

{/* Correct — Room avatar without status */}
<Avatar name="Sales Room" size="medium" isGroup />
```

**Grounded in:** `Avatar-figma.md` lines 107–108 (Type variant axis: User, Room, Auto Attendant, Call Queue, Ring Group, Channel, SMS Group) · `Avatar-figma.md` lines 92–97 (non-User types have no Color/Content/Status variant axes)

#### ❌ Don't — Add `userStatus` to Room, Call Queue, or other non-User entity avatars

> Rooms and call queues don't have presence — showing a "Busy" badge on a conference room or
> an "Available" badge on an Auto Attendant is semantically misleading and has no counterpart in
> the Figma design system.

```tsx
{/* Misleading — room/queue presence has no defined meaning */}
<Avatar name="Conference Room A" size="medium" userStatus="Available" />
<Avatar name="Support Queue" size="medium" userStatus="Busy" />
```

---

### Pair 5 — `hasStatusBorder` requires a string `userStatus`, not a React element

#### ✅ Do — Pass a valid `AvatarUserStatus` string when using `hasStatusBorder`

> `hasStatusBorder` renders the status colour as a ring around the avatar. It is only activated
> when `userStatus` holds a valid `AvatarUserStatus` string (e.g. `"Available"`, `"Busy"`).
> Passing a custom React element as `userStatus` disables the ring silently.

```tsx
{/* Correct — string userStatus activates the border ring */}
<Avatar
  name="Jane Smith"
  size="medium"
  userStatus="Available"
  hasStatusBorder
/>
```

**Grounded in:** `props.md` line 75 (`hasStatusBorder` description) · `props.md` line 130 (constraint: "Only active when `userStatus` is a valid `AvatarUserStatus` string (not a ReactElement)")

#### ❌ Don't — Combine `hasStatusBorder` with a custom React element `userStatus`

> If you pass a ReactElement as `userStatus` (e.g. a custom icon or badge), `hasStatusBorder` has
> no effect — no ring appears, and there is no error or warning. The constraint is silent.

```tsx
{/* hasStatusBorder is silently ignored — no ring will render */}
<Avatar
  name="Jane Smith"
  size="medium"
  userStatus={<CustomStatusIcon />}
  hasStatusBorder
/>
```

---

### Pair 6 — `showEditOverlay` is only available for sizes `l`–`3xl`

#### ✅ Do — Use `showEditOverlay` on `large` (48 px) or bigger avatars

> The edit overlay is designed for the profile-picture update pattern, where the avatar is
> large enough to accommodate a hover affordance. Sizes `large` through `3xl` are supported.
> The `xlarge` (80 px) size is the most common context for edit overlays.

```tsx
{/* Correct — xlarge is the canonical edit-overlay size */}
<Avatar
  name="Jane Smith"
  size="xlarge"
  showEditOverlay
  onEdit={() => openPhotoUpload()}
/>
```

**Grounded in:** `props.md` line 79 (`showEditOverlay` description) · `props.md` line 129 (constraint: "Only available for sizes `l`–`3xl`") · `examples.md` lines 103–117 (edit overlay example uses `xlarge`)

#### ❌ Don't — Enable `showEditOverlay` on `xsmall`, `small`, or `medium` avatars

> The overlay is silently suppressed for sizes below `large`. Setting `showEditOverlay={true}` on
> a `medium` avatar produces no visible change and no console warning — making this a hard-to-spot
> misconfiguration.

```tsx
{/* Overlay silently does nothing at small sizes */}
<Avatar name="Jane Smith" size="small" showEditOverlay onEdit={() => {}} />
<Avatar name="Jane Smith" size="medium" showEditOverlay onEdit={() => {}} />
```

---

### Pair 7 — Use `AvatarStack` for multi-user groups; don't roll your own layout

#### ✅ Do — Wrap related user avatars in `AvatarStack`

> `AvatarStack` handles the overlap, z-index ordering, and "+N" overflow count that group
> representations require. It ensures visual consistency and saves you from reimplementing the
> same layout in CSS every time.

```tsx
import { Avatar, AvatarStack } from '@8x8/oxygen-avatar';

<AvatarStack>
  <Avatar name="Alice Zhang" size="medium" />
  <Avatar name="Bob Patel" size="medium" />
  <Avatar name="Carol Kim" size="medium" />
</AvatarStack>
```

**Grounded in:** `props.md` line 60 (AvatarStack listed as a component in the package) · `examples.md` lines 167–178 (AvatarStack code example)

#### ❌ Don't — Manually lay out multiple avatars with negative margins or absolute positioning

> Hand-rolled overlap layouts diverge from the design system's intent for group representation
> and don't inherit future updates (overflow count, ring treatment, dark mode) that `AvatarStack`
> may introduce.

```tsx
{/* Custom overlap — bypasses AvatarStack behaviour */}
<div style={{ display: 'flex' }}>
  <Avatar name="Alice Zhang" size="medium" style={{ marginRight: '-8px' }} />
  <Avatar name="Bob Patel" size="medium" style={{ marginRight: '-8px' }} />
  <Avatar name="Carol Kim" size="medium" />
</div>
```

---

## Grounding summary

| File | Used for |
|------|----------|
| `props.md` | Content fallback chain, prop constraints (userStatus, showEditOverlay, hasStatusBorder), AvatarSize table |
| `accessibility.md` | ARIA guidance, WCAG checklist, status/presence accessibility, focus ring behaviour |
| `Avatar-figma.md` | Type variant axis (User vs non-User types), anatomy of non-User types |
| `examples.md` | AvatarStack code pattern, edit overlay example |
| `tokens.md` | Background/text token pairs (not used in pairs — no token-mixing pair included) |
| `Avatar-audit.md` | Context on current verdict NO and 2 unresolved CONFLICTs |

## Axes presented but not included

- *Size-to-context mapping* — covered by the use-case column in `props.md`; a Do/Don't pair adds little.
- *Token pairing (`avatarBackgroundN` ↔ `avatarTextN`)* — designers select Figma variants, not raw tokens.
- *Focus ring replaces presence ring on focus* — behavioural fact, not an editorial decision.
- *`isGroup` placeholder* — folded into Pair 7 (use AvatarStack for groups).
- *Custom number `size`* — escape hatch, not a usage pattern worth a Do/Don't.
