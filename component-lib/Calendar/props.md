# Calendar — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-calendar

# npm
$ npm install @8x8/oxygen-calendar
```

Registry configuration required before installing (must be on 8x8 VPN):

- **npm** — add to `.npmrc`: `@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/`
- **yarn** — add to `.yarnrc.yml`:
  ```yaml
  npmScopes:
    8x8:
      npmRegistryServer: "https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/"
  nodeLinker: node-modules
  ```

---

## `Calendar` (default export)

| Prop | Type | Default | Required | Description |
|------|------|---------|:--------:|-------------|
| `testId` | `string` | `'CALENDAR'` | | Test ID DOM attribute value |
| `date` | `Date` | — | ✱ | The currently selected date (for `'date'` display mode) |
| `range` | `DateRange` | — | | The currently selected date range (for `'dateRange'` display mode) |
| `displayMode` | `'date' \| 'dateRange'` | `'date'` | | Date selection/preview and display mode |
| `months` | `number` | `2` | | Number of visible month grids |
| `showMonthArrow` | `boolean` | `true` | | Show next/previous month selector arrows |
| `showMonthYearPickers` | `boolean` | `true` | | Show month and year selector dropdowns |
| `showPreview` | `boolean` | `true` | | Show hover preview (and range preview for `'dateRange'` mode) |
| `defaultFocusedDate` | `Date` | current date | | Date the calendar renders to by default when no selection exists |
| `minDate` | `Date` | `addYears(new Date(), -100)` | | Minimum selectable/visible date |
| `maxDate` | `Date` | `addYears(new Date(), 20)` | | Maximum selectable/visible date |
| `disabledDates` | `Date[]` | `[]` | | Dates to disable; overrides `enabledDates` |
| `enabledDates` | `Date[]` | `[]` | | Only these dates will be enabled (ignored when `disabledDates` is non-empty) |
| `disabledDateTooltip` | `(day: Date) => string \| undefined` | — | | Returns tooltip text for a disabled date, or `undefined` for no tooltip |
| `dateOptions` | `DateOptions` | `{ weekStartsOn: 0, customEvenMonths: false }` | | date-fns date options; `customEvenMonths: true` aligns row count across adjacent Month grids |
| `dayNumberFormat` | `string` | `'d'` | | [date-fns format](https://date-fns.org/v2.28.0/docs/format) for day numbers in the month grid |
| `weekDayDisplayFormat` | `string` | `'EE'` | | [date-fns format](https://date-fns.org/v2.28.0/docs/format) for weekday headers |
| `monthDisplayFormat` | `string` | `'MMMM yyyy'` | | [date-fns format](https://date-fns.org/v2.28.0/docs/format) for month title |
| `focusedMonthFormat` | `string` | `'MMMM'` | | [date-fns format](https://date-fns.org/v2.28.0/docs/format) for month names in the month picker dropdown |
| `focusedYearFormat` | `string` | `'yyyy'` | | [date-fns format](https://date-fns.org/v2.28.0/docs/format) for years in the year picker dropdown |
| `locale` | `Locale` | `en` (built-in) | | date-fns locale object for day/month names and formatting; `en` requires no setup |
| `prevMonthLabel` | `string` | — | | Accessible label for the previous-month navigation button |
| `nextMonthLabel` | `string` | — | | Accessible label for the next-month navigation button |
| `enableMaxWidth` | `boolean` | — | | Constrain the calendar to its maximum width |
| `onDateChange` | `(date: Date) => void` | — | | Fired when the user selects a date (only for `'date'` mode) |
| `onRangeChange` | `(range: DateRange) => void` | — | | Fired when the user changes the selected date range (only for `'dateRange'` mode) |
| `onPreviewChange` | `(preview?: DateRange) => void` | — | | Fired when the hover/focus preview range changes |

---

## `Month` (sub-component)

| Prop | Type | Default | Required | Description |
|------|------|---------|:--------:|-------------|
| `testId` | `string` | `'CALENDAR_MONTH'` | | Test ID DOM attribute value |
| `dateOptions` | `object` | `{ weekStartsOn: 0 }` | | date-fns date options |
| `disabledDates` | `Date[]` | `[]` | | Disabled dates |
| `displayMode` | `'date' \| 'dateRange'` | `'date'` | | Selection/preview mode |
| `showPreview` | `boolean` | `true` | | Show hover/range preview |
| `dayNumberFormat` | `string` | `'d'` | | day-fns format for day numbers |
| `showWeekDays` | `boolean` | `true` | | Show weekday header row (Mon, Tue, …) |
| `weekDayDisplayFormat` | `string` | `'EE'` | | date-fns format for weekday headers |
| `showMonthName` | `boolean` | `false` | | Show month name above the grid |
| `monthDisplayFormat` | `string` | `'MMMM yyyy'` | | date-fns format for the month name |
| `locale` | `object` | `en` (built-in) | | date-fns locale object |
| `onDayClick` | `func` | — | | Fired with `Date` when a day cell is clicked |
| `onPreviewChange` | `func` | — | | Fired with hovered/focused day (`Date`) or `undefined` |

---

## `Day` (sub-component)

| Prop | Type | Default | Required | Description |
|------|------|---------|:--------:|-------------|
| `testId` | `string` | `'CALENDAR_DAY'` | | Test ID DOM attribute value |
| `displayMode` | `'date' \| 'dateRange'` | `'date'` | | Selection/preview mode |
| `isPassive` | `boolean` | `false` | | Day belongs to adjacent month (fills grid edge) |
| `isDisabled` | `boolean` | `false` | | Day is not selectable |
| `isToday` | `boolean` | `false` | | Day is today |
| `isWeekend` | `boolean` | `false` | | Day falls on a weekend |
| `isStartOfWeek` | `boolean` | `false` | | Day is the first day of its week |
| `isEndOfWeek` | `boolean` | `false` | | Day is the last day of its week |
| `isStartOfMonth` | `boolean` | `false` | | Day is the first day of the month |
| `isEndOfMonth` | `boolean` | `false` | | Day is the last day of the month |
| `dayNumberFormat` | `string` | `'d'` | | date-fns format for the day number |
| `locale` | `object` | `en` (built-in) | | date-fns locale object |
| `disabledDateTooltip` | `(day: Date) => string \| undefined` | — | | Tooltip for disabled dates |
| `onClick` | `func` | — | | Fired on click or Enter/Space when focused |
| `onPreviewChange` | `func` | — | | Fired with hovered/focused day (`Date`) or `undefined` |

---

_Source: Oxygen MCP · Extracted 2026-05-08_
