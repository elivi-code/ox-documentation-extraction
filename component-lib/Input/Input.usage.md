---
parent: "[[Input]]"
section: usage
tags: [oxygen, component/Input, role/usage]
---

<!-- source: figma-only -->
<!-- Editorial — mirrors published Oxygen docs page (https://oxygen.8x8.com/components/textinput/usage, fetched 2026-05-13). No Figma "↳ Input examples" Do/Don't card page exists. Replace with figma-extract-usage output if such a page is created. -->

> **Scope:** Text input only (`22155:36793`). Text area is covered in [[TextArea]]. Search input shares this API surface but its Do/Don't guidance is deferred pending CONFLICT-001 resolution.

---

## When to use

> "The user needs to input information that cannot be predicted with predetermined options."

## When not to use

> "If the user has to enter a specific option other than a free-form input. If that's the case, consider using a dropdown, radio button or checkbox instead."

| Situation | Use instead |
|---|---|
| User picks one option from a small, known set | `Select` (many options) or `Radio` (≤ 5 options) |
| User picks multiple options from a known set | `Checkbox` group or multi-select `Select` |
| User enters multi-line prose | `TextArea` |
| User picks a date, time, or date range | `DateTimeSelector` / `DateTimeRangeSelector` |
| User picks a numeric value from a bounded range | `Slider` |

---

## Do / Don't pairs

### Pair 1 — Always pair with a visible, persistent label

**✅ Do** — Use a real `<label>` (or `aria-labelledby`)

```tsx
<label htmlFor="email">Email address</label>
<Input
  inputProps={{
    id: 'email', name: 'email', type: 'email',
    'aria-describedby': 'email-hint',
  }}
  onChange={handleChange}
/>
<p id="email-hint">We'll use this to send your receipt.</p>
```

**❌ Don't** — Use placeholder as the only label. The placeholder disappears on typing; screen readers don't announce it consistently. *"Avoid using placeholders whenever possible as they are not accessible, never use them to communicate important information."*

```tsx
{/* Wrong */}
<Input inputProps={{ placeholder: 'Email address', type: 'email' }} onChange={handleChange} />
```

---

### Pair 2 — Helper text for guidance; error text for failures only

**✅ Do** — Keep the two slots separate; toggle `hasError` only on validation failure.

```tsx
<label htmlFor="phone">Phone number</label>
<Input
  hasError={isInvalid}
  inputProps={{
    id: 'phone', type: 'tel',
    'aria-invalid': isInvalid ? 'true' : 'false',
    'aria-describedby': isInvalid ? 'phone-error' : 'phone-hint',
  }}
/>
{isInvalid
  ? <p id="phone-error" role="alert">Enter a valid 10-digit phone number.</p>
  : <p id="phone-hint">Format: 555-123-4567</p>}
```

**❌ Don't** — Place an error-style warning in the helper slot permanently.

---

### Pair 3 — Set `hasError` with `aria-invalid` and an associated error region

**✅ Do** — Bind the error message via `aria-errormessage` (or `aria-describedby`) with `role="alert"`.

```tsx
<Input
  hasError
  inputProps={{
    id: 'email', type: 'email',
    'aria-invalid': 'true',
    'aria-describedby': 'email-error',
    'aria-errormessage': 'email-error',
  }}
/>
<p id="email-error" role="alert">Please enter a valid email address.</p>
```

**❌ Don't** — Communicate failure with colour alone. Fails WCAG 1.4.1 and 4.1.3.

```tsx
{/* Wrong — red border, no message, no aria-invalid */}
<Input hasError inputProps={{ id: 'email', type: 'email' }} />
```

---

### Pair 4 — Pick `size` to match surface density; don't mix sizes per row

**✅ Do** — One size per form row.

```tsx
<div className="form-row">
  <Input size="medium" inputProps={{ id: 'first-name', placeholder: 'First name' }} />
  <Input size="medium" inputProps={{ id: 'last-name', placeholder: 'Last name' }} />
</div>
```

**❌ Don't** — Mix sizes in the same row. Misaligns baselines and reads as a layout bug.

---

### Pair 5 — Use `iconLeft` / `iconRight` semantically, not decoratively

**✅ Do** — Use a leading icon for a meaningful affordance (search, currency).

```tsx
import { SearchIcon } from '@8x8/oxygen-icons';
<Input
  iconLeft={SearchIcon}
  inputProps={{ id: 'filter', type: 'search', 'aria-label': 'Filter contacts' }}
  onChange={handleFilter}
/>
```

**❌ Don't** — Add a decorative icon with no functional or semantic meaning.

---

### Pair 6 — Mark required fields with both `isRequired` and `aria-required`

**✅ Do** — Set both; let the visual `*` stay decorative (`aria-hidden="true"` — handled internally).

```tsx
<label htmlFor="last-name">Last name</label>
<Input
  isRequired
  inputProps={{ id: 'last-name', name: 'lastName', 'aria-required': 'true' }}
/>
```

**❌ Don't** — Use only a visual `*` (no semantic) or only `aria-required` (no visible indicator).

---

### Pair 7 — Don't conflate `isDisabled` and `isReadOnly`

**✅ Do** — Use `isReadOnly` when the value matters but isn't editable; use `isDisabled` when the field doesn't apply.

```tsx
{/* Value must be visible and submitted — use read-only */}
<Input
  isReadOnly
  inputProps={{ id: 'account-email', value: user.email, readOnly: true, 'aria-readonly': 'true' }}
/>
{/* Field doesn't apply to user's tier — use disabled */}
<Input
  isDisabled
  inputProps={{ id: 'custom-domain', disabled: true, placeholder: 'Available on Enterprise plans' }}
/>
```

**❌ Don't** — Use `isDisabled` to display a meaningful non-editable value. Disabled removes it from the focus order and from form submission.

> ⚠ **Caveat (CONFLICT-001):** Whether `isReadOnly` is supported on Search input is unresolved. Pair 7 applies to Text input only.

---

### Pair 8 — Keep placeholder contrast within WCAG AA (or remove the placeholder)

**✅ Do** — Use label + helper text instead of a low-contrast placeholder. The default token pairing (`textColor02` / `ui05`) calculated at ~4.97:1 passes AA (4.5:1), but verify independently and prefer no placeholder for new designs.

**❌ Don't** — Ship placeholder as the sole prompt. Even where it passes AA, placeholder disappears on typing.

---

## Gaps

<!-- STUB:GAP-017 source="When CONFLICT-001 (Search input isReadOnly) is resolved: decide whether to (a) fold Search Do/Don't pairs into this doc or (b) author a separate Search-usage.md. TextArea usage is owned by component-lib/TextArea/." -->
