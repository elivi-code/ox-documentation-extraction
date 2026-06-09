---
parent: "[[TimeSelector]]"
section: accessibility
component: TimeSelector
pipeline_stage: draft
tags:
  - oxygen
  - component/TimeSelector
  - role/spoke
  - section/accessibility
  - category/date_time
---

> **Data note:** The OX MCP returned no explicit accessibility documentation for this component. Figma annotations contain no ARIA or keyboard interaction notes. All guidance below is derived from the component's interactive nature as a time-picker input — verify against the live Storybook and rendered DOM before shipping.

<!-- STUB:GAP-008 source="Audit the live component's rendered HTML for actual ARIA roles and attributes; confirm keyboard behaviour in browser; update source/accessibility.md with verified data. All current content is inferred from time-picker conventions and is not sourced from OX MCP or Figma annotations." -->

---

## ARIA role

The TimeSelector is a composite interactive widget. Expected roles:

- The visible input field should carry `role="combobox"` or render as a native `<input type="text">` with associated `aria-haspopup` pointing to the dropdown.
- When the picker dropdown is open, `aria-expanded="true"` should be set on the trigger.
- Associate the visible **Label** with the input via `for`/`id` or `aria-labelledby`.
- Associate the **hint text** with the input via `aria-describedby`.
- When `hasError` is true, the error message should be associated via `aria-describedby` and `aria-invalid="true"` should be present on the input.

> **Gap (GAP-008):** The OX MCP and Figma annotations do not confirm the exact ARIA implementation. Verify against the live Storybook and rendered DOM.

---

## Keyboard interactions

| Key | Behaviour |
|-----|-----------|
| `Tab` | Move focus to/from the TimeSelector input |
| `Enter` / `Space` | Open the time picker dropdown |
| `Escape` | Close the dropdown, return focus to the input |
| `Arrow Up` / `Arrow Down` | Navigate through time options in the open dropdown |
| `Tab` (within dropdown) | Move between hour, minute, AM/PM columns |

> **Gap (GAP-008):** Keyboard behaviour above is inferred from time-picker conventions. No authoritative keyboard map was found in MCP or Figma annotations.

---

## Focus management

- The input shows a **Focus ring** overlay using `--interactive/focus01` (#0056e0, 2 px solid) — visible in the Figma design spec.
- A **Type indicator** (cursor bar, 1 px × 24 px, `--text/textcolor01`) appears inside the input during the Focus state.
- When the dropdown closes, focus must return to the trigger input.

---

## Disabled state

- When `isDisabled` is true, the component must not receive keyboard focus.
- Visual disabled cues: muted background (`--interactive/disabled01`), muted text (`--interactive/disabled04`).
- Ensure `disabled` attribute or `aria-disabled="true"` is set on the underlying input.

> **WARN-001:** Disabled state contrast (`--interactive/disabled04` #8D8B7E on `--interactive/disabled01` #C8C8BD) has not been verified. Ratio may fall below 4.5:1 for normal text. Decorative exemption may apply if disabled text is purely presentational.

---

## Error state

- When `hasError` is true, the input border changes to `--error/error01` (2 px red).
- An error icon (triangle-exclamation) and error message text are shown below the input.
- Link the error message to the input via `aria-describedby`.
- Set `aria-invalid="true"` on the input.

---

## Screen reader guidance

- The **Label** text and **required asterisk** must be announced together — ensure the required marker is not hidden from screen readers.
- The **hint text** (if present) should be announced after the label via `aria-describedby`.
- Time values entered or selected should be reflected in the accessible name or value of the input field.

---

## WCAG 2.1 AA checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.4.3 Contrast (Minimum) | ✅ Expected | `--text/textcolor01` (#26252a) on `--ui/ui05` (#f4f3ee) — verify ratio |
| 1.4.3 Contrast (Disabled) | ⚠️ Verify | Disabled: `--interactive/disabled04` on `--interactive/disabled01` — may not meet 4.5:1 (decorative exemption may apply) |
| 1.4.11 Non-text Contrast | ✅ Expected | Focus ring `--interactive/focus01` (#0056e0) on white/light backgrounds |
| 2.1.1 Keyboard | ⚠️ Verify | Full keyboard operability requires verification in live component |
| 2.4.3 Focus Order | ✅ Expected | Focus ring is visible; tab order follows DOM order |
| 2.4.7 Focus Visible | ✅ Expected | `--interactive/focus01` 2 px focus ring is rendered explicitly |
| 3.3.1 Error Identification | ✅ Expected | Error state exposes icon + error text; link to input via `aria-describedby` |
| 3.3.2 Labels or Instructions | ✅ Expected | Label and hint text are structural elements in the design |
| 4.1.2 Name, Role, Value | ⚠️ Verify | Composite widget roles must be confirmed in rendered DOM |
