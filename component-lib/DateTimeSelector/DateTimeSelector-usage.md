---
component: DateTimeSelector
package: "@8x8/oxygen-date-time-selector"
category: date_time
role: usage
role_description: "Usage guidelines — editorial, drafted from extracted MCP/Figma artifacts via the usage-advisor skill"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from extracted artifacts (props.md, examples.md, accessibility.md, DateTimeSelector-figma.md) — NOT from Figma Do/Don't card frames. No `↳ Date picker examples` page exists in Figma file 5YihJ5WuDvnvrlrRMC4sBp. If/when one is added, replace this file with figma-extract-usage output."
source_type: editorial
audit_verdict: "YES"
siblings:
  - "[[DateTimeSelector/props]]"
  - "[[DateTimeSelector/examples]]"
  - "[[DateTimeSelector/tokens]]"
  - "[[DateTimeSelector/accessibility]]"
  - "[[DateTimeSelector/DateTimeSelector-figma]]"
  - "[[DateTimeSelector/DateTimeSelector-audit]]"
  - "[[DateTimeRangeSelector/DateTimeRangeSelector-usage]]"
tags:
  - oxygen
  - component/DateTimeSelector
  - role/usage
  - stage/editorial
  - category/date_time
---
<!-- SKILL: usage-advisor (open mode) -->
<!-- COMPONENT: DateTimeSelector -->
<!-- DRAFTED: 2026-05-13 -->
<!-- GROUNDING: full — props.md, examples.md, tokens.md, accessibility.md, DateTimeSelector-figma.md, DateTimeSelector-audit.md present; pui.md intentionally absent -->
<!-- PAIRS: 6 -->
<!-- STATUS: editorial — replace with figma-extract-usage output once `↳ Date picker examples` cards exist in Figma file 5YihJ5WuDvnvrlrRMC4sBp -->
<!-- SIBLING PRECEDENT: DateTimeRangeSelector-usage.md (2026-05-12 editorial draft); shares the same Figma trigger node 80239:8235 -->

# DateTimeSelector — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md) · [DateTimeSelector-figma.md](./DateTimeSelector-figma.md) · [DateTimeRangeSelector — Usage Guidelines](../DateTimeRangeSelector/DateTimeRangeSelector-usage.md) (range sibling — shares trigger).

> **Editorial guidance — no Figma Do/Don't cards.** No `↳ Date picker examples` page exists in the UI-components Figma file (`5YihJ5WuDvnvrlrRMC4sBp`). The pairs below are drafted from the extracted artifacts and cross-referenced with the sibling [DateTimeRangeSelector — Usage Guidelines](../DateTimeRangeSelector/DateTimeRangeSelector-usage.md), which documents the shared trigger. Replace this file with `figma-extract-usage` output once Do/Don't cards exist in Figma.

A `DateTimeSelector` lets users **pick a single date (and optionally a time)** from a 320 px trigger input that opens a popover with an embedded Calendar grid. It is the standard single-date control for forms, scheduling flows, and any surface where a user commits to one moment in time.

---

## Do / Don't

### Pair 1 — Pick the right picker for the selection type

#### ✅ Do — Use `DateTimeSelector` for a single date/time decision

A single `value: Date` + `onDateChange(date: Date)` is the canonical case. The component is right-sized when the user makes one decision — a meeting time, a deadline, an "active from" date.

```tsx
<DateTimeSelector
  value={date}
  onDateChange={setDate}
/>
```

#### ❌ Don't — Use it for a range, or as a replacement for an inline calendar

For a span (start + end, with or without times), reach for `DateTimeRangeSelector` — same trigger, range semantics, predefined-ranges panel, two-click + Finish commit. For an always-visible grid (e.g. an availability planner where the popover would just be in the way), use `Calendar` directly.

```tsx
{/* Wrong — two DateTimeSelectors do not equal a range */}
<DateTimeSelector value={start} onDateChange={setStart} />
<DateTimeSelector value={end}   onDateChange={setEnd} />
```

**Source:** [props.md:53–62](./props.md) · [DateTimeSelector-figma.md:233](./DateTimeSelector-figma.md) (shared trigger) · [DateTimeRangeSelector-usage.md → Pair 1](../DateTimeRangeSelector/DateTimeRangeSelector-usage.md).

---

### Pair 2 — Commit pattern: `closeOnDateChange` for low-stakes, explicit Finish for high-stakes

#### ✅ Do — Use `closeOnDateChange` for inline filters and casual one-tap picks

When the cost of an accidental pick is low (a list filter that re-runs instantly, a draft-state input the user can change again), `closeOnDateChange` removes a step and feels lighter.

```tsx
<DateTimeSelector
  value={filterDate}
  onDateChange={setFilterDate}
  closeOnDateChange
/>
```

#### ❌ Don't — Auto-close when the selection commits a real side effect

For scheduled meetings, billing dates, deadlines, or anything that triggers an external write at commit time, leave `closeOnDateChange` off and keep the explicit `finishButtonLabel` step. The Finish button is the user's last reversible moment before the commit; collapsing it makes accidental picks irrecoverable from the keyboard.

```tsx
{/* Wrong on a high-stakes flow — meeting is scheduled the moment the user taps a day */}
<DateTimeSelector
  value={meetingStart}
  onDateChange={(d) => { setMeetingStart(d); scheduleMeeting(d); }}
  closeOnDateChange
/>
```

**Source:** [props.md:53](./props.md) · [props.md:54](./props.md) · [examples.md:67](./examples.md). *No sibling precedent — `DateTimeRangeSelector` always commits on Finish; this axis is unique to `DateTimeSelector`.*

---

### Pair 3 — Loading state: `isLoading` is for async availability, not generic form saving

#### ✅ Do — Pair `isLoading` with a descriptive `loadingMessage` when the picker depends on data still being fetched

The intent of the loading state is "the available times aren't determined yet" — checking a roster, fetching bookable slots, validating against a calendar service. Always pair `isLoading` with a `loadingMessage`; the message is exposed via `aria-busy="true"` and read by screen readers.

```tsx
<DateTimeSelector
  value={slot}
  onDateChange={setSlot}
  isLoading={availability.status === 'loading'}
  loadingMessage="Checking available slots…"
/>
```

#### ❌ Don't — Use `isLoading` to indicate "the surrounding form is submitting"

Form-level saving belongs on the submit button or a form-level loader. Putting it on the picker freezes the field, swallows keyboard input on the trigger, and confuses screen readers about what is busy. A bare `isLoading` with no `loadingMessage` is also an accessibility regression — the picker announces "busy" with no context.

```tsx
{/* Wrong — picker isn't what's busy */}
<DateTimeSelector
  value={date}
  onDateChange={setDate}
  isLoading={form.isSubmitting}
/>
```

**Source:** [props.md:56](./props.md) · [props.md:57](./props.md) · [props.md:71](./props.md) (always pair `isLoading` with `loadingMessage`) · [accessibility.md:38](./accessibility.md) · [accessibility.md:62](./accessibility.md). *Unique to this component — `DateTimeRangeSelector` has no `isLoading` prop.*

---

### Pair 4 — Display format: pick a pattern that fits the surface and locale, never raw ISO

#### ✅ Do — Set `titleFormatPattern` to match the surrounding copy, and pass `locale` together with it

The default format renders date-fns tokens; pick a pattern that matches the form's tone — `"EEE, d MMM yyyy"` for human-readable display, `"dd/MM/yyyy HH:mm"` for dense filter bars. On non-English surfaces, the format pattern and the `locale` object travel together: month and weekday names come from `locale`, the **shape** comes from the pattern.

```tsx
import { fr } from 'date-fns/locale';

<DateTimeSelector
  value={date}
  onDateChange={setDate}
  titleFormatPattern="EEE d MMM yyyy 'à' HH:mm"
  locale={fr}
/>
```

#### ❌ Don't — Render raw ISO, or set `locale` and leave the pattern in English

A raw `Date.toString()` in the trigger is what screen readers announce if `titleFormatPattern` is omitted — the trigger button must announce a human-readable string. Half-localised UIs (French weekday names inside an English-shaped format) read worse than fully-English ones.

```tsx
{/* Wrong — locale set without a localised pattern */}
<DateTimeSelector
  value={date}
  onDateChange={setDate}
  locale={fr}
  /* titleFormatPattern missing — falls back to a default English-shaped format */
/>
```

**Source:** [props.md:61](./props.md) · [props.md:68](./props.md) · [accessibility.md:61](./accessibility.md). *Partial sibling precedent:* [DateTimeRangeSelector-usage.md → Pair 8](../DateTimeRangeSelector/DateTimeRangeSelector-usage.md).

---

### Pair 5 — `isClearable`: expose Clear for optional filters, hide it for required fields

#### ✅ Do — Set `isClearable` when the field is an optional filter

When the consuming surface runs correctly with no date selected — a filter that defaults to "all time", an optional "available after" field — a Clear affordance lets the user reset without re-opening the picker. The clear button must carry an `aria-label` like `"Clear selected date"` so screen readers don't announce a bare icon.

```tsx
<DateTimeSelector
  value={filterDate}
  onDateChange={setFilterDate}
  isClearable
/>
```

#### ❌ Don't — Expose Clear on a required field

For a required field (scheduling a meeting, a billing start date), Clear produces an invalid form state with no obvious next step. Leave `isClearable` off and let the user overwrite the selection by re-opening the picker.

```tsx
{/* Wrong — Clear lets users empty a required field */}
<DateTimeSelector
  value={meetingStart}        // required for the meeting to be created
  onDateChange={setMeetingStart}
  isClearable
/>
```

**Source:** [props.md:55](./props.md) · [accessibility.md:63](./accessibility.md).

---

### Pair 6 — `isDisabled` is for genuine unavailability, not to hide the calendar icon

#### ✅ Do — Use Disabled only when the field genuinely cannot be edited

Disabled is the right tool when permissions, an in-flight save, or a parent-form lock prevent edits. The state is announced via `aria-disabled` so it stays discoverable to screen readers while marking the field non-interactive.

```tsx
<DateTimeSelector
  value={savedDate}
  onDateChange={setSavedDate}
  isDisabled={!canEdit}
/>
```

#### ❌ Don't — Reach for Disabled because the calendar icon "looks off" in Hover/Focus/Error

The calendar icon is **intentionally hidden** in every non-Rest state — that's the design, not a bug. Disabling the field to suppress the icon removes the trigger from the tab order and strips keyboard access. If the field is informational (read-only, not "unavailable"), pair a `Label` with a formatted string instead.

```tsx
{/* Wrong — disabling to hide a visual element kills keyboard access */}
<DateTimeSelector
  value={date}
  isDisabled                    // ← removes trigger from tab order
/>
```

**Source:** [DateTimeSelector-figma.md:74](./DateTimeSelector-figma.md) · [DateTimeSelector-figma.md:141–148](./DateTimeSelector-figma.md) · [accessibility.md:72](./accessibility.md) · [DateTimeRangeSelector-usage.md → Pair 7](../DateTimeRangeSelector/DateTimeRangeSelector-usage.md).

---

## Axes skipped (cross-linked to sibling)

Two axes apply equally to `DateTimeSelector` but are documented in depth on the sibling page — cross-link rather than repeat:

- **Don't pre-fill to look populated** — leave `value={undefined}` until the user picks. See [DateTimeRangeSelector-usage.md → Pair 5](../DateTimeRangeSelector/DateTimeRangeSelector-usage.md).
- **Localise every visible string** — `finishButtonLabel`, `loadingMessage`, `titleFormatPattern`, and the Clear `aria-label` are all separate from the `locale` object. See [DateTimeRangeSelector-usage.md → Pair 8](../DateTimeRangeSelector/DateTimeRangeSelector-usage.md).

---

_Source: editorial draft via `usage-advisor` skill (open mode) · Grounded in `props.md`, `examples.md`, `tokens.md`, `accessibility.md`, `DateTimeSelector-figma.md`, `DateTimeSelector-audit.md` (extracted 2026-05-08) · Sibling precedent: `DateTimeRangeSelector-usage.md` (2026-05-12) · Drafted 2026-05-13._
