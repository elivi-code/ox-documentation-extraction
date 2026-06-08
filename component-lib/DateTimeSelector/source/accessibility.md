---
component: DateTimeSelector
package: "@8x8/oxygen-date-time-selector"
category: date_time
role: accessibility
role_description: "Accessibility specifications — ARIA roles, keyboard navigation, WCAG 2.1 AA"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: "YES"
siblings:
  - "[[DateTimeSelector/props]]"
  - "[[DateTimeSelector/examples]]"
  - "[[DateTimeSelector/tokens]]"
  - "[[DateTimeSelector/DateTimeSelector-figma]]"
  - "[[DateTimeSelector/DateTimeSelector-usage]]"
  - "[[DateTimeSelector/DateTimeSelector-audit]]"
tags:
  - oxygen
  - component/DateTimeSelector
  - role/accessibility
  - stage/spec_ready
  - category/date_time
---

# DateTimeSelector — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md)

## ARIA roles

| Element | Role / Attribute | Notes |
|---------|-----------------|-------|
| Trigger button | `role="button"` | Opens the date/time picker overlay |
| Picker overlay | `role="dialog"` | Modal/popup containing the Calendar + time input |
| Selected date display | `aria-live="polite"` | Announce date selection changes |
| Clear button | `aria-label` | Label must describe "Clear date" action |
| Finish/confirm button | `role="button"` | Closes picker and confirms selection |
| Loading state | `aria-busy="true"` | Set on the container when `isLoading` is true |

> Note: ARIA roles above are inferred from component structure and common date picker patterns.
> Verify against the rendered DOM or `@8x8/oxygen-date-time-selector` source.

---

## Keyboard interactions

| Key | Behavior |
|-----|----------|
| `Tab` | Move focus to/from the trigger button; tab through overlay controls when open |
| `Enter` / `Space` | Open/close the picker overlay from the trigger; confirm selection |
| `Escape` | Close the picker overlay without confirming |
| Arrow keys | Navigate days within the embedded Calendar grid |
| `Page Up` / `Page Down` | Navigate months within the Calendar |

> Keyboard behavior follows the ARIA Date Picker APG pattern. Verify against actual implementation.

---

## Screen reader guidance

- **Value display**: Ensure the trigger button announces the selected date in a human-readable format, not raw ISO date strings.
- **Loading state**: Set `aria-busy="true"` and provide `loadingMessage` to describe what is being fetched.
- **Clear action**: When `isClearable` is `true`, the clear button must have an `aria-label` such as `"Clear selected date"`.
- **Overlay announcement**: The picker overlay should be announced as a dialog with a descriptive `aria-label` or `aria-labelledby` referencing the field label.

---

## WCAG 2.1 AA checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.3.1 Info and Relationships | ✓ Supported | Label/input association; calendar grid structure |
| 1.4.1 Use of Color | Verify | States must be distinguishable beyond color alone |
| 1.4.3 Contrast (minimum) | Verify | Token values not exposed; verify in implementation |
| 2.1.1 Keyboard | ✓ Supported | Trigger, calendar navigation, confirm/clear fully keyboard operable |
| 2.4.3 Focus Order | ✓ Supported | Logical tab order through trigger → overlay → confirm/clear |
| 2.4.7 Focus Visible | Verify | Focus ring depends on token implementation |
| 4.1.2 Name, Role, Value | ✓ Supported | Trigger, calendar cells, and action buttons carry roles and labels |

---

_Source: Oxygen MCP · Extracted 2026-05-08_
