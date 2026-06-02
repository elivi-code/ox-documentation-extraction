---
parent: "[[Calendar]]"
section: usage
source_type: editorial
---

## Usage

<!-- source: editorial — published Oxygen docs page (https://oxygen.8x8.com/components/calendar/usage, fetched 2026-05-12), cross-referenced with extracted MCP/Figma artifacts. NOT from Figma Do/Don't card frames. -->
<!-- STUB:GAP-003 source="Designer must create Do/Don't cards using the figma-draw template on the '↳ Calendar examples' page (node 69971:10137). Re-run figma-extract-usage after cards are added; replace these editorial pairs." -->

> **Editorial guidance.** The Figma `↳ Calendar examples` page (node 69971:10137) contains illustration sections but **no `✅ Do` / `❌ Don't` card frames**, so the pairs below are transcribed from the published Oxygen docs page and cross-validated against the extracted props, examples, accessibility, and Figma specs. Replace with `figma-extract-usage` output once Do/Don't cards exist.

A Calendar lets users **select a single date or a range of dates** — past, present, or future — with optional time selection. It is the visual surface behind every date input in 8x8 product surfaces: scheduling, reporting windows, filters, and call-history queries. Two display modes share one API, driven by `displayMode` ([[Calendar.props]]).

### When to use

- Asking the user for an **exact or approximate date** (single or range).
- The user must **schedule tasks** (report generation, follow-ups).
- The user needs to **pick a reporting window** — the predefined-ranges panel is the fastest path for "Last 7 days", "This month", "Last quarter".

### When not to use

| Situation | Why | Use instead |
|-----------|-----|-------------|
| The date is not required by the underlying task | Adds friction without value. | Omit the field entirely. |
| A single date is required and you reach for the range picker | The two-click + Apply pattern overshoots a one-decision task. | `displayMode="date"` (Pair 1). |
| A free-form text date is needed (e.g. "around Q3", "TBD") | Calendar enforces a concrete `Date` — placeholder semantics are lost. | A plain text input or a fuzzy-date picker. |
| Selecting a time only (no date) | Calendar always picks a day — time inputs are an addition, not a substitute. | `TimePicker` (see DateTimeSelector siblings). |

---

## Do / Don't

### Pair 1 — Pick the variant by selection type

**✅ Do — Use `displayMode="date"` for a single date.** When the task is "pick one day", the single-date variant is faster (one click, auto-close, auto-populate) and lighter on screen real estate (312 px vs 788 px).

```tsx
<Calendar date={date} onDateChange={setDate} displayMode="date" />
```

**❌ Don't — Reach for the range picker for a one-date task.** The range variant requires two clicks plus Apply — three interactions where one would do, and Apply blocks the user on a control they don't need.

```tsx
{/* Wrong — range picker for a single-date task */}
<Calendar range={range} onRangeChange={setRange} displayMode="dateRange" />
```

### Pair 2 — Always label the month navigation buttons

**✅ Do — Pass localized `prevMonthLabel` and `nextMonthLabel`.** The `←` / `→` arrows have no visible text; their accessible name comes entirely from these props ([[Calendar.accessibility]]). Without them, screen readers announce unlabelled buttons — failing WCAG 4.1.2.

```tsx
<Calendar
  date={date}
  onDateChange={setDate}
  prevMonthLabel="Previous month"
  nextMonthLabel="Next month"
/>
```

**❌ Don't — Ship the calendar with bare arrow icons.**

```tsx
{/* Wrong — nav arrows have no accessible name */}
<Calendar date={date} onDateChange={setDate} />
```

### Pair 3 — Use `disabledDates` + `disabledDateTooltip` for selection limits

**✅ Do — Drive limits through the API, with a localized tooltip explaining why.** This is the **canonical pattern for the 90-day report window** shown on the Figma examples page. The Calendar API has **no dedicated `maxRangeDays` prop** today (GAP-011). Build the window with `disabledDates` and surface the reason via `disabledDateTooltip` so keyboard and screen-reader users hear the constraint, not just see it.

```tsx
import { Calendar } from '@8x8/oxygen-calendar';
import { addDays, isBefore } from 'date-fns';

const windowStart = addDays(new Date(), -90);

<Calendar
  displayMode="dateRange"
  range={range}
  onRangeChange={setRange}
  disabledDates={buildDisabledDates(windowStart)}
  disabledDateTooltip={(day) =>
    isBefore(day, windowStart)
      ? t('calendar.outsideReportWindow', '90-day report limit — earlier data is not retained')
      : undefined
  }
/>
```

**❌ Don't — Hide the limit by silently disabling cells.** A disabled cell with no tooltip tells the user nothing; screen-reader users get only "dimmed, button".

```tsx
{/* Wrong — limit is enforced but never explained */}
<Calendar
  displayMode="dateRange"
  range={range}
  onRangeChange={setRange}
  disabledDates={buildDisabledDates(windowStart)}
/>
```

> 🔖 **GAP-011 (CONFLICT, resolved 2026-05-12 — Option A).** The 90-day mode is a first-class Figma property (`90 days` boolean) without a dedicated API equivalent. Option A was chosen: document the `disabledDates` + `disabledDateTooltip` workaround as the canonical pattern. If Calendar gains a `maxRangeDays` prop in a future release, prefer that and update this pair.

### Pair 4 — Require an explicit Apply for a range change

**✅ Do — Keep the Reset / Cancel / Apply action bar in range mode.** A range is a two-click decision (start + end); the Apply step lets the user confirm, cancel, or adjust before the value commits, and gives keyboard users a stable focus target after the second click.

```tsx
<Calendar
  displayMode="dateRange"
  range={range}
  onRangeChange={setRange}
  /* The action bar (Reset · Cancel · Apply) is rendered by the consuming
     Date-range popover, not by Calendar itself. Don't auto-commit on the
     second click. */
/>
```

**❌ Don't — Commit the range as soon as the second day is clicked.**

```tsx
{/* Wrong — second click commits without confirmation */}
<Calendar
  displayMode="dateRange"
  onRangeChange={(range) => {
    setRange(range);
    closePopover(); // ← removes the Cancel / Reset escape hatch
  }}
/>
```

### Pair 5 — Let `locale` and `date-fns` format the dates

**✅ Do — Pass a `date-fns` locale and let the component format everything.** Date format expectations vary by locale (US uses M/D/Y, most others D/M/Y). Hand-formatting in the consuming page leads to drift. Pass `locale`, set `weekStartsOn`, and let `date-fns` handle weekday and month names.

```tsx
import { fr } from 'date-fns/locale';

<Calendar
  date={date}
  onDateChange={setDate}
  locale={fr}
  dateOptions={{ weekStartsOn: 1 }} // Monday-first
/>
```

**❌ Don't — Override formatting with a hand-rolled US format.**

```tsx
{/* Wrong — assumes M/D/Y for every locale */}
<Calendar date={date} onDateChange={setDate} monthDisplayFormat="M/d/yyyy" />
```

### Pair 6 — Surface predefined ranges for common reporting windows

**✅ Do — Use the predefined-ranges panel for "Today / Last 7 days / This month / …".** Most reporting flows reach for the same handful of windows; the 148 px panel makes those one click instead of two-clicks-plus-Apply. Reserve the day grid for cases that don't fit a preset.

```tsx
{/* Composed surface — Calendar inside DateTimeRangeSelector, which owns the panel. */}
<DateTimeRangeSelector
  predefinedRanges={[
    { label: 'Today',       value: () => ({ startDate: today, endDate: today }) },
    { label: 'Last 7 days', value: () => ({ startDate: addDays(today, -7), endDate: today }) },
    { label: 'This month',  value: () => ({ startDate: startOfMonth(today), endDate: today }) },
  ]}
  range={range}
  onRangeChange={setRange}
/>
```

**❌ Don't — Force the user to hand-pick a window the panel already supports.** If 80% of users want "Last 7 days", surfacing only the day grid burns four clicks per query and adds two extra tab stops.

### Pair 7 — Choose layout by breakpoint, don't hardcode dual-month

**✅ Do — Collapse to a single month below 540 px.** Two 280-px month columns plus the predefined-ranges panel exceeds phone width. Below 540 px, switch to `months={1}` and stack (or hide) the panel.

```tsx
const isNarrow = useMediaQuery('(max-width: 540px)');

<Calendar
  displayMode="dateRange"
  range={range}
  onRangeChange={setRange}
  months={isNarrow ? 1 : 2}
/>
```

**❌ Don't — Hardcode `months={2}` on every surface.**

```tsx
{/* Wrong — overflows narrow viewports */}
<Calendar displayMode="dateRange" range={range} onRangeChange={setRange} months={2} />
```

---

## Placement

Calendars are popovers: they open from a date input and overlay the surface.

- **Open trigger:** the user clicks the date input field; the popover anchors to it.
- **Single-date close:** selecting a date **closes the menu and populates the input** immediately — no Apply step.
- **Range close:** the popover **stays open** until the user clicks Apply (or Cancel / Reset) — a range is a two-click decision and intermediate state should not commit.

Don't render a Calendar inline without a triggering input — the popover affordance is what tells users "this is editable". See [[Calendar.composition]] for the composing wrappers.
