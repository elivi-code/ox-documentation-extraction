---
parent: "[[TimeSelector]]"
section: usage
component: TimeSelector
pipeline_stage: draft
tags:
  - oxygen
  - component/TimeSelector
  - role/spoke
  - section/usage
  - category/date_time
---

> **Editorial guidance — mirrors the published Oxygen docs page.** No `↳ TimeSelector examples` Figma page with Do/Don't card frames was located, so `figma-extract-usage` was skipped. Pairs below were derived editorially from the published Oxygen docs page (`https://oxygen.8x8.com/components/timeselector/usage`, fetched 2026-05-15 via Claude_in_Chrome MCP), cross-validated against source files. Replace with `figma-extract-usage` output if a Figma examples page is ever created.

> ⚠️ **Two unresolved audit conflicts.** GAP-001 (Figma exposes `Size=Large` but the code `TimeSelectorSize` enum only accepts `"small" | "default"`) and GAP-002 (Figma default size is `Large`; code default is `"default"` ≡ Medium) are unresolved. Sized guidance in Pair 6 refers to the code API only.

> ⚠️ **Accessibility is inferred (GAP-008).** ARIA / focus-order / keyboard notes were reconstructed from time-picker conventions — the OX MCP returned no accessibility documentation, and Figma annotations contain no a11y notes. Treat the ARIA quick reference below as recommended-to-verify, not authoritative.

A TimeSelector lets a user **pick a time of day** — either by opening a dropdown and selecting a value, or by typing the time directly into the input. Use it in forms, scheduling flows, and report filters where the user needs to enter a specific hour and minute (and optionally an AM/PM marker or timezone).

---

## Anatomy

The component anatomy numbers three parts:

1. **Label** — the accessible name of the input. Optional (controlled by `Show Label`, default true). When required, the label pairs with a red asterisk in `--error/error01`. The label area can also host an optional info icon button that reveals a tooltip.
2. **Input** — the time input field itself. Always present. Holds the displayed time value or placeholder. In Focus state, a 1 px × 24 px cursor bar appears inside the input and a 2 px focus ring overlays the container. An optional left icon (`isLeftIconVisible` + `iconLeft`) may sit inside the input.
3. **Helper text** *(optional)* — hint text rendered below the input. Controlled by `Show Hint` (default true). In the error state this slot is replaced by an **Error Area** containing a 16 × 16 error icon and red error message text.

The full structure stacks vertically (label → input → hint/error), with 4 px gaps between rows and an 8 px gap between elements inside the input row.

---

## Overview

Two key surfaces are exported by `@8x8/oxygen-time-selector`:

| Symbol | Use for | Key props |
|--------|---------|-----------|
| `TimeSelector` | A single time-of-day input + dropdown | `value`, `onChange`, `onOpen`, `onClose`, `size`, `placeholder`, `timeDisplayFormat`, `hasError`, `isDisabled`, `isLeftIconVisible`, `iconLeft`, `id`, `testId`, `portalRef` |
| `TimeValue` *(type)* | Shape of the controlled value | `{ hours, minutes, seconds }` |

> **Verbatim from the docs page (Overview):** *"A time selector allows users to pick a time; it also allows users to enter a specific time value, using the keyboard, without selecting it from a dropdown. They can be used for a wide range of scenarios including forms, scheduling, and filtering reports."*

The component is a composite of a text input and a popover dropdown, with optional label + helper text wrappers from the Forms pattern.

---

## Behaviour

### Interaction *(verbatim from the docs page)*

- "The user must click on the input fields to open the time selector dropdown."
- "Selecting a time closes the dropdown and populates the time input field."
- "The time will default to a placeholder (e.g. `hh:mm` or `hh:mm AM`), if a time has been previously selected then that time will prepopulate the time input field."
- "The system will dictate what time format will be used."
- "The user can manually enter the date using a keyboard." *(docs page says "date" — read as "time"; the intent is keyboard entry of the time value into the input)*

The popover dropdown reaches the DOM at the component root unless `portalRef` is supplied — pass `portalRef` when the TimeSelector lives inside a scrollable container or a dialog with `overflow: hidden` so the dropdown can escape the clipping region.

### States

| # | State | Trigger | Visual change |
|---|-------|---------|---------------|
| 1 | Rest | Default | `--ui/ui05` (#F4F3EE) input background; no border |
| 2 | Focus | Keyboard `Tab` or click | `--interactive/focus01` (#0056E0) 2 px ring overlay + 1 px type-cursor bar |
| 3 | Disabled | `isDisabled={true}` | `--interactive/disabled01` (#C8C8BD) background, `--interactive/disabled04` (#8D8B7E) text; no interaction |
| 4 | Error (Rest) | `hasError={true}` | `--error/error01` (#CB2233) 2 px border + Error Area shown below |
| 5 | Error (Focus) | Focus while `hasError={true}` | Both focus ring and error border visible |
| 6 | Filled | A `TimeValue` is set | Time renders in `--text/textColor02` (#6C6862) inside the input |

### Keyboard *(inferred — GAP-008)*

| Key | Behaviour (inferred) |
|-----|----------------------|
| `Tab` | Move focus to / from the TimeSelector input |
| `Enter` / `Space` | Open the time picker dropdown |
| `Escape` | Close the dropdown, return focus to the input |
| `Arrow Up` / `Arrow Down` | Navigate through time options in the open dropdown |
| `Tab` (within dropdown) | Move between hour, minute, AM/PM columns |

Use this as design intent until verified — don't rely on the exact key mapping in code reviews.

---

## Time format *(verbatim from the docs page)*

- "Both the 12-hour and 24-hour time systems are allowed."
- "If using the 12-hour format it must be accompanied by an AM/PM to follow."
- "Specific times should specify a timezone."

The component exposes a `timeDisplayFormat: string` prop to control display, but the accepted format-string syntax (moment, date-fns, custom?) is undocumented — see **GAP-004** in [[TimeSelector]] audit. Until that's resolved, treat `timeDisplayFormat` as an opaque pass-through and verify the rendered output for any format you choose.

---

## Sizes & spacing

| Code `size` | Figma size | Input height | Input width | Padding | Input typography |
|-------------|------------|-------------|-------------|---------|------------------|
| `"small"` | Small | 32 px | 80 px | 8 px all | `$label01` 12 px / lh 16 px |
| `"default"` *(default)* | Medium | 40 px | 97 px | 12 px H / 8 px V | `$body01` 14 px / lh 20 px |
| *(not in API)* | Large | 48 px | 120 px | 16 px H / 12 px V | `$body02` 16 px / lh 24 px |

> ⚠️ **Size conflict.** Figma exposes `Size=Large` as the **Figma default** (GAP-001 / GAP-002). The code `TimeSelectorSize` enum only accepts `"small" | "default"`, and `"default"` corresponds to Figma `Medium`. `<TimeSelector />` rendered without a `size` prop is therefore **Medium** in code but **Large** in Figma. Treat Large as design-only until the API conflict is resolved.

Internal spacing is hardcoded: 4 px between label / input / hint rows, 8 px between elements inside the input row, 4 px between the error icon and error text. The input border radius is **6 px**, hardcoded (no token binding).

---

## Best Practices

### When to use *(verbatim from the docs page)*

- "When asking the user for an exact or approximate time."
- "When the user is required to schedule tasks (E.g. reports)."

Reach for TimeSelector when the user must enter a **specific time of day** (not a date, not a duration) and a free-text input would be ambiguous.

### When not to use

| Situation | Why | Use instead |
|-----------|-----|-------------|
| Time is **not strictly required** | *(verbatim)* Asking for time inflates the form and slows completion. | Drop the field; default to a sensible system value. |
| The user needs to pick a **date** | TimeSelector handles hours / minutes only — no date axis in `TimeValue`. | `Calendar` |
| The user needs a **date + time** together | A single TimeSelector can't capture both; pairing two inputs tends to drift without explicit wiring. | Compose `Calendar` with `TimeSelector`, or use a date-time picker pattern (Forms). |
| The user needs to enter a **duration** | TimeSelector enforces wall-clock semantics (hours 0–23, minutes 0–59), not arbitrary durations. | A `TextField` with explicit duration parsing, or two numeric inputs. |
| The choice is between a small fixed set (e.g. "9 AM", "12 PM", "5 PM") | A full picker is overkill; a few buttons or radios scan faster. | `Radio` / `RadioGroup`, or a `Select` with the discrete options. |

---

## Do / Don't

> These pairs are derived editorially from the docs page's Behaviour + Time format + Best Practices sections, combined with the extracted API, token, and (inferred) a11y data. No Figma ✅ Do / ❌ Don't card frames exist for TimeSelector at the time of writing. Treat as provisional until a designer reviews them or a Figma examples page is created.

### Pair 1 — Reach for TimeSelector when the input is a time of day

#### ✅ Do — Use TimeSelector for hour-and-minute entry

```tsx
import { TimeSelector } from "@8x8/oxygen-time-selector";
import { useState } from "react";

const [start, setStart] = useState({ hours: 9, minutes: 0, seconds: 0 });

<TimeSelector
  value={start}
  onChange={setStart}
  testId="report-start-time"
/>
```

#### ❌ Don't — Use TimeSelector for dates, date+time, or durations

```tsx
{/* Wrong — there's no "date" to capture; use Calendar */}
<TimeSelector
  value={{ hours: 0, minutes: 0, seconds: 0 }}
  onChange={(v) => setDueDate(v as any)} // ❌ TimeValue ≠ Date
/>

{/* Wrong — durations aren't wall-clock times; the dropdown caps at 23:59 */}
<TimeSelector
  value={{ hours: 90 /* meant: 90 minutes */, minutes: 0, seconds: 0 }}
  onChange={setDuration}
/>
```

---

### Pair 2 — Control `value` with `onChange`; pre-populate when a sensible default exists

#### ✅ Do — Wire `value` + `onChange` as a controlled pair, and seed the value when you know it

```tsx
const now = new Date();
const [time, setTime] = useState({
  hours: now.getHours(),
  minutes: now.getMinutes(),
  seconds: 0,
});

<TimeSelector
  value={time}
  onChange={setTime}
  placeholder="hh:mm AM"
/>
```

#### ❌ Don't — Render `<TimeSelector />` with no `value` and no `onChange`

```tsx
{/* Wrong — uncontrolled; the parent has no way to read what the user picked */}
<TimeSelector placeholder="hh:mm AM" />
```

---

### Pair 3 — Combine 12-hour format with AM/PM, and specify a timezone when the time matters

#### ✅ Do — Pair 12-hour displays with AM/PM, and surface the timezone when the value is timezone-sensitive

```tsx
<>
  <label htmlFor="meeting-start-time">Meeting start (America/Los_Angeles)</label>
  <TimeSelector
    id="meeting-start-time"
    value={time}
    onChange={setTime}
    placeholder="hh:mm AM"
  />
</>
```

#### ❌ Don't — Show an unmarked 12-hour value, or hide the timezone for a timezone-sensitive moment

```tsx
{/* Wrong — 12-hour display with no AM/PM in placeholder or value */}
<TimeSelector
  value={{ hours: 5, minutes: 0, seconds: 0 }}
  onChange={setTime}
  placeholder="hh:mm"
  timeDisplayFormat="hh:mm"
/>
```

> ⚠️ **GAP-004:** `timeDisplayFormat` has no documented format-string syntax in the OX MCP. Verify your format string against the live Storybook before relying on it.

---

### Pair 4 — Use `hasError` together with an explicit error message + accessible wiring

#### ✅ Do — Set `hasError` and provide an error message that's announced to assistive tech

```tsx
<>
  <TimeSelector
    id="cutoff-time"
    value={cutoff}
    onChange={setCutoff}
    hasError={Boolean(error)}
    aria-invalid={Boolean(error) || undefined}
    aria-describedby={error ? "cutoff-time-error" : undefined}
  />
  {error && (
    <p id="cutoff-time-error" role="alert">
      Cutoff must be after the start time.
    </p>
  )}
</>
```

#### ❌ Don't — Style the input red without an accessible error message

```tsx
{/* Wrong — error styling with no message and no aria wiring */}
<TimeSelector
  value={cutoff}
  onChange={setCutoff}
  hasError
/>
```

> ⚠️ **GAP-008:** The exact ARIA wiring above is inferred from time-picker conventions — verify against the rendered DOM before shipping.

---

### Pair 5 — Use `isDisabled` for "this input is intentionally locked"; don't hide an empty input behind disabled

#### ✅ Do — Disable when the field is meaningfully unavailable

```tsx
<TimeSelector
  isDisabled
  value={{ hours: 10, minutes: 30, seconds: 0 }}
  onChange={setTime}
/>
```

#### ❌ Don't — Disable an empty field as a placeholder for "fill this in later"

```tsx
{/* Wrong — disabled empty field; the user can't tell what's expected here */}
<TimeSelector
  isDisabled
  value={undefined as any}
  onChange={setTime}
/>
```

> **WARN-001:** Disabled state combines `--interactive/disabled04` (#8D8B7E) text on `--interactive/disabled01` (#C8C8BD) background — contrast ratio may fall below 4.5:1. Verify before shipping unless a decorative exemption applies.

---

### Pair 6 — Match `size` to context — reserve Large until the API conflict resolves

#### ✅ Do — Use `"default"` for forms and `"small"` for dense surfaces

```tsx
{/* Form context */}
<TimeSelector value={time} onChange={setTime} />

{/* Dense filter / toolbar */}
<TimeSelector size="small" value={time} onChange={setTime} />
```

#### ❌ Don't — Author code against `size="large"` or assume Large is the default

```tsx
{/* Wrong — "large" is not a value in TimeSelectorSize */}
<TimeSelector size={"large" as any} value={time} onChange={setTime} />
```

**Source:** GAP-001 / GAP-002 — `TimeSelectorSize` enum · Figma Size axis.

---

## Accessibility quick reference

*(All bullets below are inferred — GAP-008 — verify against the rendered DOM before shipping.)*

- The input should be a `role="combobox"` (or a native `<input type="text">` with `aria-haspopup` pointing to the dropdown).
- `aria-expanded` should reflect whether the dropdown is open.
- Pair the visible **Label** with the input via `for` / `id` or `aria-labelledby`.
- Pair the **hint text** with the input via `aria-describedby`.
- When `hasError={true}`, set `aria-invalid="true"` and link the error message via `aria-describedby`.
- The focus ring uses `--interactive/focus01` (#0056E0) at 2 px — required by WCAG 2.4.7. Never suppress with `outline: none`.
- When the dropdown closes, focus must return to the trigger input.
- `isDisabled={true}` should set `disabled` (or `aria-disabled="true"`) and remove the input from the focus order.
- Required-field asterisk must be announced together with the label — don't hide it from assistive tech.

See [[TimeSelector.accessibility]] for the full WCAG 2.1 AA checklist.

---

## Related components

| Component | Relationship |
|-----------|-------------|
| [[Calendar]] | For date entry (year / month / day) — TimeSelector handles time only |
| [[Forms]] | TimeSelector is most often used inside the broader Forms pattern |
| [[TextField]] | For free-form duration entry where wall-clock semantics don't apply |
| [[Radio]] / [[Select]] | When the time choice is a small, discrete set |

---

## Gaps & open questions

| Item | Type | Description |
|------|------|-------------|
| Figma Do/Don't examples | SOURCE_GAP | No `↳ TimeSelector examples` Figma page with Do/Don't card frames was located. Re-run `figma-extract-usage` if such a page is created. |
| `Size=Large` API alignment | CONFLICT | GAP-001 / GAP-002: Figma exposes `Size=Large` as the Figma default; code API only accepts `"small"`/`"default"`. |
| `timeDisplayFormat` syntax | SOURCE_GAP | GAP-004: accepted format-string syntax undocumented. |
| Callbacks `onChange` / `onOpen` / `onClose` | SOURCE_GAP | GAP-003: callbacks inferred from Storybook stories — not in published OX MCP props list. |
| Accessibility inference | SOURCE_GAP | GAP-008: all ARIA / keyboard / focus guidance is inferred from time-picker conventions. |
| Disabled-state contrast | WARN-001 | Ratio may fall below 4.5:1 — verify or apply decorative exemption. |
| `ClockIcon` import path | WARN-002 | `@8x8/oxygen-icons` package name unverified. Confirm before publishing the icon example. |
