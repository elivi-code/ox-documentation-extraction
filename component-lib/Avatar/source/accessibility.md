---
component: Avatar
package: "@8x8/oxygen-avatar"
category: data_display
role: accessibility
role_description: "Accessibility — ARIA roles, keyboard interactions, and WCAG 2.1 AA guidance"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Avatar/props]]"
  - "[[Avatar/examples]]"
  - "[[Avatar/tokens]]"
  - "[[Avatar/Avatar-figma]]"
  - "[[Avatar/Avatar-audit]]"
tags:
  - oxygen
  - component/Avatar
  - role/accessibility
  - stage/blocked
  - category/data_display
---
# Avatar — Accessibility

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) · [examples.md](./examples.md)

---

> **Note:** No explicit accessibility annotations were found in Figma for the Avatar component.
> Guidance below is inferred from the component's nature (display + optional interactive),
> Oxygen usage documentation, and WCAG 2.1 AA requirements.

---

## Component classification

Avatar is primarily a **display component** but can be **interactive** when `onClick`, `onEdit`,
or focus states are used.

| Mode | Behaviour |
|------|-----------|
| Display only | Not focusable; parent element carries accessible context |
| Interactive (`onClick`) | Focusable; requires accessible label |
| Edit overlay (`showEditOverlay`) | Focusable; requires accessible label for edit action |

---

## ARIA guidance

### Display (non-interactive)

```tsx
{/* Avatar with no click handler — treat as decorative or labelled by surrounding context */}
<Avatar name="Jane Smith" size="medium" aria-hidden="true" />

{/* If the avatar is the only representation of the user, provide a label via parent */}
<div aria-label="Jane Smith">
  <Avatar name="Jane Smith" size="medium" />
</div>
```

### Interactive (with onClick)

```tsx
{/* Wrap in a button or apply role="button" with an accessible label */}
<button aria-label="View Jane Smith's profile">
  <Avatar name="Jane Smith" size="medium" />
</button>
```

### With status badge

```tsx
{/* Status conveyed visually must also be communicated to screen readers */}
<Avatar
  name="Jane Smith"
  size="medium"
  userStatus="Available"
  aria-label="Jane Smith, Available"
/>
```

---

## Keyboard interaction

| Key | Behaviour |
|-----|-----------|
| `Tab` | Moves focus to the avatar (if interactive) |
| `Enter` / `Space` | Triggers `onClick` handler |
| `Tab` (on edit overlay) | Moves focus to edit overlay trigger |
| `Enter` / `Space` (on edit) | Triggers `onEdit` handler |

> **Focus ring behaviour:** When an avatar has `hasStatusBorder=true` (presence ring visible) and
> receives keyboard focus (`isActive=true`), the **presence ring is replaced by the focus ring**.
> This is intentional per Figma design annotation — they do not stack.

---

## Status / presence accessibility

The status badge and presence ring convey information **visually only** by default.
Ensure status information is also available to screen readers:

```tsx
{/* Option 1: Include status in aria-label */}
<Avatar name="Jane Smith" userStatus="Busy" aria-label="Jane Smith, Busy" />

{/* Option 2: Use visually-hidden text alongside */}
<Avatar name="Jane Smith" userStatus="Busy">
  <span className="sr-only">Jane Smith — Busy</span>
</Avatar>
```

---

## WCAG 2.1 AA checklist

| Criterion | Requirement | Status |
|-----------|-------------|--------|
| 1.1.1 Non-text content | Avatar image must have alt text or be marked decorative | ⚠️ `src` prop has no `alt` — `imageProps` can pass `alt`; verify in implementation |
| 1.3.1 Info and relationships | Status info conveyed by colour alone must have text equivalent | ⚠️ Status badge is colour-only by default — requires `aria-label` augmentation |
| 1.4.1 Use of colour | Status not conveyed by colour alone | ⚠️ Status badge uses colour + icon; ensure icon has accessible meaning |
| 1.4.3 Contrast (minimum) | Text contrast ≥ 4.5:1 normal, ≥ 3:1 large | ✅ Avatar token pairs (`avatarBackgroundN` / `avatarTextN`) are purpose-tuned for contrast |
| 1.4.11 Non-text contrast | UI components ≥ 3:1 against adjacent colours | ⚠️ Focus ring colour (`focus01`) should be verified against the avatar background |
| 2.1.1 Keyboard | All interactive functionality available via keyboard | ✅ `isActive` / focus ring supported; wrap in native button for keyboard access |
| 2.4.3 Focus order | Focus order is logical | ✅ Managed by parent layout |
| 2.4.7 Focus visible | Focus indicator visible | ✅ Focus ring rendered via `isActive=true` / `interactive/focus01` token |
| 4.1.2 Name, role, value | Interactive elements have accessible name and role | ⚠️ No built-in role — must be provided by consumer (wrap in `<button>` or add `role` + `aria-label`) |

---

## UserStatus component

The status badge inside Avatar is the `UserStatus` sub-component. Its full accessibility spec is at:
https://oxygen.8x8.com/components/userstatus/usage

---

_Source: Oxygen MCP · Figma annotations · WCAG 2.1 AA · Extracted 2026-04-28_
