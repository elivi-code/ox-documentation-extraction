---
component: DateTimeRangeSelector
package: "@8x8/oxygen-date-time-range-selector"
category: date_time
role: usage
role_description: "Usage guidelines — editorial, drafted from extracted MCP/Figma artifacts via the usage-advisor skill"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from the extracted MCP/Figma artifacts (props.md, examples.md, accessibility.md, DateTimeRangeSelector-figma.md) — NOT from Figma Do/Don't card frames. The Oxygen docs site URL for this component (https://oxygen.8x8.com/components/date-time-range-selector/usage) timed out during drafting; if/when a published page exists, replace this file with figma-extract-usage output once a '↳ Date picker examples' page is populated."
source_type: editorial
audit_verdict: null
siblings:
  - "[[DateTimeRangeSelector/props]]"
  - "[[DateTimeRangeSelector/examples]]"
  - "[[DateTimeRangeSelector/tokens]]"
  - "[[DateTimeRangeSelector/accessibility]]"
  - "[[DateTimeRangeSelector/DateTimeRangeSelector-figma]]"
  - "[[DateTimeRangeSelector/DateTimeRangeSelector-audit]]"
  - "[[Calendar/Calendar-usage]]"
tags:
  - oxygen
  - component/DateTimeRangeSelector
  - role/usage
  - stage/editorial
  - category/date_time
---
<!-- SKILL: usage-advisor (open mode) + Calendar-usage.md structural template -->
<!-- COMPONENT: DateTimeRangeSelector -->
<!-- SOURCE: editorial — extracted MCP/Figma artifacts (props.md, examples.md, accessibility.md, DateTimeRangeSelector-figma.md) + Oxygen MCP component README -->
<!-- FIGMA EXAMPLES PAGE: absent — no `↳ Date picker examples` page exists in UI-components file (5YihJ5WuDvnvrlrRMC4sBp); GAP-003 in DateTimeRangeSelector-audit.md -->
<!-- PUBLISHED DOCS PAGE: probed at https://oxygen.8x8.com/components/date-time-range-selector/usage — WebFetch timed out on 2026-05-12; mirror published guidance into this file on a future pass if/when reachable -->
<!-- GROUNDING: full — props.md, examples.md, tokens.md, accessibility.md, DateTimeRangeSelector-figma.md, DateTimeRangeSelector-audit.md present; pui.md intentionally absent (audit confirmed no PUI concerns) -->
<!-- DRAFTED: 2026-05-12 -->
<!-- MODE: editorial — author the canonical usage file directly (Calendar precedent, 2026-05-12) -->
<!-- PAIRS: 8 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output if Do/Don't cards are ever added to a `↳ Date picker examples` page in Figma file 5YihJ5WuDvnvrlrRMC4sBp -->

# DateTimeRangeSelector — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [DateTimeRangeSelector-figma.md](./DateTimeRangeSelector-figma.md) ·
> [Calendar — Usage Guidelines](../Calendar/Calendar-usage.md) (open picker panel — calendar grid, predefined ranges, time row).

> **Editorial guidance — no Figma Do/Don't cards.** No `↳ Date picker examples` page exists in the UI-components Figma file (`5YihJ5WuDvnvrlrRMC4sBp`); the published Oxygen docs URL timed out during drafting. The pairs below are drafted from the extracted artifacts (`props.md`, `examples.md`, `accessibility.md`, `DateTimeRangeSelector-figma.md`) and cross-referenced with the sibling [Calendar — Usage Guidelines](../Calendar/Calendar-usage.md), which documents the open picker panel itself. Replace this file with `figma-extract-usage` output once Do/Don't cards exist in Figma.

A `DateTimeRangeSelector` lets users **select a start + end date, optionally with start and end times**, from a 320 px trigger input that opens a popover with the Calendar range picker, an optional predefined-ranges panel, and an optional time-selector row. It is the standard control behind every analytics, reporting, billing, and call-history time-window filter in 8x8 product surfaces ([DateTimeRangeSelector-figma.md:38](./DateTimeRangeSelector-figma.md), [props.md:53](./props.md)).

---

## Overview

| Surface | API | Notes |
|---------|-----|-------|
| Trigger input | `DateTimeRangeSelector` (default export) | 320 px fixed-width input that displays the formatted range and opens the popover. |
| Open picker panel | rendered internally; or `DateTimeRangePicker` (named export) for custom triggers | Calendar grid + predefined-ranges panel + time selectors + `Finish` / `Clear` action bar. |
| Predefined ranges list | `DateTimeRangeSelectorPredefinedList` (named export) | Left panel; default list includes Last hour, Today, Yesterday, Last 7 days, This month, Last month, Last 3 months, This year, Last year, Custom ([props.md:154](./props.md)). |

The trigger input is the **shared Figma "Date picker" node `80239:8235`** ([DateTimeRangeSelector-figma.md:53](./DateTimeRangeSelector-figma.md)) — the same trigger that backs `DateTimeSelector`. The visible difference is the placeholder/value text: a single date for `DateTimeSelector`, a `"start – end"` string for `DateTimeRangeSelector`.

**Source:** [props.md:49](./props.md) · [DateTimeRangeSelector-figma.md:30](./DateTimeRangeSelector-figma.md).

---

## Anatomy

The trigger is documented here. For the open picker panel (calendar grid, predefined ranges, time row), see [Calendar — Figma Design Spec](../Calendar/Calendar-figma.md).

### Trigger ([DateTimeRangeSelector-figma.md:61](./DateTimeRangeSelector-figma.md))

1. **Label zone** — `_base_form_label`. Optional, default visible. Includes the label, an `*` required marker (red, `--error/error01`), and an `Icon Button` slot for an FAQ/help icon.
2. **Dropdown (trigger field)** — `320 × 48 px` (Large) / `40 px` (default API mapping) / `32 px` (Small). Renders the placeholder (`'Select Date Range'` by default, [props.md:86](./props.md)) or the formatted range string. The calendar icon is **visible in Rest state only** — hidden in Hover, Focus, Error, and Disabled.
3. **Hint / error zone** — `_base_form_hint`. Below the dropdown. Renders hint text or, when `hasError={true}`, the error message in `--error/error01`.

### Open picker panel ([Calendar-figma.md:51](../Calendar/Calendar-figma.md))

4. **Predefined ranges panel** *(optional, 148 px wide)* — gated by the `hidePredefinedRanges` prop ([props.md:74](./props.md)). Default list documented in [props.md:154](./props.md).
5. **Date and time range header** *(optional)* — From / To date inputs and Start / End time inputs. The time row is gated by `hideTime` ([props.md:75](./props.md)); the date inputs always show.
6. **Calendar grid** — dual-month range Calendar; see [Calendar — Usage Guidelines](../Calendar/Calendar-usage.md).
7. **Action bar** — **`Clear` · `Finish`** (default labels: `clearButtonLabel: 'Clear'` [props.md:63](./props.md), `finishButtonLabel: 'Finish'` [props.md:70](./props.md)). **`onRangeChange` fires on Finish or Clear only** ([props.md:84](./props.md)) — the second day-click does **not** commit. Many consuming surfaces relabel these to `'Apply'` / `'Reset'` ([examples.md:127](./examples.md)).

---

## Behavior

### States ([DateTimeRangeSelector-figma.md:238](./DateTimeRangeSelector-figma.md))

| # | State | Trigger | Visual change | Tokens (Light mode) |
|---|-------|---------|---------------|--------------------|
| 1 | Rest | Default | Placeholder or range value on `--ui/ui05` (#f4f3ee); calendar icon visible | `--ui/ui05`, `--text/textcolor02` (placeholder) / `--text/textcolor01` (filled) |
| 2 | Hover | Pointer over Dropdown | bg → `--interactive/hover06` (#ebeae1); calendar icon hidden | `--interactive/hover06` |
| 3 | Focus | Keyboard `Tab` | 2 px focus ring `--interactive/focus01` (#0056e0); calendar icon hidden | `--interactive/focus01` |
| 4 | Error | `hasError={true}` | 2 px red border `--error/error01` (#cb2233); calendar icon hidden; error message in hint zone | `--error/error01` |
| 5 | Disabled | `isDisabled={true}` | bg → `--interactive/disabled01` (#c8c8bd); filled text → `--interactive/disabled04` (#8d8b7e); not interactive; calendar icon hidden | `--interactive/disabled01`, `--interactive/disabled04` |
| 6 | Filled | `dateTimeRange` set | Placeholder replaced by formatted range string (`dateFormat` + `timeFormat`); text → `--text/textcolor01` | `--text/textcolor01` |

> ⚠️ Token names above come from Figma's generated CSS (Light mode), not the UI-Foundations variables panel — flagged as **GAP-002** in [DateTimeRangeSelector-audit.md](./DateTimeRangeSelector-audit.md). Dark mode token values are unverified — flagged as **GAP-009**.

**Source:** [DateTimeRangeSelector-figma.md:156](./DateTimeRangeSelector-figma.md) · [accessibility.md:50](./accessibility.md).

---

## Sizes

| API value | Figma variant | Trigger height | Total component height (with label + hint) |
|-----------|---------------|----------------|--------------------------------------------|
| `size="large"` (default) | `Size=Large` | 48 px | 92 px |
| — *(no API value)* | `Size=Medium` | 40 px | 84 px |
| `size="small"` | `Size=Small` | 32 px | 76 px |

The API exposes only `'large' \| 'small'` ([props.md:89](./props.md)); the Figma `Medium` variant exists in the component set but is not selectable via props. Treat `large` as the default surface and `small` for dense filter bars / table toolbars. Width is always **320 px fixed** ([DateTimeRangeSelector-figma.md:192](./DateTimeRangeSelector-figma.md)).

**Source:** [props.md:89](./props.md) · [DateTimeRangeSelector-figma.md:204](./DateTimeRangeSelector-figma.md).

---

## Placement

- **Always render the trigger input** — the popover opens from it. Don't render `DateTimeRangePicker` standalone except for embedded surfaces (e.g. inline filters in a SlideOut) where you provide your own trigger.
- **Width is 320 px** — don't stretch the trigger to fill its container; it will misalign with neighbouring 320 px Oxygen inputs and break visual rhythm.
- **Popover anchors to the trigger** and overlays the surface; the picker stays open until `Finish` or `Clear` is pressed, or `Escape` is hit, or one of the `customCloseHandlers` ([props.md:64](./props.md)) fires.

---

## Best practices

### When to use

- Selecting a **time window for an analytics or reporting view** (last 7 days, this month, custom range).
- Picking a **billing or scheduling window** that needs start and end **with intraday precision** — leave `hideTime={false}` (default).
- Filtering **historical records** (calls, tickets, events) by date range; pair with `predefinedRanges` for the common queries and `otherCalendarProps.minDate` for data-retention windows.

### When not to use

| Situation | Why | Use instead |
|-----------|-----|-------------|
| Picking a single date (not a range) | The two-click + `Finish` commit pattern is over-engineered for a one-decision task. | `DateTimeSelector` (sibling: same trigger, single-date semantics). See Pair 1 below. |
| Picking a single time (no date) | The component always picks dates first; time inputs are an addition. | `TimeSelector`. |
| Free-form / fuzzy dates ("around Q3", "TBD") | The component enforces concrete `Date` objects. | A plain text input. |
| Inline display of a fixed range (read-only summary) | A disabled trigger conveys "unavailable", not "informational". | A `Label` + formatted string. |

**Source:** [props.md:53](./props.md) · [examples.md:38](./examples.md) · [accessibility.md:72](./accessibility.md).

---

## Do / Don't

### Pair 1 — Pick the right picker for the selection type

#### ✅ Do — Use `DateTimeRangeSelector` only when the task is a span

Two dates, with or without time, are the canonical case. The Apply step, the two-click pattern, the predefined-range panel, and the dual-month grid all exist because the user is comparing two endpoints.

```tsx
<DateTimeRangeSelector
  dateTimeRange={range}                       // { startDate, endDate }
  predefinedRange={selectedPredefinedRange}
  onRangeChange={onRangeChange}
/>
```

#### ❌ Don't — Reach for the range picker for a single date

For one-date tasks the Finish-to-commit flow is three interactions where one would do, and the predefined-ranges panel is irrelevant. Use the sibling component.

```tsx
{/* Wrong — single date through the range picker */}
<DateTimeRangeSelector
  dateTimeRange={{ startDate: oneDate, endDate: oneDate }}
  onRangeChange={({ dateTime }) => setOneDate(dateTime?.startDate)}
/>
```

**Source:** [props.md:53](./props.md) · [props.md:67](./props.md) · [DateTimeRangeSelector-figma.md:32](./DateTimeRangeSelector-figma.md) (shared trigger between DateTimeSelector and DateTimeRangeSelector).

---

### Pair 2 — Keep predefined ranges for analytics surfaces

#### ✅ Do — Leave the predefined-ranges panel visible for reporting/filtering

The default list — `Last hour, Today, Yesterday, Last 7 days, This month, Last month, Last 3 months, This year, Last year, Custom` ([props.md:154](./props.md)) — covers the queries users actually run on dashboards and call-history views. Hiding it forces them through the full calendar for a one-click decision.

```tsx
<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  predefinedRanges={defaultRangesPlusCustom}  // or omit — default list is used
/>
```

#### ❌ Don't — Hide the panel unless the surface has no recurring windows

`hidePredefinedRanges` should be reserved for surfaces where every query is bespoke (e.g. a one-off audit screen). Hiding it on a dashboard filter turns "Last 7 days" from one click into eight.

```tsx
{/* Wrong on a reporting surface */}
<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  hidePredefinedRanges
/>
```

**Source:** [props.md:74](./props.md) · [props.md:154](./props.md) · [examples.md:83](./examples.md).

---

### Pair 3 — Show the time row only when intraday matters

#### ✅ Do — Keep `hideTime={false}` for billing, scheduling, and call-history windows

Default behavior: the picker shows `Start Time` / `End Time` inputs and a sub-day commit. Use it when the consuming flow's accuracy depends on hours/minutes — e.g. "calls between 09:00 and 17:00 yesterday".

```tsx
<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  startTimeLabel="Start time"
  endTimeLabel="End time"
/>
```

#### ❌ Don't — Force users to set times for a day-granularity decision

When the consuming feature only cares about calendar days, exposing time inputs creates two failure modes: users either ignore them (and silently pick 12:00 AM boundaries) or set them wrong (introducing off-by-one bugs across timezone changes). Set `hideTime`.

```tsx
{/* Right for a day-only filter */}
<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  hideTime
/>
```

**Source:** [props.md:75](./props.md) · [examples.md:95](./examples.md) · [DateTimeRangeSelector-figma.md:225](./DateTimeRangeSelector-figma.md).

---

### Pair 4 — Commit through `Finish` / `onRangeChange`, never on the second click

#### ✅ Do — Treat `Finish` as the commit boundary

`onRangeChange` fires when the user presses **Finish** or **Clear** ([props.md:84](./props.md)) — not when the second calendar day is clicked. That confirmation step is intentional: it gives users a reversible moment after picking start + end + (optional) times, and it gives keyboard users a stable focus target. Tie expensive side effects (data refetches, URL updates, analytics events) to `onRangeChange`.

```tsx
const onRangeChange = ({ dateTime, predefinedRange } = {}) => {
  if (predefinedRange) setState({ selectedPredefinedRange: predefinedRange });
  else if (dateTime)    setState({ selectedDateTime: dateTime });
  else                  setState(defaultState);   // Clear pressed
  refetchReport(/* ... */);                       // ← side effect at commit
};
```

#### ❌ Don't — Wire side effects to `onOpen` / `onClose` or to intermediate state

`onOpen` / `onClose` ([props.md:82](./props.md), [83](./props.md)) are for analytics or focus management, not data commits. Refetching on close would fire even when the user cancelled, and refetching on every intermediate state would thrash the network during a range pick.

```tsx
{/* Wrong — refetch on close fires for cancellations too */}
<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={setRange}
  onClose={() => refetchReport(range)}   // ← also runs when nothing was changed
/>
```

**Source:** [props.md:84](./props.md) · [examples.md:52](./examples.md) (controlled-range pattern) · [accessibility.md:56](./accessibility.md) (Escape closes without applying).

---

### Pair 5 — Use the placeholder, don't pre-fill "today" to look populated

#### ✅ Do — Leave the trigger empty until the user picks a range

`placeholder` defaults to `'Select Date Range'` ([props.md:86](./props.md)). An empty trigger reads as "this is an editable filter" — Filled=False in Figma ([DateTimeRangeSelector-figma.md:133](./DateTimeRangeSelector-figma.md)). The consuming surface should default to *no filter applied*, not to a fabricated range.

```tsx
<DateTimeRangeSelector
  dateTimeRange={undefined}                  // unfilled
  predefinedRange={{ id: 'CUSTOM' }}         // matches initial state in examples
  onRangeChange={onRangeChange}
  placeholder="Select date range"            // or a localised string
/>
```

#### ❌ Don't — Seed `dateTimeRange` with `today` / `today` to "look populated"

A pre-filled range pretends the user has made a selection. Filters then run against a value the user didn't choose, the Clear button has a non-obvious effect, and the placeholder copy never gets a chance to communicate intent.

```tsx
{/* Wrong — fakes a user selection */}
<DateTimeRangeSelector
  dateTimeRange={{ startDate: new Date(), endDate: new Date() }}
  onRangeChange={onRangeChange}
/>
```

**Source:** [props.md:86](./props.md) · [examples.md:47](./examples.md) (`defaultState` pattern) · [DateTimeRangeSelector-figma.md:120](./DateTimeRangeSelector-figma.md).

---

### Pair 6 — Surface validation in the right place

#### ✅ Do — Use `hasError` for trigger-level errors and `endTimeErrorMessage` for time validation

The component has **two error surfaces**: `hasError` ([props.md:72](./props.md)) raises the red 2 px border on the trigger and renders an error message in the hint zone — use it when the range is missing or invalid on submit. The in-panel `endTimeErrorMessage` ([props.md:68](./props.md)) is announced as a polite live region ([accessibility.md:43](./accessibility.md)) when the user enters an end time before the start time. Both should be localised.

```tsx
<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  hasError={isSubmitted && !range}
  endTimeErrorMessage={t('rangePicker.endBeforeStart', 'End time cannot be before start time')}
/>
```

#### ❌ Don't — Silently swap start and end behind the user's back

If the user enters a start later than the end, fix it visibly: show the error message via `endTimeErrorMessage` (which the live region announces) and block `Finish`. Auto-swapping mutates the user's intent without telling them and breaks the audit trail in analytics events.

```tsx
{/* Wrong — silently corrects user input */}
const normalised = startDate <= endDate
  ? { startDate, endDate }
  : { startDate: endDate, endDate: startDate };   // ← user wasn't told
```

**Source:** [props.md:68](./props.md) · [props.md:72](./props.md) · [accessibility.md:43](./accessibility.md) · [accessibility.md:69](./accessibility.md).

---

### Pair 7 — Use `isDisabled` for unavailability, not as an icon-hiding trick

#### ✅ Do — Use `isDisabled` only when the range genuinely cannot be edited

`isDisabled={true}` ([props.md:80](./props.md)) sets `--interactive/disabled01` bg, dims the filled text to `--interactive/disabled04`, **prevents focus**, and exposes `aria-disabled="true"` to assistive tech ([accessibility.md:72](./accessibility.md)). Use it when the surrounding form locks the field — e.g. while a request is in-flight, or when permissions prevent editing.

```tsx
<DateTimeRangeSelector
  dateTimeRange={savedRange}
  isDisabled={!canEditFilter}
  onRangeChange={onRangeChange}
/>
```

#### ❌ Don't — Reach for `isDisabled` because the calendar icon "looks off" in Hover/Focus

The calendar icon is **intentionally hidden** in every non-Rest state ([DateTimeRangeSelector-figma.md:88](./DateTimeRangeSelector-figma.md)) — that's the design, not a bug. Disabling the field to hide the icon removes the user's ability to focus or edit. If the field is read-only (informational, not editable), pair a `Label` with a formatted string instead.

```tsx
{/* Wrong — disabling to hide a visual element breaks keyboard access */}
<DateTimeRangeSelector
  dateTimeRange={range}
  isDisabled                                // ← removes the field from the tab order
/>
```

**Source:** [props.md:80](./props.md) · [DateTimeRangeSelector-figma.md:88](./DateTimeRangeSelector-figma.md) · [DateTimeRangeSelector-figma.md:163](./DateTimeRangeSelector-figma.md) · [accessibility.md:72](./accessibility.md).

---

### Pair 8 — Localise every visible string, not just the calendar

#### ✅ Do — Pass `locale` and localised label/button props together

`locale` ([props.md:81](./props.md)) only handles month / day names and date-fns parsing. The trigger label, placeholder, From/To, Start/End time labels, Finish/Clear button labels, end-before-start error, and the `Custom` predefined-range label are all **separate props with English defaults**. Pass them all in non-English surfaces.

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

Half-localised UIs are worse than fully-English ones: users see "lundi" but "From" / "To" / "Finish", which signals "this product wasn't built for me".

```tsx
{/* Wrong — locale set, labels not */}
<DateTimeRangeSelector
  dateTimeRange={range}
  onRangeChange={onRangeChange}
  locale={fr}
  /* fromLabel / toLabel / finishButtonLabel / … all still English defaults */
/>
```

**Source:** [props.md:63](./props.md) · [props.md:65](./props.md) · [props.md:68](./props.md) · [props.md:70](./props.md) · [props.md:71](./props.md) · [props.md:81](./props.md) · [props.md:86](./props.md) · [props.md:90](./props.md) · [props.md:94](./props.md) · [examples.md:120](./examples.md) · [accessibility.md:71](./accessibility.md).

---

## Edge cases & variants

| Case | Guidance | Source |
|------|----------|--------|
| **Data-retention window** (e.g. last 90 days of call records) | Pass `otherCalendarProps={{ minDate, disabledDateTooltip }}` so out-of-window dates are visually disabled **and** explained to screen-reader users. | [examples.md:151](./examples.md) · [Calendar-usage.md → Pair 3](../Calendar/Calendar-usage.md) |
| **Custom trigger** (icon button, summary chip) | Use `inputRenderer={({ value, onClick }) => …}`. The renderer must preserve keyboard semantics — clickable + focusable + announces its label. Validate against a running instance (WARN-001 in [DateTimeRangeSelector-audit.md](./DateTimeRangeSelector-audit.md)). | [examples.md:196](./examples.md) · [props.md:79](./props.md) |
| **Closing rules** | Default close triggers: `Escape`, click outside, `Finish`, `Clear`. Add `customCloseHandlers` only when an embedding popover (e.g. a SlideOut) needs to dismiss on its own events. | [props.md:64](./props.md) |
| **Forwarding Calendar props** | `otherCalendarProps` accepts any `CalendarProps` — useful for `disabledDates`, `minDate`, `maxDate`, `disabledDateTooltip`. | [props.md:85](./props.md) · [examples.md:160](./examples.md) |
| **Dark mode** | Variants exist in Figma ([DateTimeRangeSelector-figma.md:171](./DateTimeRangeSelector-figma.md)) but token bindings are not yet extracted (GAP-009). Treat Dark behaviour as identical to Light until tokens are confirmed. | [DateTimeRangeSelector-figma.md:171](./DateTimeRangeSelector-figma.md) |

---

## Accessibility highlights

- **Live region for end-before-start validation** — `endTimeErrorMessage` is announced via `aria-live="polite"` ([accessibility.md:43](./accessibility.md)). Localise it.
- **Disabled is announced, not just visual** — `aria-disabled="true"` keeps the trigger discoverable to screen readers while marking it non-interactive ([accessibility.md:72](./accessibility.md)). Don't replace with `display: none`.
- **Keyboard escape** — `Escape` closes the picker **without applying** ([accessibility.md:56](./accessibility.md)). Don't wire destructive side effects to `onClose`; they will fire on cancel.
- **Locale must be supplied for non-English surfaces** — month/day names are pulled from the date-fns locale object ([accessibility.md:71](./accessibility.md)).
- **WCAG verification gaps** — `1.4.1 Use of Color`, `1.4.3 Contrast (minimum)`, `2.4.7 Focus Visible` are listed as **Verify** in [accessibility.md:81](./accessibility.md) until token values are confirmed (GAP-002 / GAP-007).

See [accessibility.md](./accessibility.md) for the full ARIA / keyboard / WCAG checklist.

---

## See also

- [props.md](./props.md) — complete API reference (32 props on the selector + 21 on `DateTimeRangePicker`).
- [examples.md](./examples.md) — code patterns including controlled range, French locale, 90-day window, custom input renderer.
- [tokens.md](./tokens.md) — design tokens (visual states still partially unverified — see GAP-002).
- [accessibility.md](./accessibility.md) — ARIA, keyboard, WCAG 2.1 AA.
- [DateTimeRangeSelector-figma.md](./DateTimeRangeSelector-figma.md) — full anatomy, variant axes, colour bindings for the trigger.
- [Calendar — Usage Guidelines](../Calendar/Calendar-usage.md) — open picker panel (calendar grid, predefined ranges, time row).
- [DateTimeRangeSelector-audit.md](./DateTimeRangeSelector-audit.md) — current gaps blocking a fully-verified rewrite.

---

## Appendix — Original `figma-extract-usage` gap note (2026-05-08)

Preserved for traceability. Once a `↳ Date picker examples` page is added to Figma file `5YihJ5WuDvnvrlrRMC4sBp` with `✅ Do —` / `❌ Don't —` card frames, re-run `figma-extract-usage` and replace this file with its canonical output.

> No `↳ Date picker examples` or `↳ DateTimeRangeSelector examples` page exists in the UI-components Figma file (`5YihJ5WuDvnvrlrRMC4sBp`). The `figma-extract-usage` skill found no matching examples page. No Do/Don't editorial guidance had been published for this component at the time of audit.
>
> The shared "Date picker" Figma component (node `80239:8235`) has no associated `↳` examples page. The Calendar examples page (`↳ Calendar examples`, node `69971:10137`) documents usage patterns for the open calendar panel, but not for the DateTimeRangeSelector trigger or predefined-ranges interaction patterns.
>
> | Type | Description |
> |------|-------------|
> | Missing usage page | No `↳ Date picker examples` or `↳ DateTimeRangeSelector examples` page found in Figma. Designer must create one using the `figma-draw` template before usage guidelines can be extracted. |
> | Missing Do/Don't cards | No `✅ Do —` or `❌ Don't —` frames available |
>
> _Source: Figma file page listing · Extracted 2026-05-08_

---

_Source: editorial draft via `usage-advisor` skill (open mode) + Calendar-usage.md structural template · Grounded in props.md, examples.md, tokens.md, accessibility.md, DateTimeRangeSelector-figma.md (extracted 2026-05-08) and Oxygen MCP component README · Drafted 2026-05-12_
