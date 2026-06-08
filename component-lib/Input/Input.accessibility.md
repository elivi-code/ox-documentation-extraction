---
parent: "[[Input]]"
section: accessibility
tags: [oxygen, component/Input, role/accessibility]
---

## ARIA roles

| Element | Role | Notes |
|---|---|---|
| Input field (`type="text"`) | `textbox` (implicit) | Native semantics — no explicit `role` needed |
| Input field (`type="search"`) | `searchbox` (implicit) | For Search input variant |
| Error message | `alert` or `aria-live="polite"` region | Announced when error appears |
| Required `*` | Decorative | `aria-hidden="true"` on visual `*`; use `aria-required="true"` on `<input>` |

---

## Keyboard interactions

| Key | Action |
|---|---|
| `Tab` | Move focus to input field |
| `Shift+Tab` | Move focus backward |
| Any printable key | Enters text |
| `Backspace` / `Delete` | Removes text |
| `Enter` | Submits enclosing `<form>` if present; no default on Input itself |
| `Escape` | Application-defined (e.g. clear and blur in a search bar) |

Search input additionally: `Enter` typically triggers search.

---

## Screen reader guidance

### Label association

```tsx
// ✅ Correct — htmlFor / id
<label htmlFor="username">Username</label>
<Input inputProps={{ id: 'username', name: 'username' }} />

// ✅ Correct — aria-labelledby
<span id="username-label">Username</span>
<Input inputProps={{ 'aria-labelledby': 'username-label' }} />

// ❌ Avoid — placeholder is not a label
<Input inputProps={{ placeholder: 'Username' }} />
```

### Placeholder text

**Figma annotation:** "Using placeholder text alone as a method to guide user input is not considered accessible, as it can disappear once the user starts typing."

- `hasPlaceholder=true` (Figma default) — legacy compatibility only
- `hasPlaceholder=false` — **recommended for all new designs**

### Helper text / hint

```tsx
<Input inputProps={{ id: 'email', 'aria-describedby': 'email-hint' }} />
<p id="email-hint">We'll use this to send your receipt.</p>
```

### Error messages

When `hasError=true`:
```tsx
<Input
  hasError
  inputProps={{
    'aria-invalid': 'true',
    'aria-describedby': 'email-error',
    'aria-errormessage': 'email-error',
  }}
/>
<p id="email-error" role="alert">Please enter a valid email address.</p>
```

**Figma behavior:** Error message stays visible during re-editing (Error+Focus state). Error only clears when value becomes valid.

### Required fields

```tsx
<Input
  isRequired
  inputProps={{ 'aria-required': 'true', id: 'name' }}
/>
```

Visual `*` is decorative (`aria-hidden="true"`) — handled internally by the component; verify in implementation.

### Read-only fields

```tsx
<Input
  isReadOnly
  inputProps={{ readOnly: true, 'aria-readonly': 'true', value: 'Non-editable value' }}
/>
```

### Disabled fields

```tsx
<Input isDisabled inputProps={{ disabled: true }} />
```

Disabled fields are not focusable. Use `isReadOnly` if the value must be communicated to screen reader users.

---

## Focus management

- Focus ring: blue border (`interactive/focus01` `#0056E0` Light / `#D7E3F9` Dark) on field
- Visible in both Rest→Focus and Error→Focus transitions
- Error+Focus: blue ring overrides red border; error message stays visible
- Never suppress focus ring with `outline: none` — required by WCAG 2.4.7

---

## Color contrast

| Element | Foreground | Background | Result |
|---|---|---|---|
| Label text | `textColor01` (#26252A) | Page bg | ✅ Very dark — passes |
| Placeholder text | `textColor02` (#6C6862) | `ui05` (#F4F3EE) | ✅ **~4.97:1 PASS** (calculated; verify independently) |
| Helper text | `textColor02` (#6C6862) | Page bg | ⚠ Verify against page background |
| Error text | `error01` (#CB2233) | Page bg | ⚠ Verify against WCAG AA 4.5:1 |
| Required `*` | `error01` (#CB2233) | Page bg | ⚠ Verify |
| Focus ring | `interactive/focus01` (#0056E0) | `ui05` (#F4F3EE) | ✅ **~5.54:1 PASS** (calculated; WCAG 1.4.11 ≥ 3:1) |

<!-- STUB:GAP-013 source="Formally verify focus ring contrast once tokens.md is updated with interactive/focus01 binding (calculated ~5.54:1 from Input-figma.md data — appears to pass 3:1 threshold)" -->

---

## WCAG 2.1 AA checklist

| Criterion | Requirement | Status |
|---|---|---|
| 1.1.1 Non-text content | Input has accessible label | ✅ `aria-label` / `<label>` required |
| 1.3.1 Info and relationships | Label programmatically associated | ✅ `htmlFor` / `aria-labelledby` |
| 1.3.5 Identify input purpose | `autocomplete` where appropriate | ⚠ Use `inputProps.autoComplete` |
| 1.4.3 Contrast (minimum) | Text contrast ≥ 4.5:1 | ✅ Placeholder ~4.97:1 PASS (#6C6862 / #F4F3EE, calculated) |
| 1.4.4 Resize text | Input resizes to 200% zoom | ⚠ Verify no overflow |
| 1.4.11 Non-text contrast | Focus ring ≥ 3:1 | ✅ Focus ring ~5.54:1 PASS (calculated from figma.md data) |
| 2.1.1 Keyboard | All functions via keyboard | ✅ Native input keyboard support |
| 2.4.3 Focus order | Logical focus sequence | ✅ DOM order |
| 2.4.7 Focus visible | Focus ring visible | ✅ Blue focus ring in Figma |
| 3.3.1 Error identification | Error described in text | ✅ Error message text required |
| 3.3.2 Labels or instructions | Label + optional hint text | ✅ Required in implementation |
| 3.3.3 Error suggestion | Error message suggests correction | ⚠ Application-level responsibility |
| 4.1.2 Name, role, value | `textbox` / `searchbox` role, state exposed | ✅ Native HTML semantics |
| 4.1.3 Status messages | Error `role=alert` | ✅ `role="alert"` on error message |

---

## Figma accessibility examples (node `65777:2179`)

Three documented scenarios:

1. **Input Field Error State** — blue focus ring + error message visible simultaneously during Error+Focus state
2. **Required Field** — flow: Rest → Focus → Typing → Error (invalid) → Re-focus → Correction → clear
3. **Form Validation States** — real-time (on blur) + submit-time (summary component at bottom of form)
4. **hasPlaceholder prop** — `false` = label + helper text (recommended); `true` = legacy placeholder retained
