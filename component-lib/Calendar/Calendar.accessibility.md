---
parent: "[[Calendar]]"
section: accessibility
---

## Accessibility

### ARIA roles

<!-- STUB:GAP-009 source="Verify the actual ARIA role for the Calendar root by inspecting rendered DOM or @8x8/oxygen-calendar source — currently documented as implementation-defined (application | group)." -->

| Element | Role / Attribute | Notes |
|---------|-----------------|-------|
| Calendar root | `role="application"` or `role="group"` (implementation-defined) | Provides a labelled boundary for the date picker widget |
| Month grid | `role="grid"` | Each month rendered as a grid of cells |
| Day cell | `role="gridcell"` | Individual selectable day |
| Day button | `role="button"` | Clickable/keyboard-activatable day; receives focus |
| Disabled day | `aria-disabled="true"` | Not `disabled` — remains in tab order so screen readers can announce it with tooltip text |
| Today | `aria-current="date"` | Marks today's date |
| Selected date | `aria-selected="true"` | Marks the selected date (single mode) or start/end of range |
| Month/year pickers | `role="combobox"` or `role="listbox"` | Navigation dropdowns |
| Prev/next arrows | `aria-label` via `prevMonthLabel` / `nextMonthLabel` props | Must be set for meaningful screen reader announcements |
| Live region | `aria-live="polite"` | Announce selected date changes to assistive technology (implement in the consuming page, not inside Calendar) |

### Keyboard interactions

| Key | Behavior |
|-----|----------|
| `Tab` | Move focus between navigation controls, month/year pickers, and the day grid |
| `Arrow keys` | Navigate between day cells within the grid |
| `Enter` / `Space` | Select the focused day (fires `onDateChange` or sets range boundary) |
| `Escape` | Close any open month/year picker dropdown |
| `Page Up` | Go to previous month |
| `Page Down` | Go to next month |
| `Home` | Move focus to the first day of the current week |
| `End` | Move focus to the last day of the current week |

> Keyboard behavior above follows the [ARIA Date Picker pattern](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/examples/datepicker-dialog/). Verify against the actual implementation — the `Day` component's `onClick` fires on both click and Enter/Space per prop documentation.

### Screen reader guidance

- **Disabled dates**: `disabledDateTooltip` returns a string read by screen readers when the user navigates to a disabled cell. Pass meaningful messages (e.g. _"This date is outside the allowed booking window"_).
- **Prev/next month**: Always supply `prevMonthLabel` and `nextMonthLabel` props with localised strings (e.g. `"Previous month"`, `"Next month"`).
- **Locale**: Use the `locale` prop to ensure month and day names are announced in the user's language.
- **Live announcements**: Wrap the Calendar in a consuming component that announces the selected date/range via `aria-live="polite"` so users know their selection was registered.

### WCAG 2.1 AA checklist

<!-- SKIP:GAP-010 manual="WCAG 1.4.3 Contrast and 2.4.7 Focus Visible marked 'Verify' — cannot be confirmed without resolved token values. Blocked on GAP-002 / GAP-007 (token resolution from UI-Foundations)." -->

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.3.1 Info and Relationships | ✓ Supported | Grid structure conveys day relationships |
| 1.4.1 Use of Color | ✓ Supported | States differentiated beyond color (focus ring, aria attributes) |
| 1.4.3 Contrast (minimum) | ⏳ Verify | Token values not exposed; blocked on token resolution (GAP-002/007) |
| 2.1.1 Keyboard | ✓ Supported | Full keyboard navigation via arrow keys + Enter/Space |
| 2.4.3 Focus Order | ✓ Supported | Logical tab order through controls |
| 2.4.7 Focus Visible | ⏳ Verify | Focus ring styling depends on token implementation; blocked on token resolution (GAP-002/007) |
| 4.1.2 Name, Role, Value | ✓ Supported | ARIA roles, `aria-selected`, `aria-disabled` present; `aria-label` required on nav buttons |

> ⚠️ Keyboard behavior (Page Up/Down, Home/End) is documented from the ARIA Date Picker APG pattern, not yet confirmed against the `@8x8/oxygen-calendar` implementation — spot-check before publishing (WARN-001).
