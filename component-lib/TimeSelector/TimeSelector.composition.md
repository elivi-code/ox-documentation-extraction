---
parent: "[[TimeSelector]]"
section: composition
component: TimeSelector
pipeline_stage: draft
tags:
  - oxygen
  - component/TimeSelector
  - role/spoke
  - section/composition
  - category/date_time
---

## Sub-components

TimeSelector contains one structural sub-component:

### Icon Button (label area)

| Element | Description |
|---------|-------------|
| Rendered inside | The `_base_form_label` frame (element 1c in the anatomy) |
| Purpose | Hosts an info/FAQ icon that reveals a tooltip with additional help content |
| Slot type | Fixed sub-component — not consumer-swappable |
| Icon slot | `TypeIcon` — instance swap slot accepting icon components at `iconSizeM` |
| Styling | 2 px padding, 6 px border-radius (hardcoded) |
| Figma node | `28172:41855` |

The Icon Button is visible when `Show Label` is true. The consumer cannot suppress the icon independently; it is part of the label composite.

---

## Pattern membership

TimeSelector is used as an ingredient within the following patterns:

| Pattern | How it's used |
|---------|--------------|
| [[Forms]] | TimeSelector provides the time-of-day input inside form layouts. It follows the standard label → input → hint/error stack from the Forms pattern. |

---

## Composed with

These components are commonly composed alongside TimeSelector in product code and design:

| Component | Composition context |
|-----------|-------------------|
| [[Calendar]] | Paired to capture date + time together (date from Calendar, time from TimeSelector). Neither component exposes a combined date-time picker natively — the consumer must wire the two values. |
| [[TextField]] | Alongside TimeSelector in scheduling forms when duration or free-text time entry is needed for a different field. |
| [[Select]] / [[Radio]] | Alongside or as alternatives when the time choice is a small, discrete set. |

---

## When to compose vs. replace

| Situation | Use |
|-----------|-----|
| User must pick a specific hour + minute | TimeSelector alone |
| User must pick a specific date | Calendar alone |
| User must pick a date AND time | Calendar + TimeSelector composed |
| User must enter a duration (e.g. `90 min`) | TextField (TimeSelector enforces 0–23 h / 0–59 min) |
| User picks from ≤5 preset times | Select or Radio (picker is overkill) |
