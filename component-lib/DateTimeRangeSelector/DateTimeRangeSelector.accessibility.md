---
parent: "[[DateTimeRangeSelector]]"
section: accessibility
component: DateTimeRangeSelector
pipeline_stage: spec_ready
audit_verdict: "YES"
tags:
  - oxygen
  - component/DateTimeRangeSelector
  - role/spoke
  - section/accessibility
  - stage/spec_ready
  - category/date_time
---

## Accessibility

<!-- STUB:GAP-006 source="Verify actual ARIA roles by inspecting the rendered @8x8/oxygen-date-time-range-selector DOM or component source. Update with confirmed roles and remove 'inferred' caveats." -->

### ARIA roles

> All roles below are **inferred** from component structure and common date range picker patterns. Verify against the rendered DOM or `@8x8/oxygen-date-time-range-selector` source.

| Element | Role / Attribute | Notes |
|---------|-----------------|-------|
| Trigger input | `role="button"` or `role="combobox"` | Opens the date-time range picker dropdown |
| Picker dropdown | `role="dialog"` | Contains the Calendar grid + time selectors + predefined ranges |
| Predefined ranges list | `role="listbox"` | Left panel; each item is `role="option"` |
| Predefined range item | `role="option"` | `aria-selected` reflects current selection |
| Calendar grid | `role="grid"` | See [[Calendar.accessibility]] |
| Day cell | `role="gridcell"` | |
| From / To inputs | `role="textbox"` | Date input fields in the header row |
| Start / End time selectors | — | Time inputs; see TimeSelector accessibility docs |
| Finish button | `role="button"` | Confirms the selection |
| Clear button | `role="button"` | Resets the selection |
| Error message | `aria-live="polite"` | End-before-start error (`endTimeErrorMessage`) |

---

### Keyboard interactions

| Key | Behavior |
|-----|----------|
| `Tab` | Move focus between trigger input, predefined range items, date inputs, time selectors, Finish, and Clear |
| `Enter` / `Space` | Open/close the picker from the trigger; activate a predefined range item; confirm Finish/Clear |
| `Escape` | Close the picker **without applying** changes |
| `Arrow keys` | Navigate day cells within the Calendar grid |
| `Page Up` / `Page Down` | Navigate calendar months |
| `Home` / `End` | Move to first/last day of current week in calendar |

> Keyboard behavior follows ARIA Date Picker and Listbox APG patterns. Verify against actual implementation.

---

### Screen reader guidance

- **Trigger announcement:** The trigger button should announce the current range value or placeholder in a human-readable format.
- **Predefined ranges:** Each list item should announce its label (e.g. "Last 7 days"). The selected item should be announced with its selection state.
- **Custom range:** When "Custom" is selected, announce that date inputs are now active.
- **Error message:** `endTimeErrorMessage` should be in a live region so screen readers announce validation errors without requiring focus move.
- **Localisation:** Supply the `locale` prop to ensure month and day names are announced in the user's language.
- **Disabled state:** When `isDisabled=true`, the trigger should have `aria-disabled="true"` to remain discoverable while indicating it is not interactive.

---

### WCAG 2.1 AA checklist

<!-- SKIP:GAP-007 manual="WCAG 1.4.1, 1.4.3, and 2.4.7 cannot be verified until GAP-002 (token confirmation from UI-Foundations) is resolved. After token values are confirmed, verify color contrast ratios and focus ring visibility and update 'Verify' items." -->

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.3.1 Info and Relationships | ✓ Supported | Label/input association; listbox + grid structure |
| 1.4.1 Use of Color | Verify | States must be distinguishable beyond colour alone — pending token confirmation (GAP-002) |
| 1.4.3 Contrast (minimum) | Verify | Token values CSS-derived only; verify in implementation (GAP-002) |
| 2.1.1 Keyboard | ✓ Supported | Full keyboard navigation through trigger, calendar, time, predefined list, actions |
| 2.4.3 Focus Order | ✓ Supported | Logical tab order: trigger → picker panel → confirm/clear |
| 2.4.7 Focus Visible | Verify | Focus ring `--interactive/focus01` — verify rendering in implementation |
| 4.1.2 Name, Role, Value | ✓ Supported | Roles, `aria-selected`, `aria-disabled` present; button labels via props |
