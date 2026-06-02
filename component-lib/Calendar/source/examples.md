---
component: Calendar
package: "@8x8/oxygen-calendar"
category: date_time
role: examples
role_description: "Code usage examples from basic to advanced patterns"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
siblings:
  - "[[Calendar/props]]"
  - "[[Calendar/tokens]]"
  - "[[Calendar/accessibility]]"
  - "[[Calendar/Calendar-figma]]"
  - "[[Calendar/Calendar-usage]]"
  - "[[Calendar/Calendar-audit]]"
tags:
  - oxygen
  - component/Calendar
  - role/examples
  - stage/blocked
  - category/date_time
---

# Calendar — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Single date selection

```tsx
import { Calendar } from '@8x8/oxygen-calendar';
import { useState } from 'react';

function SingleDateExample() {
  const [date, setDate] = useState<Date>();

  return (
    <Calendar
      date={date}
      onDateChange={setDate}
      displayMode="date"
    />
  );
}
```

## Date range selection

```tsx
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

## Disabled dates with tooltip

```tsx
<Calendar
  date={date}
  onDateChange={setDate}
  disabledDates={[new Date('2026-05-10'), new Date('2026-05-11')]}
  disabledDateTooltip={(day) =>
    day.getDay() === 0 || day.getDay() === 6
      ? 'Weekends are not available'
      : undefined
  }
/>
```

## Min/max date bounds

```tsx
<Calendar
  date={date}
  onDateChange={setDate}
  minDate={new Date('2026-01-01')}
  maxDate={new Date('2026-12-31')}
/>
```

## Single month view

```tsx
<Calendar
  date={date}
  onDateChange={setDate}
  months={1}
/>
```

## Custom locale (French)

```tsx
import { fr } from 'date-fns/locale';

<Calendar
  date={date}
  onDateChange={setDate}
  locale={fr}
  weekDayDisplayFormat="EEEEEE"
  monthDisplayFormat="MMMM yyyy"
/>
```

## Week starts on Monday

```tsx
<Calendar
  date={date}
  onDateChange={setDate}
  dateOptions={{ weekStartsOn: 1 }}
/>
```

## Even month rows across two panels

```tsx
<Calendar
  date={date}
  onDateChange={setDate}
  months={2}
  dateOptions={{ weekStartsOn: 0, customEvenMonths: true }}
/>
```

---

> **Note:** No clean Storybook examples were returned by the Oxygen MCP for this component. The snippets above are derived from prop descriptions and the documentation story in `Calendar.documentation.stories.tsx`.

_Source: Oxygen MCP · Extracted 2026-05-08_
