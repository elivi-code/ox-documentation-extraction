# DateTimeRangeSelector — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

<!-- NOTE: Oxygen MCP returned 1 Storybook example for @8x8/oxygen-date-time-range-selector,
     but it is a documentation story wrapped in <Doc> and <ComponentSection> — not a clean snippet.
     The core component usage pattern is extracted from the story. Additional snippets are inferred
     from prop documentation. -->

---

## Basic usage — controlled range

```tsx
import { DateTimeRangeSelector } from '@8x8/oxygen-date-time-range-selector';
import { useState } from 'react';

type RangeState = {
  selectedDateTime?: { startDate: Date; endDate?: Date };
  selectedPredefinedRange?: { id: string; value?: number };
};

const defaultState: RangeState = { selectedPredefinedRange: { id: 'CUSTOM' } };

function App() {
  const [state, setState] = useState<RangeState>(defaultState);

  const onRangeChange = ({ dateTime, predefinedRange } = {}) => {
    if (predefinedRange) {
      const { id } = predefinedRange;
      setState(
        id !== 'custom'
          ? { selectedPredefinedRange: predefinedRange }
          : { selectedDateTime: { startDate: new Date() }, selectedPredefinedRange: predefinedRange }
      );
    } else if (dateTime) {
      setState({ selectedDateTime: dateTime });
    } else {
      setState(defaultState); // Clear pressed
    }
  };

  return (
    <DateTimeRangeSelector
      predefinedRange={state.selectedPredefinedRange}
      dateTimeRange={state.selectedDateTime}
      onRangeChange={onRangeChange}
      onOpen={() => console.log('opened')}
      onClose={() => console.log('closed')}
    />
  );
}
```

---

## Without predefined ranges panel

```tsx
<DateTimeRangeSelector
  dateTimeRange={dateTimeRange}
  onRangeChange={onRangeChange}
  hidePredefinedRanges
/>
```

---

## Without time selectors (date-only range)

```tsx
<DateTimeRangeSelector
  dateTimeRange={dateTimeRange}
  onRangeChange={onRangeChange}
  hideTime
/>
```

---

## Small size

```tsx
<DateTimeRangeSelector
  dateTimeRange={dateTimeRange}
  onRangeChange={onRangeChange}
  size="small"
/>
```

---

## Custom labels

```tsx
<DateTimeRangeSelector
  dateTimeRange={dateTimeRange}
  onRangeChange={onRangeChange}
  fromLabel="Start"
  toLabel="End"
  startTimeLabel="From time"
  endTimeLabel="Until time"
  finishButtonLabel="Apply"
  clearButtonLabel="Reset"
  placeholder="Choose a range"
/>
```

---

## French locale

```tsx
import { fr } from 'date-fns/locale';

<DateTimeRangeSelector
  dateTimeRange={dateTimeRange}
  onRangeChange={onRangeChange}
  locale={fr}
  dateFormat="dd/MM/yyyy"
/>
```

---

## With 90-day limit (via Calendar props)

```tsx
// Block dates more than 90 days ago using otherCalendarProps
const ninetyDaysAgo = new Date();
ninetyDaysAgo.setDate(ninetyDaysAgo.getDate() - 90);

<DateTimeRangeSelector
  dateTimeRange={dateTimeRange}
  onRangeChange={onRangeChange}
  otherCalendarProps={{
    minDate: ninetyDaysAgo,
    disabledDateTooltip: (date) =>
      date < ninetyDaysAgo ? 'Outside 90-day data window' : undefined,
  }}
/>
```

---

## Error state

```tsx
<DateTimeRangeSelector
  dateTimeRange={dateTimeRange}
  onRangeChange={onRangeChange}
  hasError
/>
```

---

## Disabled

```tsx
<DateTimeRangeSelector
  dateTimeRange={dateTimeRange}
  onRangeChange={onRangeChange}
  isDisabled
/>
```

---

## Custom input renderer

```tsx
<DateTimeRangeSelector
  dateTimeRange={dateTimeRange}
  onRangeChange={onRangeChange}
  inputRenderer={({ value, onClick }) => (
    <button type="button" onClick={onClick}>
      {value || 'Select range'}
    </button>
  )}
/>
```

---

_Source: Oxygen MCP · Extracted 2026-05-08_
