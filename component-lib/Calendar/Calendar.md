---
component: Calendar
package: "@8x8/oxygen-calendar"
status: draft
category: date_time
figma: "https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=80239:7420"
variants: [Single, Range]
props:
  - testId: string
  - date: Date
  - range: DateRange
  - displayMode: enum
  - months: number
  - showMonthArrow: boolean
  - showMonthYearPickers: boolean
  - showPreview: boolean
  - defaultFocusedDate: Date
  - minDate: Date
  - maxDate: Date
  - disabledDates: Date[]
  - enabledDates: Date[]
  - disabledDateTooltip: function
  - dateOptions: DateOptions
  - dayNumberFormat: string
  - weekDayDisplayFormat: string
  - monthDisplayFormat: string
  - focusedMonthFormat: string
  - focusedYearFormat: string
  - locale: Locale
  - prevMonthLabel: string
  - nextMonthLabel: string
  - enableMaxWidth: boolean
  - onDateChange: function
  - onRangeChange: function
  - onPreviewChange: function
subcomponents: ["[[Month]]", "[[Day]]"]
related: ["[[DateTimeSelector]]", "[[DateTimeRangeSelector]]", "[[TimePicker]]", "[[TextInput]]"]
patterns: ["[[Forms]]"]
tokens: ["[[--ui/ui01]]", "[[--ui/ui02]]", "[[--ui/ui05]]", "[[--ui/ui06]]", "[[--ui/shadow01]]", "[[--actions/action01]]", "[[--actions/action09]]", "[[--text/textcolor01]]", "[[--text/textcolor06]]", "[[--interactive/focus01]]"]
spokes:
  - "[[Calendar.props]]"
  - "[[Calendar.anatomy]]"
  - "[[Calendar.tokens]]"
  - "[[Calendar.usage]]"
  - "[[Calendar.accessibility]]"
  - "[[Calendar.platform]]"
  - "[[Calendar.composition]]"
tags: [component, date_time, date-picker]
---

## Overview

Calendar lets users select a single date or a range of dates — optionally with time — and is the visual surface behind every date input in 8x8 products (scheduling, reporting windows, filters). One API serves two layouts via `displayMode`: a 312 × 348 single-date picker and a 788 × 596 dual-month range picker with an optional predefined-ranges panel and Reset/Cancel/Apply action bar. It is always rendered as a popover from a date input, never standalone.

> **Status: draft.** Two major SOURCE_GAPs remain — no canonical Storybook examples (GAP-001) and token names are provisional (from Figma CSS, not the UI-Foundations variables panel — GAP-002/007). Usage guidance is editorial (published docs page), not Figma-native Do/Don't cards (GAP-003).

## Spokes

- [[Calendar.props]] — 27 props including `date`, `range`, `displayMode`, `months`; plus `Month` and `Day` sub-component props and `DateRange` / `DateOptions` type shapes
- [[Calendar.anatomy]] — range (11 parts) + single (4 parts) layouts across 2 variants; 4 persistent + 7 interaction states; breakpoint behaviour
- [[Calendar.tokens]] — ~16 element/state color bindings + 6 text styles covering background, text, selection, focus, dividers (token names provisional)
- [[Calendar.usage]] — 7 Do/Don't pairs covering variant choice, nav labelling, selection limits, explicit Apply, locale formatting, predefined ranges, responsive layout (editorial)
- [[Calendar.accessibility]] — ARIA roles, full keyboard map, screen-reader guidance, WCAG 2.1 AA checklist (2 items pending token resolution)
- [[Calendar.platform]] — no PUI requirements
- [[Calendar.composition]] — subcomponents `Month` + `Day`; rendered inside [[DateTimeSelector]] / [[DateTimeRangeSelector]]; related Time selector, Text input, Forms
