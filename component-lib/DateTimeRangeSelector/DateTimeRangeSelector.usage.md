---
parent: "[[DateTimeRangeSelector]]"
section: usage
component: DateTimeRangeSelector
pipeline_stage: spec_ready
audit_verdict: "YES"
source_type: editorial
tags:
  - oxygen
  - component/DateTimeRangeSelector
  - role/spoke
  - section/usage
  - stage/spec_ready
  - category/date_time
---

<!-- source: figma-only — no Figma Do/Don't cards; editorial draft via usage-advisor skill (open mode) grounded in props.md, examples.md, accessibility.md, DateTimeRangeSelector-figma.md. Drafted 2026-05-12. Replace with figma-extract-usage output once a '↳ Date picker examples' page is added to Figma file 5YihJ5WuDvnvrlrRMC4sBp. -->

## Usage Guidelines

> **Editorial — no Figma Do/Don't cards.** No `↳ Date picker examples` page exists in the UI-components Figma file (`5YihJ5WuDvnvrlrRMC4sBp`). All pairs are grounded in the extracted artifacts. Replace with `figma-extract-usage` output once Do/Don't cards exist.

A `DateTimeRangeSelector` lets users select a start + end date, optionally with times, from a 320px trigger input that opens a popover with the Calendar range picker, an optional predefined-ranges panel, and an optional time-selector row.

---

### Pair 1 — Pick the right picker for the selection type

#### ✅ Do — Use `DateTimeRangeSelector` only when the task is a span

```tsx
<DateTimeRangeSelector
  dateTimeRange={range}
  predefinedRange={selectedPredefinedRange}
  onRangeChange={onRangeChange}
/>
```

#### ❌ Don't — Reach for the range picker for a single date

For one-date tasks the Finish-to-commit flow is three interactions where one would do.

```tsx
{/* Wrong — single date through the range picker */}
<DateTimeRangeSelector
  dateTimeRange={{ startDate: oneDate, endDate: oneDate }}
  onRangeChange={({ dateTime }) => setOneDate(dateTime?.startDate)}
/>
```

---

### Pair 2 — Keep predefined ranges for analytics surfaces

#### ✅ Do — Leave the predefined-ranges panel visible for reporting/filtering

The default list covers the queries users actually run on dashboards and call-history views.

```tsx
<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  predefinedRanges={defaultRangesPlusCustom}
/>
```

#### ❌ Don't — Hide the panel unless the surface has no recurring windows

`hidePredefinedRanges` should be reserved for surfaces where every query is bespoke.

```tsx
{/* Wrong on a reporting surface */}
<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  hidePredefinedRanges
/>
```

---

### Pair 3 — Show the time row only when intraday matters

#### ✅ Do — Keep `hideTime={false}` for billing, scheduling, and call-history windows

```tsx
<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  startTimeLabel="Start time"
  endTimeLabel="End time"
/>
```

#### ❌ Don't — Force users to set times for a day-granularity decision

Exposing time inputs for date-only decisions introduces off-by-one bugs across timezone changes.

```tsx
{/* Right for a day-only filter */}
<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  hideTime
/>
```

---

### Pair 4 — Commit through `Finish` / `onRangeChange`, never on the second click

#### ✅ Do — Tie side effects to `onRangeChange`

`onRangeChange` fires when the user presses **Finish** or **Clear** — not when the second calendar day is clicked.

```tsx
const onRangeChange = ({ dateTime, predefinedRange } = {}) => {
  if (predefinedRange) setState({ selectedPredefinedRange: predefinedRange });
  else if (dateTime)    setState({ selectedDateTime: dateTime });
  else                  setState(defaultState); // Clear pressed
  refetchReport();
};
```

#### ❌ Don't — Wire side effects to `onOpen` / `onClose`

`onClose` fires even when the user cancels with Escape.

```tsx
{/* Wrong */}
<DateTimeRangeSelector
  onClose={() => refetchReport(range)}
/>
```

---

### Pair 5 — Use the placeholder, don't pre-fill "today" to look populated

#### ✅ Do — Leave the trigger empty until the user picks a range

```tsx
<DateTimeRangeSelector
  dateTimeRange={undefined}
  predefinedRange={{ id: 'CUSTOM' }}
  onRangeChange={onRangeChange}
  placeholder="Select date range"
/>
```

#### ❌ Don't — Seed `dateTimeRange` with `today` / `today`

A pre-filled range pretends the user has made a selection.

```tsx
{/* Wrong */}
<DateTimeRangeSelector
  dateTimeRange={{ startDate: new Date(), endDate: new Date() }}
  onRangeChange={onRangeChange}
/>
```

---

### Pair 6 — Surface validation in the right place

#### ✅ Do — Use `hasError` for trigger-level errors and `endTimeErrorMessage` for time validation

```tsx
<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  hasError={isSubmitted && !range}
  endTimeErrorMessage={t('rangePicker.endBeforeStart', 'End time cannot be before start time')}
/>
```

#### ❌ Don't — Silently swap start and end behind the user's back

Auto-swapping mutates user intent without announcing it.

```tsx
{/* Wrong */}
const normalised = startDate <= endDate
  ? { startDate, endDate }
  : { startDate: endDate, endDate: startDate }; // user wasn't told
```

---

### Pair 7 — Use `isDisabled` for unavailability, not as an icon-hiding trick

#### ✅ Do — Use `isDisabled` only when the range genuinely cannot be edited

```tsx
<DateTimeRangeSelector
  dateTimeRange={savedRange}
  isDisabled={!canEditFilter}
  onRangeChange={onRangeChange}
/>
```

#### ❌ Don't — Reach for `isDisabled` because the calendar icon "looks off" in Hover/Focus

The calendar icon is intentionally hidden in every non-Rest state — that's the design.

```tsx
{/* Wrong — disabling to hide a visual element breaks keyboard access */}
<DateTimeRangeSelector
  dateTimeRange={range}
  isDisabled
/>
```

---

### Pair 8 — Localise every visible string, not just the calendar

#### ✅ Do — Pass `locale` and localised label/button props together

```tsx
import { fr } from 'date-fns/locale';

<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  locale={fr}
  dateFormat="dd/MM/yyyy"
  placeholder={t('range.selectDateRange')}
  fromLabel={t('range.from')}
  toLabel={t('range.to')}
  startTimeLabel={t('range.startTime')}
  endTimeLabel={t('range.endTime')}
  finishButtonLabel={t('range.apply')}
  clearButtonLabel={t('range.reset')}
  customPredefinedRangeLabel={t('range.custom')}
  endTimeErrorMessage={t('range.endBeforeStart')}
/>
```

#### ❌ Don't — Pass `locale` and leave the rest in English

Half-localised UIs signal "this product wasn't built for me".

```tsx
{/* Wrong */}
<DateTimeRangeSelector locale={fr} />
```

---

## Edge cases

| Case | Guidance |
|------|----------|
| Data-retention window | Pass `otherCalendarProps={{ minDate, disabledDateTooltip }}` |
| Custom trigger | Use `inputRenderer={({ value, onClick }) => …}` — must preserve keyboard semantics (WARN-001) |
| Closing rules | Default: Escape, click outside, Finish, Clear. Add `customCloseHandlers` only for embedding popovers |
| Forwarding Calendar props | `otherCalendarProps` accepts any `CalendarProps` |
| Dark mode | Variants exist in Figma but token bindings unextracted (GAP-009) |
