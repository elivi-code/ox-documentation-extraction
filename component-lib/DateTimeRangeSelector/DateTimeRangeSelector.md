---
component: DateTimeRangeSelector
package: "@8x8/oxygen-date-time-range-selector"
status: partial
category: date_time
figma: "https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=80239:8235"
variants:
  - Large (default)
  - Small
  - Rest / Hover / Focus / Error / Disabled
  - Filled / Unfilled
props:
  - clearButtonLabel: string
  - customCloseHandlers: CloseHandler[]
  - customPredefinedRangeLabel: string
  - dateFormat: string
  - dateTimeRange: DateTimeRange
  - endTimeErrorMessage: string
  - endTimeLabel: string
  - finishButtonLabel: string
  - fromLabel: string
  - hasError: boolean
  - headerRenderer: function
  - hidePredefinedRanges: boolean
  - hideTime: boolean
  - iconLeft: React.ElementType
  - id: string
  - inputIcon: React.ReactNode
  - inputRenderer: function
  - isDisabled: boolean
  - locale: Locale
  - onClose: function
  - onOpen: function
  - onRangeChange: function
  - otherCalendarProps: Partial<CalendarProps>
  - placeholder: string
  - predefinedRange: SelectedPredefinedRange
  - predefinedRanges: PredefinedRange[]
  - size: enum
  - startTimeLabel: string
  - testId: string
  - theme: Partial<Theme>
  - timeFormat: string
  - toLabel: string
subcomponents:
  - "[[DateTimeRangePicker]]"
  - "[[DateTimeRangeSelectorPredefinedList]]"
  - "[[Calendar]]"
related:
  - "[[DateTimeSelector]]"
  - "[[TimeSelector]]"
patterns:
  - "[[analytics-filter-bar]]"
  - "[[billing-window-selector]]"
  - "[[call-history-filter]]"
tokens:
  - "--ui/ui05"
  - "--text/textcolor01"
  - "--text/textcolor02"
  - "--interactive/hover06"
  - "--interactive/focus01"
  - "--interactive/disabled01"
  - "--interactive/disabled04"
  - "--error/error01"
spokes:
  - "[[DateTimeRangeSelector.props]]"
  - "[[DateTimeRangeSelector.anatomy]]"
  - "[[DateTimeRangeSelector.tokens]]"
  - "[[DateTimeRangeSelector.usage]]"
  - "[[DateTimeRangeSelector.accessibility]]"
  - "[[DateTimeRangeSelector.platform]]"
  - "[[DateTimeRangeSelector.composition]]"
pipeline_stage: spec_ready
audit_verdict: "YES"
siblings:
  - "[[DateTimeRangeSelector.props]]"
  - "[[DateTimeRangeSelector.anatomy]]"
  - "[[DateTimeRangeSelector.tokens]]"
  - "[[DateTimeRangeSelector.usage]]"
  - "[[DateTimeRangeSelector.accessibility]]"
  - "[[DateTimeRangeSelector.platform]]"
  - "[[DateTimeRangeSelector.composition]]"
tags:
  - oxygen
  - component/DateTimeRangeSelector
  - role/hub
  - stage/spec_ready
  - category/date_time
---

## Overview

`DateTimeRangeSelector` is a 320px trigger input that opens a popover containing a dual-month calendar range picker, an optional predefined-ranges panel (Last 7 days, This month, etc.), and an optional intraday time-selector row. Selection is committed via **Finish** or **Clear** — not on the second date click — making `onRangeChange` the single integration point for analytics, reporting, billing, and call-history time-window filters across 8x8 product surfaces. The trigger is shared with `DateTimeSelector` (same Figma node `80239:8235`); the open picker panel is `@8x8/oxygen-calendar` embedded internally.

---

## Spokes

- [[DateTimeRangeSelector.props]] — 32 props on the selector including dateTimeRange, onRangeChange, hidePredefinedRanges, hideTime, hasError, isDisabled, locale; 21 props on DateTimeRangePicker (Type/Default pending GAP-004)
- [[DateTimeRangeSelector.anatomy]] — 3 elements (label zone, dropdown trigger, hint zone) across 5 states (Rest/Hover/Focus/Error/Disabled), 5 variant axes (Mode/Size/State/Error/Filled), 3 sizes; design intent annotations absent (GAP-008)
- [[DateTimeRangeSelector.tokens]] — 8 colour tokens covering background, border, text, focus ring, disabled surface; 5 typography tokens; 8 hardcoded spacing/radius values; semantic names CSS-derived, unverified against UI-Foundations (GAP-002); dark mode unextracted (GAP-009)
- [[DateTimeRangeSelector.usage]] — 8 Do/Don't pairs covering picker type, predefined-ranges visibility, time-row visibility, Finish commit boundary, placeholder vs pre-fill, validation, isDisabled semantics, full localisation (editorial — no Figma Do/Don't cards)
- [[DateTimeRangeSelector.accessibility]] — ARIA roles (inferred, verify against DOM — GAP-006), keyboard navigation, screen reader guidance, WCAG 2.1 AA checklist (3 items pending token confirmation — GAP-007)
- [[DateTimeRangeSelector.platform]] — no PUI requirements
- [[DateTimeRangeSelector.composition]] — composes Calendar, DateTimeRangePicker, DateTimeRangeSelectorPredefinedList; sibling of DateTimeSelector; ingredient in analytics filter bars and billing window selectors
