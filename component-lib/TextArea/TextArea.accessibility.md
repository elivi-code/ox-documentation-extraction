---
parent: "[[TextArea]]"
section: accessibility
pipeline_stage: draft
audit_verdict: partial
tags:
  - oxygen
  - component/TextArea
  - section/accessibility
---

## ARIA role

The Oxygen `Textarea` renders a native HTML `<textarea>` element. No explicit `role` attribute is needed — the browser assigns the implicit ARIA role of `textbox` with `aria-multiline="true"` automatically.

> No explicit ARIA role annotations were found in the Figma file. The guidance below is inferred from the component type (native multiline text input).

---

## Labelling

The Figma design shows a visible label rendered as a sibling element above the input field. In code, this label must be associated programmatically with the textarea:

```tsx
{/* Option 1 — htmlFor + id */}
<label htmlFor="message">Label</label>
<Textarea id="message" />

{/* Option 2 — aria-label (no visible label) */}
<Textarea aria-label="Message" />

{/* Option 3 — aria-labelledby */}
<span id="msg-label">Label</span>
<Textarea aria-labelledby="msg-label" />
```

The Oxygen `Textarea` component does not render its own `<label>` element — labelling is the consumer's responsibility.

---

## Hint and error text

The Figma design includes optional hint text below the input and an error message area (with triangle icon). These must be linked to the textarea for screen readers:

```tsx
<Textarea
  id="message"
  aria-describedby="message-hint message-error"
  hasError={hasError}
  aria-invalid={hasError ? 'true' : undefined}
/>
<span id="message-hint">This is a hint to help users.</span>
{hasError && (
  <span id="message-error" role="alert">Error message goes here.</span>
)}
```

- Use `aria-describedby` to reference both hint and error IDs.
- Use `role="alert"` on the error message container so it is announced immediately when it appears.

---

## Keyboard interactions

| Key | Behavior |
|-----|----------|
| `Tab` | Moves focus to/from the textarea |
| `Shift+Tab` | Moves focus backwards |
| Typing | Inserts character at cursor |
| `Enter` | Inserts newline (multiline) |
| `Home` / `End` | Move cursor to start/end of line |
| `Ctrl+A` | Select all text |
| `Ctrl+Z` | Undo |
| `Escape` | No built-in behavior — consumers can add `onKeyDown` to blur |

---

## Focus indicator

The Figma focus state shows a 2px solid ring in `--interactive/focus01` (`#0056e0`) applied as an absolute overlay inside the input container (border-radius 6px). This meets WCAG 2.1 SC 2.4.11 (Focus Appearance).

---

## Disabled state

- Set `isDisabled={true}` — this maps to the HTML `disabled` attribute on the underlying `<textarea>`.
- Disabled elements are excluded from the tab order automatically.
- Screen readers announce the element as "dimmed" or "unavailable" — do not additionally hide with `aria-hidden`.

---

## Read-only state

- Set `isReadOnly={true}` — this maps to the HTML `readonly` attribute.
- Read-only textareas remain in the tab order and are announced as "read only" by screen readers.
- Unlike disabled, read-only text can be selected and copied.

---

## Error state

- Set `hasError={true}` — applies a red border (visual indicator only).
- Also set `aria-invalid="true"` — the standard ARIA attribute for marking an invalid form field. Screen readers announce it as "invalid entry" or equivalent before the field label.
- Screen readers do not announce the border change alone. Always pair with a visible error message linked via `aria-describedby` and `role="alert"`.
- The Figma design uses an error triangle icon + error text below the field. The icon is decorative (`aria-hidden="true"`) and the text carries the message.

```tsx
<Textarea
  id="message"
  hasError={hasError}
  aria-invalid={hasError ? 'true' : undefined}
  aria-describedby={hasError ? 'message-error' : undefined}
/>
{hasError && (
  <span id="message-error" role="alert">
    Error message goes here.
  </span>
)}
```

---

## Required field

- The Figma design shows a red `*` asterisk next to the label for required fields.
- Mark required fields with the HTML `required` attribute and `aria-required="true"` (or just `required` on the native `<textarea>`).
- The `*` in the label should be supplemented with `aria-label` or screen-reader-only text like `(required)` — asterisks alone are not reliably announced by all screen readers.

---

## WCAG 2.1 AA Checklist

| Criterion | Level | Status | Notes |
|-----------|-------|--------|-------|
| 1.3.1 Info and Relationships | A | ✅ Supported | `<textarea>` carries semantic role; label association is consumer's responsibility |
| 1.4.3 Contrast (Minimum) | AA | ✅ Passes | Label `#26252a` on white, placeholder `#6c6862` on `#f4f3ee` pass AA. Disabled text `#8d8b7e` on `#c8c8bd` ≈ 1.9:1 — below the 3:1 threshold for normal text, but **explicitly exempt** under WCAG 1.4.3 Note 1 (inactive UI components have no contrast requirement) |
| 1.4.11 Non-text Contrast | AA | ✅ Passes | Focus ring `#0056e0` on `#f4f3ee` background; error border `#cb2233` on `#f4f3ee` |
| 2.1.1 Keyboard | A | ✅ Supported | Native `<textarea>` is fully keyboard operable |
| 2.4.3 Focus Order | A | ✅ Supported | Follows DOM order; disabled removes from tab order |
| 2.4.7 Focus Visible | AA | ✅ Supported | 2px focus ring applied in Focus state (Figma annotated) |
| 2.4.11 Focus Appearance | AA | ✅ Supported | Focus ring meets minimum area and contrast requirements |
| 3.3.1 Error Identification | A | ⚠️ Consumer responsibility | `hasError` adds visual border + `aria-invalid`; consumer must provide accessible error message via `aria-describedby` + `role="alert"` |
| 3.3.2 Labels or Instructions | A | ⚠️ Consumer responsibility | Component does not render `<label>`; consumer must provide programmatic label |
| 4.1.2 Name, Role, Value | A | ✅ Supported | Native `<textarea>` provides implicit role and value; name via `aria-label` / `aria-labelledby` is consumer's responsibility |

---

## Screen reader guidance

- **VoiceOver / NVDA:** announces "Label, required, text area" (when `id` + `<label for>` + `required` are set correctly).
- **Invalid state:** announces "invalid entry" or equivalent before the label when `aria-invalid="true"` is set.
- **Hint text:** announced when user focuses and `aria-describedby` points to hint element.
- **Error text:** announced immediately on appearance when `role="alert"` is used.
- **Disabled:** announced as "dimmed" (macOS VoiceOver) or "unavailable" (NVDA).
- **Read-only:** announced as "read only" before the field description.

---

_Source: Oxygen MCP + Figma MCP (accessibility annotations not present in Figma — guidance inferred from component type) · Extracted 2026-04-29 · DOC_GAP fixes applied (GAP-003, GAP-010) 2026-06-05_
