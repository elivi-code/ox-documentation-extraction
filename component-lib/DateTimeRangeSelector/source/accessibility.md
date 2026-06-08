---
component: DateTimeRangeSelector
package: "@8x8/oxygen-date-time-range-selector"
category: date_time
role: accessibility
role_description: "Accessibility specifications — ARIA roles, keyboard navigation, WCAG 2.1 AA"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: "YES"
siblings:
  - "[[DateTimeRangeSelector/props]]"
  - "[[DateTimeRangeSelector/examples]]"
  - "[[DateTimeRangeSelector/tokens]]"
  - "[[DateTimeRangeSelector/DateTimeRangeSelector-figma]]"
  - "[[DateTimeRangeSelector/DateTimeRangeSelector-usage]]"
  - "[[DateTimeRangeSelector/DateTimeRangeSelector-audit]]"
tags:
  - oxygen
  - component/DateTimeRangeSelector
  - role/accessibility
  - stage/spec_ready
  - category/date_time
---

# DateTimeRangeSelector — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md)

## ARIA roles

| Element | Role / Attribute | Notes |
|---------|-----------------|-------|
| Trigger input | `role="button"` or `role="combobox"` | Opens the date-time range picker dropdown |
| Picker dropdown | `role="dialog"` | Contains the Calendar grid + time selectors + predefined ranges |
| Predefined ranges list | `role="listbox"` | Left panel; each item is `role="option"` |
| Predefined range item | `role="option"` | `aria-selected` reflects current selection |
| Calendar grid | `role="grid"` | See Calendar accessibility docs |
| Day cell | `role="gridcell"` | |
| From / To inputs | `role="textbox"` | Date input fields in the header row |
| Start / End time selectors | — | Time inputs; see TimeSelector accessibility docs |
| Finish button | `role="button"` | Confirms the selection |
| Clear button | `role="button"` | Resets the selection |
| Error message | `aria-live="polite"` | End-before-start error (`endTimeErrorMessage`) |

> Note: ARIA roles are inferred from component structure and common date range picker patterns.
> Verify against the rendered DOM or `@8x8/oxygen-date-time-range-selector` source.

---

## Keyboard interactions

| Key | Behavior |
|-----|----------|
| `Tab` | Move focus between trigger input, predefined range items, date inputs, time selectors, Finish, and Clear |
| `Enter` / `Space` | Open/close the picker from the trigger; activate a predefined range item; confirm Finish/Clear |
| `Escape` | Close the picker without applying changes |
| `Arrow keys` | Navigate day cells within the Calendar grid |
| `Page Up` / `Page Down` | Navigate calendar months |
| `Home` / `End` | Move to first/last day of current week in calendar |

> Keyboard behavior follows ARIA Date Picker and Listbox APG patterns. Verify against actual implementation.

---

## Screen reader guidance

- **Trigger announcement**: The trigger button should announce the current range value or placeholder in a human-readable format.
- **Predefined ranges**: Each list item should announce its label (e.g. "Last 7 days"). The selected item should be announced with its selection state.
- **Custom range**: When "Custom" is selected, announce that date inputs are now active.
- **Error message**: `endTimeErrorMessage` should be in a live region so screen readers announce validation errors without requiring focus move.
- **Localisation**: Supply the `locale` prop to ensure month and day names are announced in the user's language.
- **Disabled state**: When `isDisabled=true`, the trigger should have `aria-disabled="true"` to remain discoverable while indicating it is not interactive.

---

## WCAG 2.1 AA checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.3.1 Info and Relationships | ✓ Supported | Label/input association; listbox + grid structure |
| 1.4.1 Use of Color | Verify | States must be distinguishable beyond colour alone |
| 1.4.3 Contrast (minimum) | Verify | Token values not exposed; verify in implementation |
| 2.1.1 Keyboard | ✓ Supported | Full keyboard navigation through trigger, calendar, time, predefined list, actions |
| 2.4.3 Focus Order | ✓ Supported | Logical tab order: trigger → picker panel → confirm/clear |
| 2.4.7 Focus Visible | Verify | Focus ring depends on token implementation (`--interactive/focus01`) |
| 4.1.2 Name, Role, Value | ✓ Supported | Roles, `aria-selected`, `aria-disabled` present; button labels via props |

---

_Source: Oxygen MCP · Extracted 2026-05-08_
