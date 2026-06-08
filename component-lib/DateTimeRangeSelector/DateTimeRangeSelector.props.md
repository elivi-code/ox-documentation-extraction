---
parent: "[[DateTimeRangeSelector]]"
section: props
component: DateTimeRangeSelector
pipeline_stage: spec_ready
audit_verdict: "YES"
tags:
  - oxygen
  - component/DateTimeRangeSelector
  - role/spoke
  - section/props
  - stage/spec_ready
  - category/date_time
---

## Props

### DateTimeRangeSelector

| Name | Type | Default | Required | Description |
|------|------|---------|:--------:|-------------|
| `clearButtonLabel` | `string` | `'Clear'` | No | Label text for the clear button |
| `customCloseHandlers` | `CloseHandler[]` | `[]` | No | Events that should trigger closing the dropdown |
| `customPredefinedRangeLabel` | `string` | `'Custom'` | No | Label for the "Custom" entry in the predefined ranges list |
| `dateFormat` | `string` | `'MM/dd/yyyy'` | No | Date format pattern (date-fns format) |
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
| `timeFormat` | `string` | `'hh:mm a'` | No | Time format pattern (date-fns format) |
| `toLabel` | `string` | `'To'` | No | Label for the end date input |

### DateTimeRangePicker

`DateTimeRangePicker` is the internal open picker panel. Use it when you need to render the calendar + time selectors without the trigger input wrapper.

<!-- STUB:GAP-004 source="Add Type and Default columns to the DateTimeRangePicker props table, or confirm with the component team which props have defaults and which are always required when using DateTimeRangePicker standalone." -->

| Prop | Description |
|------|-------------|
| `dateTimeRange` | The selected date range |
| `predefinedRange` | Currently active predefined range |
| `predefinedRanges` | Predefined range options |
| `dateFormat` | Date format pattern |
| `timeFormat` | Time format pattern |
| `locale` | date-fns locale |
| `hidePredefinedRanges` | Hide predefined ranges panel |
| `hideTime` | Hide time selector row |
| `fromLabel` | From label |
| `startTimeLabel` | Start time label |
| `toLabel` | To label |
| `endTimeLabel` | End time label |
| `customPredefinedRangeLabel` | Custom range label |
| `endTimeErrorMessage` | End-before-start error message |
| `onClose` | Close handler |
| `onRangeChange` | Range change handler |
| `otherCalendarProps` | Props forwarded to Calendar |
| `testId` | Test ID |
| `id` | Element ID |
| `setOuterState` | Internal state setter |
| `footer` | Custom footer content |

### DateTimeRangeSelectorPredefinedList

Named export for the predefined ranges list sub-component. Props not separately documented — see source for full interface.

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
}
```

---

## Notes

- `onRangeChange` receives `{ dateTime, predefinedRange }` — exactly one will be defined depending on whether the user picked a custom range or a predefined one. When Clear is pressed, both are undefined (reset).
- `predefinedRanges` defaults to: Today, Last hour, Yesterday, Last 7 days, This month, Last month, Last 3 months, This year, Last year, Custom.
- `otherCalendarProps` accepts any `CalendarProps` from `@8x8/oxygen-calendar` — useful for `disabledDates`, `minDate`, `maxDate`.
- `locale` works with date-fns v2 locale imports (e.g. `import { fr } from 'date-fns/locale'`).
- `iconLeft` (line 76 of props.md) does not appear in the shared Figma "Date picker" anatomy — verify whether it renders within the trigger input or is used elsewhere (WARN-002).
