---
component: Label
package: "@8x8/oxygen-label"
category: data_display
role: accessibility
role_description: "Accessibility — ARIA roles, keyboard interactions, and WCAG 2.1 AA guidance"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Label/props]]"
  - "[[Label/examples]]"
  - "[[Label/tokens]]"
  - "[[Label/Label-figma]]"
  - "[[Label/label-pui]]"
  - "[[Label/label-audit]]"
tags:
  - oxygen
  - component/Label
  - role/accessibility
  - stage/blocked
  - category/data_display
---
# Label — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md)

## Overview

`Label` renders as an HTML `<label>` element. The MCP returned no explicit accessibility documentation for this component; guidance below is derived from the component's nature, HTML semantics, and WCAG 2.1 AA requirements.

## ARIA role

| Element | Role / Semantics |
|---------|-----------------|
| Root element | `<label>` (implicit `role="none"`, associates with a form control) |
| Info box trigger | Button (rendered as `<button>`) |

## Associating with a form control

Always provide `htmlFor` pointing to the `id` of the associated input. This is the primary accessibility hook:

```tsx
<Label value="Email" htmlFor="email" />
<Input id="email" />
```

When `htmlFor` is set, clicking the label moves focus to the associated control — the native browser behaviour of `<label>`.

## Required indicator

When `isRequired` is `true`, a visual required indicator is appended. Ensure the associated form validation message is also surfaced programmatically (e.g. via `aria-describedby` on the input).

## Disabled state

`isDisabled` visually mutes the label. It does not suppress assistive technology — screen readers will still announce the label text. Pair with `isDisabled` on the associated form control so the disabled state is conveyed through that control's `aria-disabled`.

## Info box

- `infoBoxButtonLabel` provides the accessible name for the info box trigger button. **Always supply this prop** when using `infoBoxText` — without it, the trigger button has no accessible label.
- `infoBoxShowOn` controls when the popover opens; for keyboard users, ensure the trigger is reachable by `Tab` and activatable by `Enter`/`Space`.

## Overflow tooltip

When `showTooltipOnOverflow` is `true`, a tooltip is shown for truncated text. Tooltips must be accessible to keyboard and screen reader users — verify that the tooltip content is announced by assistive technology.

## Keyboard interaction

| Key | Behaviour |
|-----|-----------|
| `Tab` | Moves focus to the info box trigger button (if present) |
| `Enter` / `Space` | Activates the info box trigger or action link |
| Click on label | Moves focus to the associated form control (`htmlFor`) |

## WCAG 2.1 AA checklist

| Criterion | Guidance |
|-----------|----------|
| 1.3.1 Info and Relationships | Use `htmlFor` to associate label with its control programmatically |
| 1.4.3 Contrast (Minimum) | `textColor01` provides sufficient contrast in both light and dark themes — verify with actual theme values |
| 2.1.1 Keyboard | Info box trigger and action link are keyboard-accessible |
| 2.4.6 Headings and Labels | Label text should be descriptive enough to identify the purpose of the associated control |
| 3.3.2 Labels or Instructions | Required fields should also communicate their required state to assistive technology |
| 4.1.2 Name, Role, Value | Info box trigger button must have `infoBoxButtonLabel` to meet this criterion |

_Source: Oxygen MCP · Extracted 2026-05-01_
