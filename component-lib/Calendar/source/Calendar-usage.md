---
component: Calendar
package: "@8x8/oxygen-calendar"
category: date_time
role: usage
role_description: "Usage guidelines — editorial, compiled from the published Oxygen docs page and the extracted MCP/Figma artifacts"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from the published Oxygen docs page (https://oxygen.8x8.com/components/calendar/usage, fetched 2026-05-12) cross-referenced with extracted MCP/Figma artifacts — NOT from Figma Do/Don't card frames. The previous Calendar-usage.md (figma-extract-usage output, 2026-05-08) is preserved as the Figma examples page reference appendix below. Re-run /doc-audit Calendar after creation; replace pairs with figma-extract-usage output when a Figma ↳ Calendar examples page is populated with Do/Don't cards."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Calendar/props]]"
  - "[[Calendar/examples]]"
  - "[[Calendar/tokens]]"
  - "[[Calendar/accessibility]]"
  - "[[Calendar/Calendar-figma]]"
  - "[[Calendar/Calendar-audit]]"
tags:
  - oxygen
  - component/Calendar
  - role/usage
  - stage/editorial
  - category/date_time
---
<!-- SOURCE: editorial — published Oxygen docs page (https://oxygen.8x8.com/components/calendar/usage, fetched 2026-05-12) + extracted MCP/Figma artifacts -->
<!-- FIGMA EXAMPLES PAGE: present (node 69971:10137) but contains illustration sections only — no ✅ Do / ❌ Don't card frames, so figma-extract-usage cannot produce editorial Do/Don't pairs -->
<!-- GROUNDING: full — props.md, examples.md, tokens.md, accessibility.md, Calendar-figma.md, Calendar-audit.md, published docs page -->
<!-- DRAFTED: 2026-05-12 -->
<!-- MODE: docs-mirrored -->
<!-- PAIRS: 7 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output if Do/Don't cards are ever added to the Figma "↳ Calendar examples" page (node 69971:10137) -->

# Calendar — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [Calendar-figma.md](./Calendar-figma.md)

> **Editorial guidance — mirrors the published Oxygen docs page.** The Figma `↳ Calendar examples` page (node 69971:10137) contains illustration sections (date-picker layouts, breakpoints, popovers, 90-day limit, intraday) but **no `✅ Do —` / `❌ Don't —` card frames**, so `figma-extract-usage` cannot produce editorial Do/Don't pairs. The pairs below are transcribed from the published Oxygen docs page for Calendar (`https://oxygen.8x8.com/components/calendar/usage`, fetched 2026-05-12) and cross-validated against [props.md](./props.md), [examples.md](./examples.md), [accessibility.md](./accessibility.md), and [Calendar-figma.md](./Calendar-figma.md). Replace with `figma-extract-usage` output if Do/Don't cards are ever added to the examples page.

A Calendar lets users **select a single date or a range of dates** — past, present, or future — with optional time selection. It is the visual surface behind every date input in 8x8 product surfaces: scheduling, reporting windows, filters, and call-history queries. Two display modes share a single component: a single-date picker and a date-range picker, both driven by the `displayMode` prop ([props.md:67](./props.md)).

---

## Overview

The component exposes two variants through one API:

| Variant | API | Use for | Notes |
|---------|-----|---------|-------|
| Single date | `displayMode="date"` (default) | Picking one specific calendar day | Selecting a date closes the menu and populates the input. |
| Date range | `displayMode="dateRange"` | Picking a start + end day (optionally with start/end time and a predefined-ranges panel) | First click sets `startDate`, second sets `endDate`; the change is **committed by clicking Apply**, not by the second click alone. |

The default range layout shows two months side-by-side with a predefined-ranges panel and Reset / Cancel / Apply action buttons ([Calendar-figma.md:51](./Calendar-figma.md)). The single layout is a 312 × 348 px standalone month grid ([Calendar-figma.md:67](./Calendar-figma.md)).

**Source:** Published docs — Overview section · [props.md:67](./props.md) · [Calendar-figma.md:107](./Calendar-figma.md).

---

## Anatomy

### Single date calendar ([Calendar-figma.md:67](./Calendar-figma.md))

1. **Navigation** — `←` previous-month, month dropdown, year dropdown, `→` next-month. The arrow buttons take their accessible name from `prevMonthLabel` / `nextMonthLabel` ([props.md:85](./props.md)).
2. **Days of the week** — weekday header row, format controlled by `weekDayDisplayFormat` ([props.md:80](./props.md), default `'EE'`).
3. **Date grid** — 40 × 40 px day cells. Today is marked with a dot; the selected day is filled.
4. **Title** — `monthDisplayFormat` ([props.md:81](./props.md), default `'MMMM yyyy'`).
5. **Calendar menu** — the popover container itself (border `--ui/ui01`, radius 6 px, shadow `--ui/shadow01`).

The calendar opens from a date input on the consuming surface — the input is a sibling concern, **not** part of the Calendar component.

### Date range calendar ([Calendar-figma.md:51](./Calendar-figma.md))

In addition to navigation, weekday row, and date grid:

6. **Predefined ranges panel** _(optional, 148 px wide)_ — "Today / Last hour / Yesterday / Last 7 days / This month / Last month / Last 3 months / This year / Last year / Custom". Controlled by the Figma boolean `predefinedRanges` ([Calendar-figma.md:125](./Calendar-figma.md)).
7. **Date and time range inputs** _(optional)_ — From / To date inputs and Start / End time inputs at the top, gated by the Figma boolean `time` ([Calendar-figma.md:124](./Calendar-figma.md)).
8. **Action bar** — Reset · Cancel · Apply. **Apply commits the range** — until then, the user can cancel without side effects.

---

## Behavior

### States ([Calendar-figma.md:247](./Calendar-figma.md))

| # | State | Trigger | Visual | Token |
|---|-------|---------|--------|-------|
| 1 | Rest | Default | Day number in `--text/textcolor01`, transparent bg | `--text/textcolor01` |
| 2 | Hover (day) | Pointer over a valid day | Cell bg → `--ui/ui02` | `--ui/ui02` |
| 3 | Focus (day) | Keyboard `Tab` / arrows | 2 px ring in `--interactive/focus01` + white inset shadow | `--interactive/focus01` |
| 4 | Selected (day) | Click or Enter / Space | Filled circle `--actions/action01`; text → white | `--actions/action01` |
| 5 | Current day | Today | Dot indicator below the day number | `--actions/action01` |
| 6 | In-range | Range mode, between `startDate` and `endDate` | Cell bg → `--ui/ui01` | `--ui/ui01` |
| 7 | Disabled | `disabledDates` or outside `minDate`/`maxDate` | Greyed text (`--text/textcolor06`), `aria-disabled="true"`, tooltip via `disabledDateTooltip` | `--text/textcolor06` |
| 8 | Passive (dimmed) | Day belongs to the adjacent month | Greyed text, still focusable | `--text/textcolor06` |

> ⚠️ Token names above come from Figma's generated CSS, not the UI-Foundations variables panel — flagged as **GAP-002** / **GAP-007** in [Calendar-audit.md](./Calendar-audit.md). Treat the table as authoritative for structure; defer to UI-Foundations once token mapping is confirmed.

**Source:** Published docs — States · [Calendar-figma.md:247](./Calendar-figma.md) · [accessibility.md:32](./accessibility.md).

---

## Sizes & responsive layout

The Calendar has no `size` prop — it adapts via `months` ([props.md:68](./props.md)) and breakpoint-driven layout shifts. From [Calendar-figma.md:235](./Calendar-figma.md):

| Breakpoint | Predefined ranges | Layout |
|------------|------------------|--------|
| ≥ 769 px | optional | Dual-month grid (default `months={2}`) |
| 541–768 px | optional | Dual-month, compact |
| 320–540 px | optional | **Single-month, stacked** — set `months={1}` |

The predefined-ranges panel is `148px` wide and is hidden by default on narrow surfaces — it would otherwise dominate the viewport.

---

## Placement

Calendars are popovers: they open from a date input and overlay the surface. From the published docs Behavior sections:

- **Open trigger:** the user clicks the date input field; the popover anchors to it.
- **Single-date close:** selecting a date **closes the menu and populates the input** immediately — no Apply step.
- **Range close:** the popover **stays open** until the user clicks Apply (or Cancel / Reset). This is intentional — a range is a two-click decision and intermediate state should not commit.

Don't render a Calendar inline without a triggering input — the popover affordance is what tells users "this is editable".

---

## Best practices

### When to use

- When asking the user for an **exact or approximate date** (single or range).
- When the user is required to **schedule tasks** (e.g. report generation, follow-ups).
- When the user needs to **pick a reporting window** — the predefined-ranges panel is the fastest path for "Last 7 days", "This month", "Last quarter".

### When not to use

| Situation | Why | Use instead |
|-----------|-----|-------------|
| The date is not required by the underlying task | Adds friction without value — reduce content on the page. | Omit the field entirely. |
| A single date is required and you reach for the range picker | The two-click + Apply pattern overshoots a one-decision task and hides the action behind extra steps. | `displayMode="date"`. See Pair 1. |
| A free-form text date is needed (e.g. "around Q3", "TBD") | Calendar enforces a concrete `Date` — placeholder semantics are lost. | A plain text input or a dedicated picker for fuzzy dates. |
| Selecting a time only (no date) | Calendar always picks a day — time inputs are an _addition_, not a substitute. | `TimePicker` (see DateTimeSelector siblings). |

**Source:** Published docs — Best Practices section · [props.md:67](./props.md).

---

## Do / Don't

### Pair 1 — Pick the variant by selection type

#### ✅ Do — Use `displayMode="date"` for a single date

When the task is "pick one day", the single-date variant is faster (one click, auto-close, auto-populate) and lighter on screen real estate (312 px vs 788 px).

```tsx
<Calendar
  date={date}
  onDateChange={setDate}
  displayMode="date"
/>
```

#### ❌ Don't — Reach for the range picker for a one-date task

The range variant requires the user to click twice and then click Apply. For a single date that's three interactions where one would do, and the Apply step blocks them on a control they don't need.

```tsx
{/* Wrong — range picker for a single-date task */}
<Calendar
  range={range}
  onRangeChange={setRange}
  displayMode="dateRange"
/>
```

**Source:** Published docs — "When not to use" (Date Range Calendar) · [examples.md:29](./examples.md) · [examples.md:48](./examples.md).

---

### Pair 2 — Always label the month navigation buttons

#### ✅ Do — Pass localized `prevMonthLabel` and `nextMonthLabel`

The `←` / `→` arrows have no visible text. The accessible name comes entirely from these props ([accessibility.md:41](./accessibility.md)). Without them, screen readers announce the buttons as unlabelled — failing WCAG 4.1.2.

```tsx
<Calendar
  date={date}
  onDateChange={setDate}
  prevMonthLabel="Previous month"
  nextMonthLabel="Next month"
/>
```

#### ❌ Don't — Ship the calendar with bare arrow icons

```tsx
{/* Wrong — nav arrows have no accessible name */}
<Calendar date={date} onDateChange={setDate} />
```

**Source:** Published docs — Anatomy (Navigation) · [props.md:85](./props.md) · [accessibility.md:41](./accessibility.md) · [accessibility.md:66](./accessibility.md).

---

### Pair 3 — Use `disabledDates` + `disabledDateTooltip` for selection limits

#### ✅ Do — Drive limits through the API, with a localized tooltip explaining why

This is the **canonical pattern for the 90-day report window** illustrated on the Figma examples page ([Calendar-figma.md:126](./Calendar-figma.md), [Calendar-usage.md → Figma examples reference](#figma-examples-page-reference) below). The Calendar API has **no dedicated `maxRangeDays` prop** today ([Calendar-audit.md:279](./Calendar-audit.md), GAP-011). Build the window with `disabledDates` and surface the reason via `disabledDateTooltip` so keyboard and screen-reader users hear the constraint, not just see it.

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

#### ❌ Don't — Hide the limit by silently disabling cells

A disabled cell with no tooltip tells the user nothing — they click, nothing happens, and they don't know why. Screen-reader users get even less, because `aria-disabled` without an associated reason announces only "dimmed, button".

```tsx
{/* Wrong — limit is enforced but never explained */}
<Calendar
  displayMode="dateRange"
  range={range}
  onRangeChange={setRange}
  disabledDates={buildDisabledDates(windowStart)}
/>
```

> 🔖 **GAP-011 (CONFLICT, resolved 2026-05-12 — Option A).** The 90-day mode is a first-class Figma property (`90 days` boolean, [Calendar-figma.md:126](./Calendar-figma.md)) without a dedicated API equivalent. Option A was chosen: document the `disabledDates` + `disabledDateTooltip` workaround as the canonical pattern (above). If Calendar gains a `maxRangeDays` prop in a future release, prefer that and update this pair. See [Calendar-audit.md](./Calendar-audit.md) GAP-011.

**Source:** Published docs — Date Range Calendar / States (Disabled) · [examples.md:69](./examples.md) · [accessibility.md:65](./accessibility.md) · [Calendar-audit.md:279](./Calendar-audit.md) (GAP-011).

---

### Pair 4 — Require an explicit Apply for a range change

#### ✅ Do — Keep the Reset / Cancel / Apply action bar in range mode

A range is a two-click decision (start + end). The Apply step gives the user a moment to confirm, cancel, or adjust before the value commits to the consuming form/filter. It also gives keyboard users a stable focus target after the second click.

```tsx
<Calendar
  displayMode="dateRange"
  range={range}
  onRangeChange={setRange}
  /* The action bar (Reset · Cancel · Apply) is rendered by the
     consuming Date-range popover, not by Calendar itself — see
     DateTimeRangeSelector. Don't auto-commit on the second click. */
/>
```

#### ❌ Don't — Commit the range as soon as the second day is clicked

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

**Source:** Published docs — Date Range Calendar > Behavior · [Calendar-figma.md:55](./Calendar-figma.md) (Action bar row).

---

### Pair 5 — Let `locale` and `date-fns` format the dates

#### ✅ Do — Pass a `date-fns` locale and let the component format everything

Date format expectations vary by locale ("the US uses M/D/Y, most other locations use D/M/Y" — published docs). Hand-formatting dates in the consuming page leads to drift: today's "5/12/2026" reads as 12 May to a US user and 5 December to a UK one. Pass `locale`, set `weekStartsOn`, and let `date-fns` handle weekday and month names.

```tsx
import { fr } from 'date-fns/locale';

<Calendar
  date={date}
  onDateChange={setDate}
  locale={fr}
  dateOptions={{ weekStartsOn: 1 }} // Monday-first
/>
```

#### ❌ Don't — Override formatting with a hand-rolled US format

```tsx
{/* Wrong — assumes M/D/Y for every locale */}
<Calendar
  date={date}
  onDateChange={setDate}
  monthDisplayFormat="M/d/yyyy"
/>
```

**Source:** Published docs — Date Format subsection · [props.md:84](./props.md) · [examples.md:105](./examples.md) · [examples.md:119](./examples.md).

---

### Pair 6 — Surface predefined ranges for common reporting windows

#### ✅ Do — Use the predefined-ranges panel for "Today / Last 7 days / This month / …"

Most reporting flows reach for the same handful of windows. The predefined-ranges panel ([Calendar-figma.md:56](./Calendar-figma.md), 148 px) makes those one click instead of two-clicks-plus-Apply. Reserve the day grid for the cases that don't fit a preset.

```tsx
{/* Composed surface — Calendar inside DateTimeRangeSelector,
    which owns the predefined-ranges panel. */}
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

#### ❌ Don't — Force the user to hand-pick a window the panel already supports

If the surface is a report filter and 80 % of users want "Last 7 days", surfacing only the day grid burns four clicks per query and adds two extra tab stops.

**Source:** Published docs — Date Range Calendar / Anatomy (Predetermined range) · [Calendar-figma.md:56](./Calendar-figma.md) · existing Figma annotation in the [Figma examples page reference](#figma-examples-page-reference) below.

---

### Pair 7 — Choose layout by breakpoint, don't hardcode dual-month

#### ✅ Do — Collapse to a single month below 540 px

Two 280-px month columns plus the predefined-ranges panel exceeds the width of a phone. Below 540 px, switch to `months={1}` and stack the predefined-ranges panel above the grid (or hide it).

```tsx
const isNarrow = useMediaQuery('(max-width: 540px)');

<Calendar
  displayMode="dateRange"
  range={range}
  onRangeChange={setRange}
  months={isNarrow ? 1 : 2}
/>
```

#### ❌ Don't — Hardcode `months={2}` on every surface

```tsx
{/* Wrong — overflows narrow viewports */}
<Calendar
  displayMode="dateRange"
  range={range}
  onRangeChange={setRange}
  months={2}
/>
```

**Source:** Published docs — Anatomy (responsive layout) · [Calendar-figma.md:235](./Calendar-figma.md) · existing breakpoint annotation in the [Figma examples page reference](#figma-examples-page-reference) below · [examples.md:96](./examples.md).

---

## Related components

The published docs page lists these neighbours:

- **Time selector** — paired with Calendar in range mode to add start/end time inputs (the Figma `time` boolean, [Calendar-figma.md:124](./Calendar-figma.md)).
- **Text input** — the surface that the Calendar popover anchors to. Calendar is not standalone; it always opens from an input.
- **Forms** — the pattern that hosts most Calendar usage.

From the extracted artifacts, two further Oxygen components compose Calendar in practice:

- **`DateTimeSelector`** — single-date input + Calendar popover wrapper. See [DateTimeSelector/](../DateTimeSelector/).
- **`DateTimeRangeSelector`** — range input + Calendar popover + predefined ranges + action bar. See [DateTimeRangeSelector/](../DateTimeRangeSelector/).

<!-- TODO: confirm whether `Popover` and `Tooltip` are listed under "Related" on the published docs page (the page fetched 2026-05-12 lists Time selector + Text input + Forms only). -->

---

## Accessibility quick reference

Cross-references to [accessibility.md](./accessibility.md):

- The day grid renders as `role="grid"` with `role="gridcell"` children ([accessibility.md:34](./accessibility.md)).
- Today is marked with `aria-current="date"`; the selected day with `aria-selected="true"` ([accessibility.md:38](./accessibility.md)).
- Disabled days carry `aria-disabled="true"` and **remain in the tab order** so the `disabledDateTooltip` is announced ([accessibility.md:37](./accessibility.md), [accessibility.md:65](./accessibility.md)).
- `Tab`, arrow keys, `Enter`/`Space`, `Page Up`/`Page Down`, `Home`/`End` are all wired ([accessibility.md:48](./accessibility.md)). Keyboard behavior follows the ARIA Date Picker pattern — verify against the implementation per the note at [accessibility.md:59](./accessibility.md).
- Always supply `prevMonthLabel` / `nextMonthLabel` (Pair 2) and `locale` (Pair 5).
- Wrap the consuming surface in an `aria-live="polite"` region so the selection is announced ([accessibility.md:42](./accessibility.md), [accessibility.md:68](./accessibility.md)).
- WCAG 1.4.3 (Contrast) and 2.4.7 (Focus Visible) are marked **Verify** in [accessibility.md:78](./accessibility.md) — they depend on tokens that are still unresolved (GAP-002, GAP-007 in [Calendar-audit.md](./Calendar-audit.md)).

---

## Gaps

| Item | Type | Description |
|------|------|-------------|
| Figma Do/Don't cards | SOURCE_GAP (GAP-003) | The `↳ Calendar examples` page (node 69971:10137) has illustration sections but no `✅ Do —` / `❌ Don't —` frames. Pairs above are editorially transcribed from the published Oxygen docs page (`https://oxygen.8x8.com/components/calendar/usage`, fetched 2026-05-12). Re-run `figma-extract-usage` if cards are added. |
| 90-day limit API | CONFLICT (GAP-011, **blocker**) | Figma exposes a `90 days` boolean ([Calendar-figma.md:126](./Calendar-figma.md)); the API has no `maxRangeDays` equivalent. Pair 3 documents the recommended `disabledDates` + `disabledDateTooltip` workaround. If the component team adds a dedicated prop, update Pair 3. Tracked in [Calendar-audit.md:279](./Calendar-audit.md). |
| Token names sourced from CSS, not UI-Foundations variables panel | SOURCE_GAP (GAP-002, GAP-007) | The States table cites `--ui/ui01`, `--actions/action01`, etc. as they appear in Figma's generated CSS — the canonical token names from the UI-Foundations library (file key `iVY5nI8JAxM05Apnnvozzs`) have not been confirmed. WCAG 1.4.3 / 2.4.7 are marked **Verify** until resolved. |
| Storybook canonical examples | SOURCE_GAP (GAP-001) | The 8 snippets in [examples.md](./examples.md) are derived from prop descriptions, not canonical Storybook stories. Confirm with the component team. |
| Type shapes for `DateRange` / `DateOptions` | DOC_GAP (GAP-004, GAP-005) | `range` prop's `DateRange` interface and `dateOptions`'s `DateOptions` interface are not fully spelled out in [props.md:66](./props.md) / [props.md:78](./props.md). Auto-fixable. |
| `enableMaxWidth` default | DOC_GAP (GAP-006) | Default value not documented at [props.md:87](./props.md). Look up in source. |
| Keyboard interactions verified | SOURCE_GAP (WARN-001 in audit) | Page Up/Down, Home/End behavior is documented from the ARIA APG pattern, not confirmed against `@8x8/oxygen-calendar` source. Spot-check before publishing. |
| Dark mode | SOURCE_GAP (WARN-002 in audit) | Figma component set has only a `light` mode variant ([Calendar-figma.md:107](./Calendar-figma.md)). Dark mode is "likely CSS-token-driven at runtime" — unconfirmed. |
| Anatomy numbering parity with published docs | DOC_GAP | The published docs list 6 single + 8 range anatomy items; the lists above adopt the same numbering. Re-verify if the docs page changes. |
| "Related" list completeness | DOC_GAP | Published docs list Time selector + Text input + Forms only; the additions (`DateTimeSelector`, `DateTimeRangeSelector`) are derived from sibling folder presence. Confirm with the docs team. |

---

## Figma examples page reference

The `↳ Calendar examples` Figma page (node 69971:10137) contains five illustration sections — preserved here from the prior `figma-extract-usage` output (2026-05-08) so the Figma annotations remain searchable in the doc set.

### Page sections

| Section | Description |
|---------|-------------|
| Date picker examples | Default range and single calendar in light mode |
| Date picker range responsive | Breakpoint demonstrations (992→769, 768→541, 540→320) with/without predefined ranges panel |
| Popovers inside Date picker | Predefined ranges popover, time popover, month picker popover |
| 90 days limit | Disabled date states, tooltip behaviour on hover/focus |
| Intraday | Intraday toggle on/off and intraday info tooltip |

### Verbatim annotations

**Popovers inside Date picker**

> **Predefined ranges popover sizing:** For predefined ranges popover, the max-height is set to 400px, the width is set to 300px.

> **Predefined ranges trigger:** Predefined ranges list will appear on click on the dropdown button.

> **Time / month / year popovers:** For time, month and year popovers, the max-height is set to 240px.

**90 days limit**

> **Context:** Some reports have a limit of 90 days for stored data.

> **Disabled dates:** If the dates are not in the 90 days segment, the state for those dates will be disabled.

> **Tooltip on hover:** On hover — tooltip is displayed.

> **Tooltip on focus:** On focus — tooltip is displayed.

> **90-day boundary indicator:** Persistent details. *(references a Marker component placed at the 90-day boundary in the calendar grid)*

### Breakpoint behaviour

| Breakpoint range | Predefined ranges | Layout |
|-----------------|------------------|--------|
| 992 → 769 px | Visible | Dual month + ranges panel |
| 992 → 769 px | Hidden | Dual month only |
| 768 → 541 px | Visible | Dual month + ranges panel |
| 768 → 541 px | Hidden | Dual month, narrower |
| 540 → 320 px | Visible | Single month + stacked ranges |
| 540 → 320 px | Hidden | Single month only |

---

_Source: Published Oxygen docs page (`https://oxygen.8x8.com/components/calendar/usage`, fetched 2026-05-12) · Cross-referenced with Oxygen MCP and Figma extraction (2026-05-08) · Editorial draft 2026-05-12_
