---
parent: "[[Button]]"
section: usage
component: Button
package: "@8x8/oxygen-button"
source_type: editorial
tags: [oxygen, component/Button, role/usage, section/usage]
---

# Button — Usage Guidelines

> **Editorial guidance** transcribed from the published Oxygen docs page (`https://oxygen.8x8.com/docs/components/button/usage`, screenshot 2026-05-11) and cross-validated against the extracted MCP/Figma artifacts. No Figma `↳ Button examples` Do/Don't card frames exist; replace with `figma-extract-usage` output if one is created.

Buttons let users initiate an action, submit a form, or trigger a state change. Visual weight, color, and placement together signal **how important** an action is relative to everything else on the surface.

---

## Type matrix

| Type | Oxygen API | Use for | Notes |
|------|-----------|---------|-------|
| Primary | `variant="primary"` (default) | The single most important action on a surface | One per surface — Pair 1 |
| Secondary | `variant="secondary"` | Supporting actions next to a primary | Can repeat per surface |
| Text | `variant="text"` | Low-emphasis inline actions | No visible container at rest — Pair 2 |
| Destructive | `isDestructive` + any variant | Irreversible / data-loss actions | Pair with confirmation — Pair 3 |
| Split | `ButtonGroup` of two buttons | A default action plus a related menu | Default action is most-used — Pair 6 |
| Dropdown | `DropdownButton` | Action that opens a menu, no single default | Pair with `Popover`/`PopoverMenu` |
| Icon | `IconButton` or `Button` with `isCircular` | Compact, icon-only triggers | Always carry an accessible name — Pair 4 |
| Control | `tertiary` / `tertiaryReversed` / `success` / `destructive` + `isCircular` | Call-control & toolbar affordances | Live on dark/inverted surfaces |

<!-- SKIP:GAP-018 manual="Published docs reference 'Soft', 'Disclosure', 'Optional', 'Indeterminate' treatments — absent from props.md. Likely composition patterns, not first-class API variants. Confirm with Oxygen team." -->

---

## Sizes

- **`large`** is recommended for touch targets (meets WCAG 2.5.5 fingertip minimums).
- **`medium`** is the default for desktop, mouse-driven UI.
- **`small`** is for compact layouts (toolbars, dense forms).
- Only the **`large` (48px)** container dimensions are confirmed from Figma; Medium/Small are a SOURCE_GAP — do not hand-assert pixel values.

Do not mix sizes within a single action row — Pair 5.

---

## Placement & alignment

- **Primary action sits on the right** in horizontal action rows (Western reading order).
- **Secondary/tertiary actions sit to the left** of the primary, separated by `ButtonGroup` spacing.
- **Destructive actions** are usually **left-most**, away from the resting primary affordance, to reduce accidental activation.
- Use `<ButtonGroup align="right" />` for dialogs and `align="left"` for inline forms.

<!-- SKIP:GAP-019 manual="Exact 'primary right-aligned in dialogs' wording not captured from docs screenshot at readable resolution. Confirm verbatim from the published Alignment section." -->

---

## Do / Don't

### Pair 1 — One primary per surface

**✅ Do** — single Primary button for the most important action:

```tsx
<ButtonGroup align="right">
  <Button variant="text">Cancel</Button>
  <Button variant="secondary">Save as draft</Button>
  <Button variant="primary">Publish</Button>
</ButtonGroup>
```

**❌ Don't** — stack multiple Primary buttons; they compete for attention and erode hierarchy:

```tsx
<ButtonGroup align="right">
  <Button variant="primary">Save as draft</Button>
  <Button variant="primary">Publish</Button>
</ButtonGroup>
```

### Pair 2 — Text buttons for low-emphasis actions

**✅ Do** — `variant="text"` for inline, low-priority actions:

```tsx
<ButtonGroup>
  <Button variant="text">Cancel</Button>
  <Button variant="primary">Confirm</Button>
</ButtonGroup>
```

**❌ Don't** — use Text buttons as the primary call-to-action (the affordance disappears):

```tsx
<ButtonGroup align="right">
  <Button variant="text">Publish</Button>
</ButtonGroup>
```

### Pair 3 — Reserve destructive styling for irreversible actions

**✅ Do** — combine `isDestructive` with a confirmation step:

```tsx
<Button variant="primary" isDestructive onClick={openConfirmDialog}>
  Delete account
</Button>
```

**❌ Don't** — use `isDestructive` for routine actions or as emphasis:

```tsx
<Button variant="primary" isDestructive>Sign out</Button>
```

### Pair 4 — Icon-only buttons must carry an accessible name

**✅ Do** — pair `IconButton` with a `Tooltip` (its `title` becomes the accessible name):

```tsx
<Tooltip title="Add reaction">
  <IconButton>
    <AddReactionIcon />
  </IconButton>
</Tooltip>
```

**❌ Don't** — ship a bare icon button with no label (fails WCAG 4.1.2):

```tsx
<IconButton>
  <AddReactionIcon />
</IconButton>
```

### Pair 5 — Keep one size per action row

**✅ Do** — match button sizes within a `ButtonGroup`:

```tsx
<ButtonGroup spacing="small">
  <Button size="small" variant="text">Cancel</Button>
  <Button size="small" variant="secondary">Save as draft</Button>
  <Button size="small" variant="primary">Publish</Button>
</ButtonGroup>
```

**❌ Don't** — mix sizes within a single action row (breaks alignment and rhythm):

```tsx
<ButtonGroup>
  <Button size="small" variant="text">Cancel</Button>
  <Button size="large" variant="primary">Publish</Button>
</ButtonGroup>
```

### Pair 6 — Choose Split vs Dropdown by user intent

**✅ Do** — use a Split (`ButtonGroup` of two) when one action is clearly the default:

```tsx
<ButtonGroup>
  <Button variant="primary">Reply</Button>
  <DropdownButton variant="primary" aria-label="More reply options" />
</ButtonGroup>
```

**✅ Do** — use a `DropdownButton` alone when there is no single default:

```tsx
<DropdownButton>Reply</DropdownButton>
```

**❌ Don't** — surface a "Reply" split when half your users want "Reply all".

### Pair 7 — Don't disable a button to hide a validation error

**✅ Do** — keep the button enabled and surface the error inline:

```tsx
<form onSubmit={handleSubmit}>
  <Input label="Email" error={emailError} aria-describedby="email-error" />
  <Button type="submit">Save</Button>
</form>
```

**❌ Don't** — disable submit until every field is valid with no explanation:

```tsx
<Button type="submit" isDisabled={!isFormValid}>Save</Button>
```

> If you must disable (e.g. during a long-running submit), pair it with a visible status message via `aria-describedby` so the disabled reason is announced.

---

## When not to use

| Situation | Use instead |
|-----------|-------------|
| Navigating to another page or external URL | `TextLink` (or routing equivalent) |
| Inline within a paragraph of body text | `TextLink` |
| Representing a non-interactive label or status | `Badge`, `Chip`, or plain text |
| As the only validation feedback (disabling until valid) | Keep enabled, show inline field errors — Pair 7 |

---

## Related components

- **`ButtonGroup`** — horizontal arrangement with shared spacing/alignment.
- **`DropdownButton`** — button that opens a menu (typically `Popover`/`PopoverMenu`).
- **`IconButton`** — compact icon-only trigger; always pair with `Tooltip`.
- **`TextLink`** — for navigation rather than actions.

<!-- SKIP:GAP-020 manual="Related list derived from props.md/accessibility.md, not confirmed against the live docs page. Additional entries (Tooltip, Popover, ConfirmDialog) may exist — confirm." -->
