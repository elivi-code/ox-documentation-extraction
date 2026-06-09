---
parent: "[[Label]]"
section: accessibility
---

<!-- STUB:GAP-010 source="Designer must add accessibility annotations to the Figma _base_form_label component — ARIA role, focus order, and keyboard interaction annotations are absent (confirmed via annotations: [] from Desktop Bridge)" -->

## ARIA role

| Element | Role / Semantics |
|---------|-----------------|
| Root element | `<label>` (implicit `role="none"`; associates with a form control) |
| Info box trigger | Button (rendered as `<button>`) |

> All accessibility content below is inferred from the component's nature, HTML semantics, and WCAG 2.1 AA requirements — the MCP returned no explicit accessibility documentation for this component (GAP-011).

## Associating with a form control

Always provide `htmlFor` pointing to the `id` of the associated input:

```tsx
<Label value="Email" htmlFor="email" />
<Input id="email" />
```

When `htmlFor` is set, clicking the label moves focus to the associated control. Screen readers announce the label text when the user reaches that control.

## Required indicator

When `isRequired` is `true`, a visual required indicator is appended. The asterisk is a **visual signal only** — ensure the required state is also surfaced programmatically:

```tsx
<Label value="Password" htmlFor="password" isRequired />
<Input id="password" type="password" aria-required="true" />
```

## Disabled state

`isDisabled` visually mutes the label. It does not suppress assistive technology — screen readers still announce the label text. Pair with `isDisabled` on the associated form control so AT hears the constraint through the control's `aria-disabled`.

> **Note (GAP-012):** The disabled color token(s) are unknown — the MCP did not return them and Figma has no disabled variant for this component.

## Info box

- `infoBoxButtonLabel` provides the accessible name for the info box trigger button. **Always supply this prop** when using `infoBoxText` — without it the trigger has no accessible label and fails WCAG 4.1.2.
- `infoBoxShowOn` controls when the popover opens. For keyboard users, verify the trigger is reachable by `Tab` and activatable by `Enter`/`Space`.

## Overflow tooltip

When `showTooltipOnOverflow` is `true`, verify that the tooltip content is announced by assistive technology and reachable without a pointer device.

## Keyboard interaction

| Key | Behaviour |
|-----|-----------|
| `Tab` | Moves focus to the info box trigger button (if present) |
| `Enter` / `Space` | Activates the info box trigger or inline action link |
| Click on label | Moves focus to the associated form control (`htmlFor`) |

## WCAG 2.1 AA checklist

| Criterion | Guidance |
|-----------|----------|
| 1.3.1 Info and Relationships | Use `htmlFor` to associate label with its control programmatically |
| 1.4.3 Contrast (Minimum) | `text/textColor01` provides sufficient contrast in both themes — verify with actual token values |
| 2.1.1 Keyboard | Info box trigger and action link are keyboard-accessible |
| 2.4.6 Headings and Labels | Label text should be descriptive enough to identify the associated control's purpose |
| 3.3.2 Labels or Instructions | Required fields must also communicate the required state to AT |
| 4.1.2 Name, Role, Value | Info box trigger must have `infoBoxButtonLabel` to meet this criterion |

_Source: Oxygen MCP · Inferred from component semantics · Extracted 2026-05-01_
