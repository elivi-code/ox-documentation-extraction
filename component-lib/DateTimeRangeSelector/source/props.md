---
component: DateTimeRangeSelector
package: "@8x8/oxygen-date-time-range-selector"
category: date_time
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: "YES"
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - figma
  - usage
  - audit
siblings:
  - "[[DateTimeRangeSelector/examples]]"
  - "[[DateTimeRangeSelector/tokens]]"
  - "[[DateTimeRangeSelector/accessibility]]"
  - "[[DateTimeRangeSelector/DateTimeRangeSelector-figma]]"
  - "[[DateTimeRangeSelector/DateTimeRangeSelector-usage]]"
  - "[[DateTimeRangeSelector/DateTimeRangeSelector-audit]]"
tags:
  - oxygen
  - component/DateTimeRangeSelector
  - role/props
  - stage/spec_ready
  - category/date_time
---

# DateTimeRangeSelector — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```bash
npm install @8x8/oxygen-date-time-range-selector
```

```tsx
import { DateTimeRangeSelector } from '@8x8/oxygen-date-time-range-selector';
```

---

## Components in this package

| Component | Export | Description |
|-----------|--------|-------------|
| `DateTimeRangeSelector` | default | Full date-time range picker with trigger input + dropdown |
| `DateTimeRangePicker` | named | Internal picker panel (calendar + time selectors); use for custom trigger layouts |
| `DateTimeRangeSelectorPredefinedList` | named | Predefined ranges list sub-component |

---

## DateTimeRangeSelector props

| Prop | Type | Default | Required | Description |
|------|------|---------|:--------:|-------------|
| `clearButtonLabel` | `string` | `'Clear'` | No | Label text for the clear button |
| `customCloseHandlers` | `CloseHandler[]` | `[]` | No | Events that should trigger closing the dropdown |
| `customPredefinedRangeLabel` | `string` | `'Custom'` | No | Label for the "Custom" entry in the predefined ranges list |
| `dateFormat` | `string` | `'MM/dd/yyyy'` | No | Date format pattern ([date-fns format](https://date-fns.org/v2.28.0/docs/format)) |
| `dateTimeRange` | `DateTimeRange` | — | No | The currently selected date-time range |
| `endTimeErrorMessage` | `string` | `'Cannot be before start time'` | No | Error message when end time precedes start time |
| `endTimeLabel` | `string` | `'End Time'` | No | Label for the end time selector |
| `finishButtonLabel` | `string` | `'Finish'` | No | Label text for the finish/apply button |
| `fromLabel` | `string` | `'From'` | No | Label for the start date input |
| `hasError` | `boolean` | `false` | No | Whether the trigger input is in an error state |
| `headerRenderer` | `(props: DateTimeRangeSelectorProps) => React.ReactNode` | — | No | Render function for a custom calendar header |
| `hidePredefinedRanges` | `boolean` | `false` | No | Hide the predefined ranges panel |
| `hideTime` | `boolean` | `false` | No | Hide the intraday time selector row |
| `iconLeft` | `React.ElementType` | `null` | No | Icon component to display on the left side of the input |
| `id` | `string` | — | No | `id` attribute for the input element |
| `inputIcon` | `React.ReactNode` | — | No | Replaces the default calendar icon; pass `null` to show no icon |
| `inputRenderer` | `(props: InputRendererProps) => React.ReactNode` | — | No | Render function for a fully custom trigger input |
| `isDisabled` | `boolean` | `false` | No | Whether the input is disabled |
| `locale` | `Locale` | — | No | date-fns locale object for localised month/day names |
| `onClose` | `() => void` | `noop` | No | Callback fired when the dropdown closes |
| `onOpen` | `() => void` | `noop` | No | Callback fired when the dropdown opens |
| `onRangeChange` | `(changes: { dateTime?: DateTimeRange; predefinedRange?: SelectedPredefinedRange }) => void` | `noop` | No | Callback fired when the Finish or Clear button is pressed |
| `otherCalendarProps` | `Partial<CalendarProps>` | `{}` | No | Additional props forwarded to the embedded Calendar component |
| `placeholder` | `string` | `'Select Date Range'` | No | Placeholder text when no range is selected |
| `predefinedRange` | `SelectedPredefinedRange` | `{ id: 'CUSTOM' }` | No | Currently active predefined range |
| `predefinedRanges` | `PredefinedRange[]` | `defaultPredefinedRanges` | No | List of predefined range options shown in the left panel |
| `size` | `'large' \| 'small'` | `'large'` | No | Size of the trigger input |
| `startTimeLabel` | `string` | `'Start Time'` | No | Label for the start time selector |
| `testId` | `string` | `'DATE_TIME_RANGE_SELECTOR'` | No | `data-testid` DOM attribute |
| `theme` | `Partial<Theme>` | — | No | Theme override; default supplied by Oxygen theme provider |
| `timeFormat` | `string` | `'hh:mm a'` | No | Time format pattern ([date-fns format](https://date-fns.org/v2.28.0/docs/format)) |
| `toLabel` | `string` | `'To'` | No | Label for the end date input |

---

## DateTimeRangePicker props

`DateTimeRangePicker` is the internal open picker panel. Use it when you need to render the calendar + time selectors without the trigger input wrapper.

| Prop | Type | Description |
|------|------|-------------|
| `dateTimeRange` | `DateTimeRange` | The selected date range |
| `predefinedRange` | `SelectedPredefinedRange` | Currently active predefined range |
| `predefinedRanges` | `PredefinedRange[]` | Predefined range options |
| `dateFormat` | `string` | Date format pattern |
| `timeFormat` | `string` | Time format pattern |
| `locale` | `object` | date-fns locale |
| `hidePredefinedRanges` | `boolean` | Hide predefined ranges panel |
| `hideTime` | `boolean` | Hide time selector row |
| `fromLabel` | `string` | From label |
| `startTimeLabel` | `string` | Start time label |
| `toLabel` | `string` | To label |
| `endTimeLabel` | `string` | End time label |
| `customPredefinedRangeLabel` | `string` | Custom range label |
| `endTimeErrorMessage` | `string` | End-before-start error message |
| `onClose` | `() => void` | Close handler |
| `onRangeChange` | `(changes: object) => void` | Range change handler |
| `otherCalendarProps` | `OtherCalendarProps` | Props forwarded to Calendar |
| `testId` | `string` | Test ID |
| `id` | `string` | Element ID |
| `setOuterState` | `(arg0: object) => void` | Internal state setter |
| `footer` | `ReactNode` | Custom footer content |

---

## Type interfaces

```ts
interface DateTimeRange {
  startDate: Date;
  endDate: Date;
}

interface SelectedPredefinedRange {
  id: string;
  value?: number;
}

interface PredefinedRange {
  id: string;
  label: string;
  value?: number;
  // Fixed range or relative range with optional argument
}
```

---

## Notes

- `onRangeChange` receives `{ dateTime, predefinedRange }` — exactly one will be defined depending on whether the user picked a custom range or a predefined one. When Clear is pressed, both are undefined (reset).
- `predefinedRanges` defaults to the built-in list: Today, Last hour, Yesterday, Last 7 days, This month, Last month, Last 3 months, This year, Last year, Custom.
- `otherCalendarProps` accepts any `CalendarProps` from `@8x8/oxygen-calendar` — useful for `disabledDates`, `minDate`, `maxDate`.
- `locale` works with date-fns v2 locale imports (e.g. `import { fr } from 'date-fns/locale'`).

---

_Source: Oxygen MCP · Extracted 2026-05-08_
