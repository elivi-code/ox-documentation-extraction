---
parent: "[[Radio]]"
section: accessibility
---

## ARIA Roles & Attributes

| Element | Role / Attribute | Notes |
|---------|-----------------|-------|
| `RadioGroup` container | `role="radiogroup"` | Groups related radio inputs semantically |
| `Radio` input | `role="radio"` | Native `<input type="radio">` |
| Group label | `aria-labelledby` / `aria-label` | The optional group label should label the `radiogroup` |
| Info button | `aria-label` | Set via `infoBoxButtonLabel` — required when `infoBoxText` is used |
| Checked state | `aria-checked` | Managed automatically by the native input |
| Disabled state | `aria-disabled` / `disabled` | Set via `isDisabled` prop |

---

## Keyboard Interactions

| Key | Behavior |
|-----|----------|
| `Tab` | Moves focus into the radio group (to the checked option, or first option if none selected) |
| `Arrow Up` / `Arrow Left` | Moves focus to **and selects** the previous radio in the group |
| `Arrow Down` / `Arrow Right` | Moves focus to **and selects** the next radio in the group |
| `Tab` (from last item) | Moves focus out of the radio group to the next focusable element |
| `Space` | Selects the focused radio button (if not already selected) |

> **Focus behavior:** The focus ring encompasses the entire Radio Button row — from the Radio Button Input to the label. The whole row area is interactive, clickable, and responsive to hover actions.

---

## Screen Reader Guidance

- The group label (if provided) is announced before the individual radio options.
- Each `Radio` announces its label and checked/unchecked state.
- When `infoBoxText` is used, the info button is announced using `infoBoxButtonLabel` — always provide a meaningful label (e.g., `"More info about Enterprise plan"`).
- Radio Button Input (no label) must have its purpose conveyed by surrounding context or an explicit `aria-label`/`aria-labelledby` on the input or group.

---

## Focus

The focus ring covers the entire Radio Button row (input + label area), not just the input circle. The whole area is interactive and responds to hover and click events.

---

## Font Scaling & Zoom

- Increasing browser font size enlarges the label text but does **not** change the size of the Radio Button Input itself. Radio Input alignment remains at the top of the label.
- Using browser zoom proportionally increases the font size, Radio Button Input size, and the gap between them.

---

## Multiline Labels

When a label text wraps to a second line or more, the Radio Button Input alignment stays at the top of the label text (not centered).

---

## WCAG 2.1 AA Checklist

| Criterion | Level | Status | Notes |
|-----------|-------|--------|-------|
| 1.3.1 Info and Relationships | A | ✅ | Semantic `radiogroup` / `radio` roles convey structure |
| 1.4.3 Contrast (Minimum) | AA | ✅ | Labels and inputs meet contrast requirements in both light and dark themes |
| 1.4.4 Resize Text | AA | ✅ | Font scaling does not break layout; radio aligns to top of multiline labels |
| 2.1.1 Keyboard | A | ✅ | Full arrow-key navigation within group; Tab moves in/out |
| 2.4.3 Focus Order | A | ✅ | Focus moves logically through the radio group |
| 2.4.7 Focus Visible | AA | ✅ | Visible focus ring on the entire Radio Button row |
| 3.3.2 Labels or Instructions | A | ✅ | Each radio has a label; info button has `infoBoxButtonLabel` |
| 4.1.2 Name, Role, Value | A | ✅ | Native radio inputs with proper labels; checked/disabled state communicated |
