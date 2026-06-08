---
component: DateTimeSelector
status: draft
package: "@8x8/oxygen-date-time-selector"
category: date_time
figma: "https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp?node-id=80239-8235"
variants:
  - Light
  - Dark
  - Large
  - Medium
  - Small
props:
  - closeOnDateChange: boolean
  - finishButtonLabel: string
  - isClearable: boolean
  - isLoading: boolean
  - loadingMessage: string
  - onBlur: function
  - onDateChange: function
  - onFocus: function
  - titleFormatPattern: string
  - value: Date
subcomponents:
  - "[[_base_form_label]]"
  - "[[_base_form_hint]]"
  - "[[Icon Button]]"
related:
  - "[[DateTimeRangeSelector]]"
  - "[[Calendar]]"
patterns:
  - "[[Scheduling Form]]"
  - "[[Filter Bar]]"
tokens:
  - "--ui/ui05"
  - "--text/textcolor01"
  - "--text/textcolor02"
  - "--error/error01"
  - "--interactive/focus01"
spokes:
  - "[[DateTimeSelector.props]]"
  - "[[DateTimeSelector.anatomy]]"
  - "[[DateTimeSelector.tokens]]"
  - "[[DateTimeSelector.usage]]"
  - "[[DateTimeSelector.accessibility]]"
  - "[[DateTimeSelector.platform]]"
  - "[[DateTimeSelector.composition]]"
tags:
  - component
  - date_time
  - interactive
---

## Overview

DateTimeSelector is a 320 px form field that opens a popover with an embedded Calendar grid for selecting a single date and time. It is the standard single-date control for forms, scheduling flows, and surfaces where a user commits to one moment in time. The Figma trigger component set (node `80239:8235`) is shared with `DateTimeRangeSelector` — `DateTimeSelector` uses `value: Date` (single); `DateTimeRangeSelector` uses the same trigger with range semantics.

## Spokes

- [[DateTimeSelector.props]] — 10 props including value, onDateChange, closeOnDateChange
- [[DateTimeSelector.anatomy]] — 3 elements across 68 variants (2 modes × 3 sizes × 4 states × 2 error × 2 filled), 6 visual states
- [[DateTimeSelector.tokens]] — CSS-derived color and typography tokens; MCP tokens absent (major SOURCE_GAP)
- [[DateTimeSelector.usage]] — 6 Do/Don't pairs covering picker selection, commit pattern, loading state
- [[DateTimeSelector.accessibility]] — keyboard, ARIA, focus
- [[DateTimeSelector.platform]] — no PUI requirements
- [[DateTimeSelector.composition]] — subcomponents _base_form_label, _base_form_hint, Icon Button; related to DateTimeRangeSelector and Calendar
