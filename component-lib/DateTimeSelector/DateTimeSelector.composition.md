---
parent: "[[DateTimeSelector]]"
section: composition
---

## Subcomponents

| Subcomponent | Type | Role | Notes |
|---|---|---|---|
| `[[_base_form_label]]` | instance (optional slot) | Form label zone | Label text + required asterisk + faq icon; toggled by `Show Label` property |
| `[[_base_form_hint]]` | instance (optional slot) | Form hint zone | Hint or error text below field; toggled by `Show Hint` property |
| `[[Icon Button]]` | instance | Help/FAQ icon in label | 20×20px, faq icon (16×16); nested inside `_base_form_label` |
| `Dropdown` | frame (internal) | Date picker trigger | Always present; houses text content, calendar icon, focus ring, and error area |

> `_base_form_label` and `_base_form_hint` are shared instances used across other Oxygen form fields.

## Related components

| Component | Relationship |
|---|---|
| `[[DateTimeRangeSelector]]` | Sibling — shares the same Figma trigger component set (node `80239:8235`). Use for start/end date-time ranges instead of single-date. |
| `[[Calendar]]` | Embedded in the picker popover — provides the calendar grid for day navigation. |

## Common patterns

- **Scheduling forms** — single date/time commitment (meeting start, deadline, billing date)
- **Filter bars** — optional date filter with `isClearable` and `closeOnDateChange`
- **Availability pickers** — `isLoading` + `loadingMessage` pattern for async slot fetching
