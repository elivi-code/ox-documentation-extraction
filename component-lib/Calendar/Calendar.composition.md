---
parent: "[[Calendar]]"
section: composition
---

## Composition

### Subcomponents (rendered inside Calendar)

| Component | Role |
|-----------|------|
| `Month` | One month grid. Calendar renders `months` of these side by side. |
| `Day` | A single day cell within a `Month` grid; carries the `isToday` / `isDisabled` / `isPassive` / selection flags. |
| `_Day Number` (Figma atom) | Day cell visual — background range fill, focus ring, day digit. |
| `_Predefined ranges item` (Figma atom) | One row in the optional predefined-ranges panel. |
| `_Range type` (Figma atom) | Optional Intraday toggle + From/To date + Start/End time input row. |

### Composing wrappers (Calendar rendered inside these)

Calendar is **not standalone** — it always opens as a popover from a date input. Two Oxygen components compose it in practice:

- **`DateTimeSelector`** — single-date input + Calendar popover wrapper. See [DateTimeSelector/](../DateTimeSelector/).
- **`DateTimeRangeSelector`** — range input + Calendar popover + predefined-ranges panel + Reset/Cancel/Apply action bar. See [DateTimeRangeSelector/](../DateTimeRangeSelector/).

The action bar and predefined-ranges panel are owned by the composing wrapper, not by Calendar itself (see [[Calendar.usage]] Pairs 4 and 6).

### Related components

From the published docs page:

- **Time selector** — paired with Calendar in range mode to add start/end time inputs (the Figma `time` boolean).
- **Text input** — the surface the Calendar popover anchors to.
- **Forms** — the pattern that hosts most Calendar usage.

---

## Examples

<!-- STUB:GAP-001 source="Oxygen MCP returned 0 clean Storybook examples for the calendar package. Extract canonical Storybook examples from @8x8/oxygen-calendar source once available, or confirm with the component team that the documentation story is the only example." -->

> The snippets below are derived from prop descriptions and the documentation story (`Calendar.documentation.stories.tsx`), **not** from canonical Storybook stories. Confirm with the component team (GAP-001).

```tsx
// Single date selection
import { Calendar } from '@8x8/oxygen-calendar';
import { useState } from 'react';

function SingleDateExample() {
  const [date, setDate] = useState<Date>();
  return <Calendar date={date} onDateChange={setDate} displayMode="date" />;
}
```

```tsx
// Date range selection
import { Calendar } from '@8x8/oxygen-calendar';
import { useState } from 'react';
import type { DateRange } from '@8x8/oxygen-calendar';

function DateRangeExample() {
  const [range, setRange] = useState<DateRange>();
  return (
    <Calendar
      date={range?.startDate}
      range={range}
      onRangeChange={setRange}
      displayMode="dateRange"
    />
  );
}
```

```tsx
// Min/max date bounds
<Calendar
  date={date}
  onDateChange={setDate}
  minDate={new Date('2026-01-01')}
  maxDate={new Date('2026-12-31')}
/>
```

```tsx
// Single month view
<Calendar date={date} onDateChange={setDate} months={1} />
```

```tsx
// Week starts on Monday
<Calendar date={date} onDateChange={setDate} dateOptions={{ weekStartsOn: 1 }} />
```

See [[Calendar.usage]] for disabled-dates, locale, and 90-day-window patterns.
