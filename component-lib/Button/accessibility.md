---
component: Button
package: "@8x8/oxygen-button"
category: interaction
role: accessibility
role_description: "Accessibility — ARIA roles, keyboard interactions, and WCAG 2.1 AA guidance"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Button/props]]"
  - "[[Button/examples]]"
  - "[[Button/tokens]]"
  - "[[Button/Button-figma]]"
  - "[[Button/Button-usage]]"
  - "[[Button/Button-audit]]"
tags:
  - oxygen
  - component/Button
  - role/accessibility
  - stage/blocked
  - category/interaction
---
# Button — Accessibility

> **See also:** [Props](props.md) · [Examples](examples.md) · [Tokens](tokens.md) · [Usage](Button-usage.md)

## ARIA Role

The `Button` component renders a native `<button>` element, which carries the implicit ARIA role of `button`. No additional `role` attribute is needed.

---

## Keyboard Interactions

| Key | Behaviour |
|-----|-----------|
| `Tab` | Moves focus to the button (including disabled buttons — see note below) |
| `Shift + Tab` | Moves focus away from the button |
| `Enter` | Activates the button; submits a form if `type="submit"` |
| `Space` | Activates the button |

---

## Disabled State

The Oxygen `Button` uses the `isDisabled` prop rather than the native HTML `disabled` attribute. This means:

- The button **remains focusable** (it does not leave the tab order).
- **Form submission is not fired** when a disabled button is clicked.
- Screen readers will still announce the button; ensure the surrounding context makes the disabled reason clear.

```tsx
// Disabled button is focusable but does not submit the form
<form onSubmit={() => alert('submit')}>
  <Button type="submit" isDisabled>Submit</Button>
</form>
```

> Avoid disabling buttons without providing clear guidance on how the user can enable them (see Best Practices).

---

## Screen Reader Guidance

| Scenario | Recommendation |
|----------|---------------|
| Button with text label | No extra annotation needed — label is the accessible name |
| `isCircular` / icon-only `Button` | Pass a descriptive `aria-label` or wrap with `Tooltip` |
| `IconButton` | Always pair with `<Tooltip title="…">` — the tooltip text serves as the accessible name |
| `DropdownButton` | Ensure the popover/menu it opens is correctly linked with `aria-controls` and `aria-expanded` |
| Destructive action | Confirm dialog pattern is recommended; announce consequence in button label or `aria-describedby` |

### IconButton + Tooltip pattern

```tsx
import Tooltip from '@8x8/oxygen-tooltip';
import { IconButton } from '@8x8/oxygen-button';
import { AddReactionIcon } from '@8x8/oxygen-icon';

<Tooltip title="Add reaction">
  <IconButton>
    <AddReactionIcon />
  </IconButton>
</Tooltip>
```

---

## WCAG 2.1 AA Checklist

| Criterion | Requirement | Notes |
|-----------|-------------|-------|
| 1.4.3 Contrast (Minimum) | Text contrast ≥ 4.5:1 | Handled by Oxygen tokens; verify custom `theme` overrides |
| 1.4.11 Non-text Contrast | UI component contrast ≥ 3:1 against adjacent colour | Button border/background against page background |
| 2.1.1 Keyboard | All functionality operable via keyboard | Native `<button>` satisfies this |
| 2.4.3 Focus Order | Focus order is logical | Tab order follows DOM order; use `ButtonGroup` for grouping |
| 2.4.7 Focus Visible | Focus indicator must be visible | Oxygen provides a default focus ring; do not suppress with `outline: none` |
| 4.1.2 Name, Role, Value | Every button has an accessible name | Text buttons: label text; icon-only: `aria-label` or Tooltip |
| 2.4.6 Headings and Labels | Labels are descriptive | Use clear action verbs (e.g. "Delete file", not just "Delete") |
| 3.2.2 On Input | Buttons should not trigger unexpected context changes | Destructive actions should be preceded by confirmation |

---

## Best Practices

- **Label clarity:** Use sentence-style action verbs ("Save changes", "Delete account"). Avoid vague labels like "OK" or "Click here".
- **Icon-only buttons:** Always provide an accessible name via `aria-label` or a `Tooltip`. Users relying on screen readers or switch controls cannot interpret icons alone.
- **Destructive actions:** Add a confirmation step (e.g. modal) before executing irreversible operations. Consider `aria-describedby` pointing to a warning message.
- **Disabled buttons:** Prefer keeping buttons enabled and showing inline validation errors rather than disabling without explanation.
- **One primary button:** Do not place more than one primary button per section or dialog — this preserves a clear focal point for keyboard and AT users.
- **Button vs. link:** Use `Button` for actions; use `TextLink` for navigation. Do not style a link as a button or vice versa — the semantics matter for screen readers.

---

_Source: Oxygen MCP · Extracted 2026-04-28_
