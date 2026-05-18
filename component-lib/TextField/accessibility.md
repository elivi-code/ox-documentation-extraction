---
component: TextField
package: "@8x8/oxygen-textField"
category: form_inputs
role: accessibility
role_description: "Accessibility — ARIA roles, keyboard interactions, and WCAG 2.1 AA guidance"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[TextField/props]]"
  - "[[TextField/examples]]"
  - "[[TextField/tokens]]"
  - "[[TextField/figma]]"
  - "[[TextField/TextField-pui]]"
  - "[[TextField/TextField-audit]]"
tags:
  - oxygen
  - component/TextField
  - role/accessibility
  - stage/spec_ready
  - category/form_inputs
---
# TextField — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md) · [figma.md](figma.md)

## ARIA roles & semantics

- Renders a native `<input>` element — inherits implicit `role="textbox"`.
- When `isRequired` is set, the `required` attribute must be present on the input; the visual `*` beside the label is supplementary and should not be the only indicator.
- When `hasError` is set, associate the error message with the input via `aria-describedby` pointing to the error text element's `id`.
- The hint/description text (`description` prop) should also be linked via `aria-describedby`.
- When `isReadOnly` is set, the `readonly` attribute is present; the browser announces this to screen readers automatically.
- When `isDisabled` is set, the `disabled` attribute is present; disabled fields are removed from the tab order and not announced as interactive.
- `label` renders a `<label>` element associated with the input via `for`/`id`. Always provide a `label` or a visible alternative; never rely on `placeholder` alone as a label.

## Keyboard interactions

| Key | Behaviour |
|-----|-----------|
| `Tab` | Moves focus to the input |
| `Shift + Tab` | Moves focus away |
| Any printable key | Types into the field |
| `Backspace` / `Delete` | Removes characters |
| `Home` / `End` | Moves caret to start/end of value |
| `Arrow Left / Right` | Moves caret within value |
| `Ctrl/Cmd + A` | Selects all text |

## Focus indicator

- Focus ring is a **2px solid border** using `--interactive/focus01` (`#0056E0` light, `#D7E3F9` dark) rendered as an absolute overlay inside the input container.
- Focus must be visible at all times and must not be suppressed for keyboard-only flows.

## Screen reader guidance

- Announce the label, required state, current value, and any hint/error text when the field receives focus.
- Error messages linked via `aria-describedby` are announced immediately when the field is focused in the error state.
- Placeholder text is read by most screen readers but is not a substitute for a persistent label.
- The info icon button beside the label (`infoBoxText` / `infoBoxButtonLabel`) must have an accessible name (set via `aria-label` through `inputProps` if not provided by default).

## WCAG 2.1 AA checklist

| Criterion | Requirement | Notes |
|-----------|-------------|-------|
| 1.3.1 Info and Relationships | Labels must be programmatically associated | Use `label` prop; do not use placeholder-only labelling |
| 1.3.3 Sensory Characteristics | Error state must not rely on colour alone | Error border + icon + error text all present in `hasError` state |
| 1.4.1 Use of Colour | Disabled / error states must not rely on colour alone | Disabled state should also use reduced opacity or visual pattern |
| 1.4.3 Contrast (Minimum) | Text contrast ≥ 4.5:1 | `textColor01` (#26252A on `#F4F3EE`) passes; verify dark mode |
| 1.4.4 Resize Text | Input text must scale to 200% without loss of content | Use relative units; avoid overflow:hidden on input containers |
| 2.1.1 Keyboard | All functionality accessible via keyboard | ✓ Native `<input>` |
| 2.4.3 Focus Order | Focus order must be logical | ✓ Follow DOM order |
| 2.4.7 Focus Visible | Focus indicator must be visible | ✓ 2px focus ring |
| 3.3.1 Error Identification | Errors must be described in text | Use `hasError` + `description` with error message |
| 3.3.2 Labels or Instructions | Provide labels for all inputs | ✓ `label` prop required; hint via `description` |
| 4.1.2 Name, Role, Value | Input name, role, and state must be programmatically determinable | ✓ Native `<input>` with label association |

## Disabled state guidance

Disabled inputs (`isDisabled`) are not keyboard-reachable. If users need to see the value but not edit it, prefer `isReadOnly` instead, which keeps the field in the tab order and is announced by screen readers.

_Source: Oxygen MCP + Figma (inferred from component nature) · Extracted 2026-04-29_
