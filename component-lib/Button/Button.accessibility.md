---
parent: "[[Button]]"
section: accessibility
component: Button
package: "@8x8/oxygen-button"
tags: [oxygen, component/Button, role/accessibility, section/accessibility]
---

# Button — Accessibility

## ARIA Role

`Button` renders a native `<button>` element with the implicit ARIA role `button`. No `role` attribute is needed.

---

## Keyboard Interactions

| Key | Behaviour |
|-----|-----------|
| `Tab` | Moves focus to the button (including disabled buttons — see note) |
| `Shift + Tab` | Moves focus away from the button |
| `Enter` | Activates the button; submits a form if `type="submit"` |
| `Space` | Activates the button |

---

## Disabled State

Oxygen `Button` uses the `isDisabled` prop, not the native HTML `disabled` attribute:

- The button **remains focusable** (does not leave the tab order).
- **Form submission is not fired** when a disabled button is clicked.
- Screen readers still announce the button; make the disabled reason clear in surrounding context.

```tsx
<form onSubmit={() => alert('submit')}>
  <Button type="submit" isDisabled>Submit</Button>
</form>
```

---

## Screen Reader Guidance

| Scenario | Recommendation |
|----------|---------------|
| Button with text label | No extra annotation — label is the accessible name |
| `isCircular` / icon-only `Button` | Pass a descriptive `aria-label` or wrap with `Tooltip` |
| `IconButton` | Always pair with `<Tooltip title="…">` — tooltip text is the accessible name |
| `DropdownButton` | Link the popover/menu with `aria-controls` and `aria-expanded` |
| Destructive action | Confirm-dialog pattern; announce consequence in label or `aria-describedby` |
| Toggle button (`isActive`) | Set `aria-pressed={isActive}` so AT announces the pressed/unpressed state |

### IconButton + Tooltip pattern

```tsx
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
| 1.4.11 Non-text Contrast | UI component contrast ≥ 3:1 | Button border/background vs page background |
| 2.1.1 Keyboard | All functionality operable via keyboard | Native `<button>` satisfies this |
| 2.4.3 Focus Order | Focus order is logical | Tab order follows DOM order; use `ButtonGroup` for grouping |
| 2.4.7 Focus Visible | Focus indicator visible | Default focus ring — never suppress with `outline: none` |
| 4.1.2 Name, Role, Value | Every button has an accessible name | Text: label; icon-only: `aria-label`/Tooltip |
| 2.4.6 Headings and Labels | Labels are descriptive | Use action verbs ("Delete file", not "Delete") |
| 3.2.2 On Input | No unexpected context changes | Destructive actions preceded by confirmation |

> ⚠️ **WARN-002:** WCAG 2.5.3 (Label in Name) is not in the checklist. Icon buttons with both a visible tooltip and `aria-label` should have matching values to satisfy it. Advisory.

---

## Best Practices

- **Label clarity:** sentence-style action verbs ("Save changes"). Avoid "OK" or "Click here".
- **Icon-only buttons:** always provide an accessible name via `aria-label` or `Tooltip`.
- **Destructive actions:** add a confirmation step before irreversible operations; consider `aria-describedby`.
- **Disabled buttons:** prefer keeping enabled and showing inline validation errors over disabling without explanation.
- **One primary button** per section or dialog — preserves a clear focal point.
- **Button vs. link:** `Button` for actions, `TextLink` for navigation — the semantics matter for screen readers.
