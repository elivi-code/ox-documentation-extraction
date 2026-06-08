---
parent: "[[DateTimeSelector]]"
section: usage
---

<!-- STUB:GAP-003 source="Re-run figma-extract-usage and replace source/DateTimeSelector-usage.md once '↳ Date picker examples' Do/Don't cards are added to Figma file 5YihJ5WuDvnvrlrRMC4sBp. Current content is editorial (usage-advisor, 2026-05-13)." -->

<!-- source: editorial — no Figma Do/Don't page exists. Drafted from props.md, examples.md, accessibility.md, DateTimeSelector-figma.md. Replace with figma-extract-usage output when Figma cards exist. -->

A `DateTimeSelector` lets users **pick a single date (and optionally a time)** from a 320 px trigger input that opens a popover with an embedded Calendar grid. It is the standard single-date control for forms, scheduling flows, and any surface where a user commits to one moment in time.

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

For a span (start + end), reach for `DateTimeRangeSelector` — same trigger, range semantics, predefined-ranges panel, two-click + Finish commit. For an always-visible grid, use `Calendar` directly.

```tsx
{/* Wrong — two DateTimeSelectors do not equal a range */}
<DateTimeSelector value={start} onDateChange={setStart} />
<DateTimeSelector value={end}   onDateChange={setEnd} />
```

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

For scheduled meetings, billing dates, or deadlines, leave `closeOnDateChange` off and keep the explicit `finishButtonLabel` step. The Finish button is the user's last reversible moment before the commit.

```tsx
{/* Wrong on a high-stakes flow */}
<DateTimeSelector
  value={meetingStart}
  onDateChange={(d) => { setMeetingStart(d); scheduleMeeting(d); }}
  closeOnDateChange
/>
```

---

### Pair 3 — Loading state: `isLoading` is for async availability, not generic form saving

#### ✅ Do — Pair `isLoading` with a descriptive `loadingMessage` when the picker depends on data still being fetched

```tsx
<DateTimeSelector
  value={slot}
  onDateChange={setSlot}
  isLoading={availability.status === 'loading'}
  loadingMessage="Checking available slots…"
/>
```

#### ❌ Don't — Use `isLoading` to indicate "the surrounding form is submitting"

Form-level saving belongs on the submit button. A bare `isLoading` with no `loadingMessage` is also an accessibility regression — the picker announces "busy" with no context.

```tsx
{/* Wrong — picker isn't what's busy */}
<DateTimeSelector
  value={date}
  onDateChange={setDate}
  isLoading={form.isSubmitting}
/>
```

---

### Pair 4 — Display format: pick a pattern that fits the surface and locale, never raw ISO

#### ✅ Do — Set `titleFormatPattern` to match the surrounding copy

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

A raw `Date.toString()` in the trigger is what screen readers announce if `titleFormatPattern` is omitted.

```tsx
{/* Wrong — locale set without a localised pattern */}
<DateTimeSelector
  value={date}
  onDateChange={setDate}
  locale={fr}
/>
```

---

### Pair 5 — `isClearable`: expose Clear for optional filters, hide it for required fields

#### ✅ Do — Set `isClearable` when the field is an optional filter

```tsx
<DateTimeSelector
  value={filterDate}
  onDateChange={setFilterDate}
  isClearable
/>
```

#### ❌ Don't — Expose Clear on a required field

For a required field, Clear produces an invalid form state with no obvious next step.

```tsx
{/* Wrong — Clear lets users empty a required field */}
<DateTimeSelector
  value={meetingStart}
  onDateChange={setMeetingStart}
  isClearable
/>
```

---

### Pair 6 — `isDisabled` is for genuine unavailability, not to hide the calendar icon

#### ✅ Do — Use Disabled only when the field genuinely cannot be edited

```tsx
<DateTimeSelector
  value={savedDate}
  onDateChange={setSavedDate}
  isDisabled={!canEdit}
/>
```

#### ❌ Don't — Reach for Disabled because the calendar icon "looks off" in Hover/Focus/Error

The calendar icon is **intentionally hidden** in every non-Rest state — that's the design, not a bug. Disabling the field removes the trigger from the tab order and strips keyboard access.

```tsx
{/* Wrong — disabling to hide a visual element kills keyboard access */}
<DateTimeSelector
  value={date}
  isDisabled
/>
```

---

## Cross-linked axes

Two axes apply equally to `DateTimeSelector` but are documented in depth on the sibling page:

- **Don't pre-fill to look populated** — leave `value={undefined}` until the user picks. See [[DateTimeRangeSelector.usage]].
- **Localise every visible string** — `finishButtonLabel`, `loadingMessage`, `titleFormatPattern`, and the Clear `aria-label` are all separate from the `locale` object. See [[DateTimeRangeSelector.usage]].
