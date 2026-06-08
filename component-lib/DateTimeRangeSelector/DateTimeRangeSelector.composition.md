---
parent: "[[DateTimeRangeSelector]]"
section: composition
component: DateTimeRangeSelector
pipeline_stage: spec_ready
audit_verdict: "YES"
tags:
  - oxygen
  - component/DateTimeRangeSelector
  - role/spoke
  - section/composition
  - stage/spec_ready
  - category/date_time
---

## Composition

### Subcomponents (structural containment)

| Component | Export | Role |
|-----------|--------|------|
| [[DateTimeRangePicker]] | named | Internal open picker panel — calendar grid + time selectors + predefined ranges + action bar. Use standalone only when embedding in a custom trigger layout. |
| [[DateTimeRangeSelectorPredefinedList]] | named | Predefined ranges list sub-component. Can be composed separately for custom filter UIs. |
| [[Calendar]] | implicit (embedded) | The dual-month range calendar rendered inside the open picker panel. Token documentation lives in [[Calendar.tokens]]. |

### Props that accept components

| Prop | Accepts | Notes |
|------|---------|-------|
| `inputRenderer` | `(props: InputRendererProps) => React.ReactNode` | Fully custom trigger input; replaces the default Dropdown frame. Must be focusable and keyboard-accessible (WARN-001). |
| `headerRenderer` | `(props: DateTimeRangeSelectorProps) => React.ReactNode` | Custom calendar header inside the open picker panel. |
| `inputIcon` | `React.ReactNode` | Replaces the default calendar icon. Pass `null` to show no icon. |
| `iconLeft` | `React.ElementType` | Icon on the left side of the trigger input. Not represented in the Figma anatomy — verify against rendered DOM (WARN-002). |
| `otherCalendarProps` | `Partial<CalendarProps>` | Any [[Calendar]] prop forwarded to the embedded calendar (e.g. `minDate`, `maxDate`, `disabledDates`, `disabledDateTooltip`). |

---

### Related components (peer / contextual)

| Component | Relationship |
|-----------|-------------|
| [[DateTimeSelector]] | Sibling — shares the same Figma trigger input (node `80239:8235`). Use when selecting a single date, not a range. |
| [[Calendar]] | The open picker panel uses the Calendar range-picker internally. |
| [[TimeSelector]] | For time-only selection without a date component. |

---

### Patterns (ingredient in)

| Pattern | Notes |
|---------|-------|
| Analytics / reporting filter bar | Primary use case — predefined ranges + custom window for dashboard time filters |
| Billing window selector | Start + end date with intraday time precision; `hideTime={false}` (default) |
| Call history / event log filter | Historical record filtering; pair with `otherCalendarProps.minDate` for retention-window limits |
| Inline filter (SlideOut / drawer) | Use `DateTimeRangePicker` (named export) with a custom trigger; `customCloseHandlers` for dismiss-on-close |

---

### Composition examples

#### Standalone picker panel (custom trigger)

```tsx
import { DateTimeRangePicker } from '@8x8/oxygen-date-time-range-selector';

// Render the open panel directly — supply your own trigger
<DateTimeRangePicker
  dateTimeRange={range}
  predefinedRange={predefinedRange}
  onRangeChange={onRangeChange}
  onClose={closePanel}
/>
```

#### With 90-day data-retention window

```tsx
const ninetyDaysAgo = new Date();
ninetyDaysAgo.setDate(ninetyDaysAgo.getDate() - 90);

<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  otherCalendarProps={{
    minDate: ninetyDaysAgo,
    disabledDateTooltip: (date) =>
      date < ninetyDaysAgo ? 'Outside 90-day data window' : undefined,
  }}
/>
```

#### Custom input renderer

```tsx
<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  inputRenderer={({ value, onClick }) => (
    <button type="button" onClick={onClick}>
      {value || 'Select range'}
    </button>
  )}
/>
```
