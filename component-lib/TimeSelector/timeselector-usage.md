---
component: TimeSelector
package: "@8x8/oxygen-time-selector"
category: date_time
role: usage
role_description: "Usage guidelines — editorial, compiled from the published Oxygen docs page and the extracted MCP artifacts"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from https://oxygen.8x8.com/components/timeselector/usage (fetched 2026-05-15 via Claude_in_Chrome MCP) cross-referenced with extracted MCP artifacts (props.md, examples.md, tokens.md, accessibility.md, timeselector-figma.md). No Figma '↳ TimeSelector examples' page is available — figma-extract-usage skipped. Re-run /doc-audit TimeSelector after creation; replace pairs with figma-extract-usage output if Figma Do/Don't cards are ever added."
source_type: editorial
audit_verdict: null
siblings:
  - "[[TimeSelector/props]]"
  - "[[TimeSelector/examples]]"
  - "[[TimeSelector/tokens]]"
  - "[[TimeSelector/accessibility]]"
  - "[[TimeSelector/timeselector-figma]]"
tags:
  - oxygen
  - component/TimeSelector
  - role/usage
  - stage/editorial
  - category/date_time
---
<!-- SOURCE: editorial — published Oxygen docs page (https://oxygen.8x8.com/components/timeselector/usage, fetched 2026-05-15 via Claude_in_Chrome MCP) + extracted MCP artifacts -->
<!-- FIGMA EXAMPLES PAGE: absent / not run — figma-extract-usage skipped per user direction -->
<!-- GROUNDING: partial — props.md, examples.md, tokens.md, accessibility.md, timeselector-figma.md, published docs page. Audit (timeselector-audit.md) flags GAP-001/002 (Size=Large), GAP-004 (timeDisplayFormat syntax), GAP-008 (a11y inferred) as open caveats. -->
<!-- DRAFTED: 2026-05-15 -->
<!-- MODE: docs-mirrored -->
<!-- PAIRS: 6 (derived from docs page Behaviour + Time format + Best Practices sections cross-validated against extracted artifacts) -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma "↳ TimeSelector examples" page is created with Do/Don't card frames -->

# TimeSelector — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md) · [timeselector-figma.md](./timeselector-figma.md)

> **Editorial guidance — mirrors the published Oxygen docs page.** No `↳ TimeSelector examples` Figma page with Do/Don't card frames was located, so `figma-extract-usage` was skipped. The body below transcribes the published Oxygen docs page for TimeSelector (`https://oxygen.8x8.com/components/timeselector/usage`, fetched 2026-05-15 via Claude_in_Chrome MCP) verbatim where the page asserts something, and derives Do/Don't pairs from the page's Behaviour + Time format + Best Practices content cross-validated against [props.md](./props.md), [examples.md](./examples.md), [tokens.md](./tokens.md), [accessibility.md](./accessibility.md), and [timeselector-figma.md](./timeselector-figma.md). Replace with `figma-extract-usage` output if a Figma examples page is ever created with Do/Don't cards.

> ⚠️ **Two unresolved audit conflicts.** [timeselector-audit.md](./timeselector-audit.md) flags **GAP-001** (Figma exposes `Size=Large` but the code `TimeSelectorSize` enum only accepts `"small" | "default"`) and **GAP-002** (Figma default size is `Large`; code default is `"default"` ≡ Medium). These remain unresolved at the time of writing and constrain the size guidance in [Pair 6](#pair-6--match-size-to-context--reserve-large-until-the-api-conflict-resolves). Sized guidance refers to the code API only.

> ⚠️ **Accessibility is inferred (GAP-008).** [accessibility.md](./accessibility.md) was reconstructed from time-picker conventions — the OX MCP returned no accessibility documentation, and Figma annotations contain no ARIA / focus-order / keyboard notes ([timeselector-figma.md:236](./timeselector-figma.md)). Treat the ARIA quick reference below as recommended-to-verify, not authoritative.

A TimeSelector lets a user **pick a time of day** — either by opening a dropdown and selecting a value, or by typing the time directly into the input ([source: docs page Overview](https://oxygen.8x8.com/components/timeselector/usage)). Use it in forms, scheduling flows, and report filters where the user needs to enter a specific hour and minute (and optionally an AM/PM marker or timezone).

---

## Anatomy

The published docs page numbers three parts on the anatomy illustration ([oxygen.8x8.com/components/timeselector/usage](https://oxygen.8x8.com/components/timeselector/usage)):

1. **Label** — the accessible name of the input. Optional in the Figma component (controlled by `Show Label` — `Show Label#19887:0`, default `true`, [timeselector-figma.md:91](./timeselector-figma.md)). When required, the label pairs with a red asterisk in `--error/error01` ([tokens.md:54](./tokens.md), [timeselector-figma.md:52](./timeselector-figma.md)). The label area can also host an optional info icon button that reveals a tooltip ([timeselector-figma.md:53](./timeselector-figma.md)).
2. **Input** — the time input field itself. Always present ([timeselector-figma.md:54](./timeselector-figma.md)). Holds the displayed time value or placeholder. In Focus state, a 1 px × 24 px cursor bar appears inside the input and a 2 px focus ring overlays the container ([timeselector-figma.md:57](./timeselector-figma.md), [tokens.md:65](./tokens.md)). An optional left icon (`isLeftIconVisible` + `iconLeft`, [props.md:74](./props.md)) may sit inside the input.
3. **Helper text** *(optional)* — hint text rendered below the input. Controlled by the `Show Hint` Figma boolean (`Show Hint#19869:10`, default `true`, [timeselector-figma.md:92](./timeselector-figma.md)). In the error state this slot is replaced by an **Error Area** containing a 16 × 16 error icon and red error message text ([timeselector-figma.md:60](./timeselector-figma.md), [tokens.md:54](./tokens.md)).

The full structure stacks vertically (label → input → hint/error), with `4 px` gaps between rows and an `8 px` gap between elements inside the input row ([timeselector-figma.md:197](./timeselector-figma.md)).

---

## Overview

Two key surfaces are exported by `@8x8/oxygen-time-selector` ([props.md:38](./props.md)):

| Symbol | Use for | Key props |
|--------|---------|-----------|
| `TimeSelector` | A single time-of-day input + dropdown | `value`, `onChange`, `onOpen`, `onClose`, `size`, `placeholder`, `timeDisplayFormat`, `hasError`, `isDisabled`, `isLeftIconVisible`, `iconLeft`, `id`, `testId`, `portalRef` |
| `TimeValue` *(type)* | Shape of the controlled value | `{ hours, minutes, seconds }` ([props.md:94](./props.md)) |

> **Verbatim from the docs page (Overview):** *"A time selector allows users to pick a time; it also allows users to enter a specific time value, using the keyboard, without selecting it from a dropdown. They can be used for a wide range of scenarios including forms, scheduling, and filtering reports."*

The component is a composite of a text input and a popover dropdown, with optional label + helper text wrappers from the Forms pattern.

---

## Behaviour

### Interaction *(verbatim from the docs page)*

- "The user must click on the input fields to open the time selector dropdown."
- "Selecting a time closes the dropdown and populates the time input field."
- "The time will default to a placeholder (e.g. `hh:mm` or `hh:mm AM`), if a time has been previously selected then that time will prepopulate the time input field."
- "The system will dictate what time format will be used."
- "The user can manually enter the date using a keyboard." *(the docs page says "date" here — read as "time"; the intent is keyboard entry of the time value into the input)*

The popover dropdown reaches the DOM at the component root unless `portalRef` is supplied — pass `portalRef` when the TimeSelector lives inside a scrollable container or a dialog with `overflow: hidden` so the dropdown can escape the clipping region ([examples.md:114](./examples.md), [props.md:78](./props.md)).

### States *(from `tokens.md` + `timeselector-figma.md`)*

| # | State | Trigger | Visual change |
|---|-------|---------|---------------|
| 1 | Rest | Default | `--ui/ui05` (#F4F3EE) input background; no border ([tokens.md:65](./tokens.md)) |
| 2 | Focus | Keyboard `Tab` or click | `--interactive/focus01` (#0056E0) 2 px ring overlay + 1 px type-cursor bar ([tokens.md:65](./tokens.md), [timeselector-figma.md:215](./timeselector-figma.md)) |
| 3 | Disabled | `isDisabled={true}` | `--interactive/disabled01` (#C8C8BD) background, `--interactive/disabled04` (#8D8B7E) text; no interaction ([tokens.md:65](./tokens.md), [props.md:73](./props.md)) |
| 4 | Error (Rest) | `hasError={true}` | `--error/error01` (#CB2233) 2 px border + Error Area shown below ([tokens.md:65](./tokens.md), [props.md:72](./props.md)) |
| 5 | Error (Focus) | Focus while `hasError={true}` | Both focus ring and error border visible ([timeselector-figma.md:218](./timeselector-figma.md)) |
| 6 | Filled | A `TimeValue` is set | Time renders in `--text/textColor02` (#6C6862) inside the input ([tokens.md:53](./tokens.md), [timeselector-figma.md:148](./timeselector-figma.md)) |

### Keyboard *(inferred — GAP-008)*

[accessibility.md:46](./accessibility.md) records the expected keyboard map based on time-picker conventions. It is **not yet verified** against the rendered DOM:

| Key | Behaviour (inferred) |
|-----|----------------------|
| `Tab` | Move focus to / from the TimeSelector input |
| `Enter` / `Space` | Open the time picker dropdown |
| `Escape` | Close the dropdown, return focus to the input |
| `Arrow Up` / `Arrow Down` | Navigate through time options in the open dropdown |
| `Tab` (within dropdown) | Move between hour, minute, AM/PM columns |

Use this as a design intent until verified — don't rely on the exact key mapping in code reviews.

---

## Time format *(verbatim from the docs page)*

- "Both the 12-hour and 24-hour time systems are allowed."
- "If using the 12-hour format it must be accompanied by an AM/PM to follow."
- "Specific times should specify a timezone."

The component exposes a `timeDisplayFormat: string` prop to control display ([props.md:70](./props.md)), but the accepted format-string syntax (moment, date-fns, custom?) is undocumented — see **GAP-004** in [timeselector-audit.md](./timeselector-audit.md). Until that's resolved, treat `timeDisplayFormat` as an opaque pass-through and verify the rendered output for any format you choose.

---

## Sizes & spacing

| Code `size` | Figma size | Input height | Input width | Padding | Input typography |
|-------------|------------|-------------|-------------|---------|------------------|
| `"small"` | Small | 32 px | 80 px | 8 px all | `$label01` 12 px / lh 16 px ([tokens.md:107](./tokens.md)) |
| `"default"` *(default)* | Medium | 40 px | 97 px | 12 px H / 8 px V | `$body01` 14 px / lh 20 px ([tokens.md:108](./tokens.md)) |
| _(not in API)_ | Large | 48 px | 120 px | 16 px H / 12 px V | `$body02` 16 px / lh 24 px ([tokens.md:109](./tokens.md)) |

> ⚠️ **Size conflict.** The Figma component set exposes `Size=Large` and uses it as the **Figma default** ([timeselector-figma.md:80](./timeselector-figma.md), GAP-001 / GAP-002). The code `TimeSelectorSize` enum only accepts `"small" | "default"`, and `"default"` corresponds to Figma `Medium` ([props.md:85](./props.md)). The default for `<TimeSelector />` rendered without a `size` prop is therefore **Medium**, which diverges from the Figma default of **Large**. Treat Large as design-only until the API conflict is resolved.

Internal spacing within the component is hardcoded ([timeselector-figma.md:194](./timeselector-figma.md)): `4 px` between label / input / hint rows, `8 px` between elements inside the input row, `4 px` between the error icon and error text. The input border radius is **6 px**, hardcoded (no token binding, [timeselector-figma.md:119](./timeselector-figma.md)).

---

## Best Practices

### When to use *(verbatim from the docs page)*

- "When asking the user for an exact or approximate time."
- "When the user is required to schedule tasks (E.g. reports)."

Practically, reach for TimeSelector when **all** of these are true:

- The user must enter a **specific time of day** (not a date, not a duration).
- The granularity needed is hours + minutes (and optionally AM/PM or a timezone — see [Pair 3](#pair-3--combine-12-hour-format-with-ampm-and-specify-a-timezone-when-the-time-matters)).
- A free-text input would be ambiguous (e.g. "5" could be `05:00`, `17:00`, or `05:00 AM`) — the structured input + dropdown removes that ambiguity.

### When not to use *(combines docs page + editorial)*

The docs page states only one rule: *"When time is not necessarily required. Reduce the content on a page by only asking for necessary data."* Cross-referencing the patterns observed elsewhere in the Oxygen system, the broader "when not to use" table is:

| Situation | Why | Use instead |
|-----------|-----|-------------|
| Time is **not strictly required** for the task | *(verbatim from the docs page)* Asking for time inflates the form and slows completion. | Drop the field; default to a sensible system value. |
| The user needs to pick a **date** (year-month-day) | TimeSelector handles hours / minutes only — there is no date axis in `TimeValue` ([props.md:94](./props.md)). | `Calendar` *(listed under Related on the docs page)*. |
| The user needs to pick a **date + time** together | A single TimeSelector can't capture both; pairing two inputs without explicit wiring tends to drift. | Compose `Calendar` with `TimeSelector`, or use a single date-time picker pattern (Forms). |
| The user needs to enter a **duration** (`90 minutes`, `2h 30m`) | TimeSelector enforces wall-clock semantics (hours 0–23, minutes 0–59), not arbitrary durations. | A `TextField` with explicit duration parsing, or two numeric inputs (`hours` + `minutes`). |
| The choice is between a small fixed set (e.g. "9 AM", "12 PM", "5 PM") | A full picker is overkill; a few buttons or radios scan faster. | `Radio` / `RadioGroup`, or a `Select` with the discrete options. |

**Source:** Published docs — Best Practices (verbatim "When to use" / "When not to use") · Related (Calendar, Forms) · cross-validated against [../Radio/Radio-usage.md](../Radio/Radio-usage.md) "many options → Select" rule.

---

## Do / Don't

> These pairs are derived editorially from the docs page's Behaviour + Time format + Best Practices sections combined with the extracted API, token, and (inferred) a11y data. No Figma ✅ Do / ❌ Don't card frames exist for TimeSelector at the time of writing (the `↳ TimeSelector examples` page is absent or was not located). Treat as provisional until a designer reviews them or a Figma examples page is created.

### Pair 1 — Reach for TimeSelector when the input is a time of day

#### ✅ Do — Use TimeSelector for hour-and-minute entry

The `TimeValue` shape — `{ hours, minutes, seconds }` ([props.md:94](./props.md)) — is purpose-built for a single moment within a day. Use it for meeting start times, report-window cutoffs, or scheduling triggers.

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

A TimeSelector models a wall-clock moment only — there's no calendar axis in `TimeValue` ([props.md:94](./props.md)), and the dropdown surface has no day-picker affordance ([timeselector-figma.md:54](./timeselector-figma.md)). Forcing it into duration or date roles produces ambiguous, hard-to-validate input.

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

**Source:** Published docs — Overview / Related (Calendar) · [props.md:94](./props.md) (`TimeValue` shape) · [timeselector-figma.md:54](./timeselector-figma.md) (input is "Time select", no date axis).

---

### Pair 2 — Control `value` with `onChange`; pre-populate when a sensible default exists

#### ✅ Do — Wire `value` + `onChange` as a controlled pair, and seed the value when you know it

The docs page is explicit: *"The time will default to a placeholder (e.g. `hh:mm` or `hh:mm AM`), if a time has been previously selected then that time will prepopulate the time input field."* Pass an initial `TimeValue` whenever you have one — the user's last choice, the system "now", or a sensible business default (start-of-day, top-of-hour). Use `onChange` to keep state in sync so re-renders don't drop user input ([examples.md:34](./examples.md), [props.md:65](./props.md)).

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

The component is designed as a controlled input — the docs page describes a populate-on-select interaction that requires a value source to read back from ([props.md:65](./props.md), [examples.md:36](./examples.md)). Rendering it without `value` + `onChange` either freezes the input or causes the parent to lose track of what the user entered.

```tsx
{/* Wrong — uncontrolled; the parent has no way to read what the user picked */}
<TimeSelector placeholder="hh:mm AM" />
```

**Source:** Published docs — Behaviour (populate-on-select, verbatim) · [props.md:65](./props.md) · [examples.md:30](./examples.md).

---

### Pair 3 — Combine 12-hour format with AM/PM, and specify a timezone when the time matters

#### ✅ Do — Pair 12-hour displays with AM/PM, and surface the timezone when the value is timezone-sensitive

The docs page asserts two rules verbatim: *"If using the 12-hour format it must be accompanied by an AM/PM to follow."* and *"Specific times should specify a timezone."* Surface the AM/PM marker in the placeholder so the user knows what the input expects, and label the field (or a sibling hint) with the timezone the system will interpret the value in.

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

Without AM/PM, `5:00` is ambiguous: morning or evening? Without a timezone label, `09:00` is ambiguous across users in different regions — a problem that compounds when the value is persisted and read back in a different session.

```tsx
{/* Wrong — 12-hour display with no AM/PM in placeholder or value */}
<TimeSelector
  value={{ hours: 5, minutes: 0, seconds: 0 }}
  onChange={setTime}
  placeholder="hh:mm"
  timeDisplayFormat="hh:mm"
/>
```

**Source:** Published docs — Time format (both rules verbatim) · [props.md:70](./props.md) (`timeDisplayFormat`) · `placeholder` example at [examples.md:71](./examples.md).

> ⚠️ **GAP-004:** `timeDisplayFormat` has no documented format-string syntax in the OX MCP. Verify your format string against the live Storybook before relying on it.

---

### Pair 4 — Use `hasError` together with an explicit error message + accessible wiring

#### ✅ Do — Set `hasError` and provide an error message that's announced to assistive tech

When validation fails, set `hasError={true}` so the input picks up the `--error/error01` 2 px border and exposes the Error Area below the input ([tokens.md:65](./tokens.md), [timeselector-figma.md:217](./timeselector-figma.md)). Pair it with an error message linked via `aria-describedby` and set `aria-invalid="true"` on the input ([accessibility.md:40](./accessibility.md), [accessibility.md:81](./accessibility.md)).

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

Setting `hasError` without a paired message gives sighted users a red border with no reason and gives screen-reader users no signal at all that the field is invalid. The red border alone also leans entirely on colour to convey state, which fails WCAG 1.4.1.

```tsx
{/* Wrong — error styling with no message and no aria wiring */}
<TimeSelector
  value={cutoff}
  onChange={setCutoff}
  hasError
/>
```

**Source:** [accessibility.md:76](./accessibility.md) (Error state expectations) · [tokens.md:65](./tokens.md) (`--error/error01` border) · [timeselector-figma.md:217](./timeselector-figma.md) (Error Area visual).

> ⚠️ **GAP-008:** The exact ARIA wiring above is inferred from time-picker conventions — verify against the rendered DOM before shipping.

---

### Pair 5 — Use `isDisabled` for "this input is intentionally locked"; don't hide an empty input behind disabled

#### ✅ Do — Disable when the field is meaningfully unavailable

`isDisabled={true}` ([props.md:73](./props.md)) sets the input to `--interactive/disabled01` background + `--interactive/disabled04` text ([tokens.md:65](./tokens.md)) and (per [accessibility.md:70](./accessibility.md)) removes the input from the focus order. Use it when the field has a real value that the user can read but can't currently change — for example, a scheduled-time field on a completed report.

```tsx
<TimeSelector
  isDisabled
  value={{ hours: 10, minutes: 30, seconds: 0 }}
  onChange={setTime}
/>
```

#### ❌ Don't — Disable an empty field as a placeholder for "fill this in later"

A disabled empty input gives no affordance to the user, drops out of the focus order, and may not meet contrast in the disabled state (see WARN-001 in [timeselector-audit.md](./timeselector-audit.md)). If the field isn't ready to be edited yet, hide it; if it's optional, leave it enabled with a placeholder.

```tsx
{/* Wrong — disabled empty field; the user can't tell what's expected here */}
<TimeSelector
  isDisabled
  value={undefined as any}
  onChange={setTime}
/>
```

**Source:** [props.md:73](./props.md) · [accessibility.md:68](./accessibility.md) (Disabled state) · [tokens.md:65](./tokens.md) (disabled tokens) · [timeselector-audit.md](./timeselector-audit.md) WARN-001 (disabled contrast).

---

### Pair 6 — Match `size` to context — reserve Large until the API conflict resolves

#### ✅ Do — Use `"default"` for forms and `"small"` for dense surfaces

The `TimeSelectorSize` enum exposes two values: `"small"` (32 px height, `$label01` typography) and `"default"` (40 px height, `$body01` typography) ([tokens.md:105](./tokens.md), [props.md:85](./props.md)). `"default"` is the right pick for stand-alone forms; `"small"` is appropriate for inline filters or tightly packed table cells where the 40 px height would crowd surrounding controls.

```tsx
{/* Form context */}
<TimeSelector value={time} onChange={setTime} />

{/* Dense filter / toolbar */}
<TimeSelector size="small" value={time} onChange={setTime} />
```

#### ❌ Don't — Author code against `size="large"` or assume Large is the default

Figma exposes a Large variant (48 px height, `$body02` typography) and uses it as the Figma default ([timeselector-figma.md:80](./timeselector-figma.md)), but the code API has no matching enum value — passing `size="large"` is a TypeScript error against `TimeSelectorSize` ([props.md:85](./props.md)), and `<TimeSelector />` rendered with no size prop falls back to `"default"` (Medium), not Large. Treat Large as design-only until **GAP-001** / **GAP-002** are resolved.

```tsx
{/* Wrong — "large" is not a value in TimeSelectorSize */}
<TimeSelector size={"large" as any} value={time} onChange={setTime} />
```

**Source:** [props.md:85](./props.md) (`TimeSelectorSize` enum) · [tokens.md:105](./tokens.md) (Size variants table) · [timeselector-figma.md:80](./timeselector-figma.md) (Figma Size axis) · [timeselector-audit.md](./timeselector-audit.md) GAP-001 / GAP-002.

---

## Accessibility quick reference

Cross-references to [accessibility.md](./accessibility.md). **All bullets below are inferred** (GAP-008) — verify against the rendered DOM before shipping:

- The input should be a `role="combobox"` (or a native `<input type="text">` with `aria-haspopup` pointing to the dropdown) ([accessibility.md:36](./accessibility.md)).
- `aria-expanded` should reflect whether the dropdown is open ([accessibility.md:37](./accessibility.md)).
- Pair the visible **Label** with the input via `for` / `id` or `aria-labelledby` ([accessibility.md:38](./accessibility.md)).
- Pair the **hint text** with the input via `aria-describedby` ([accessibility.md:39](./accessibility.md)).
- When `hasError={true}`, set `aria-invalid="true"` and link the error message via `aria-describedby` ([accessibility.md:40](./accessibility.md)).
- The focus ring uses `--interactive/focus01` (#0056E0) at 2 px ([accessibility.md:62](./accessibility.md), [tokens.md:65](./tokens.md)) — required by WCAG 2.4.7. Never suppress with `outline: none`.
- When the dropdown closes, focus must return to the trigger input ([accessibility.md:64](./accessibility.md)).
- `isDisabled={true}` should set `disabled` (or `aria-disabled="true"`) and remove the input from the focus order ([accessibility.md:70](./accessibility.md)).
- Required-field asterisk must be announced together with the label — don't hide it from assistive tech ([accessibility.md:87](./accessibility.md)).

See [accessibility.md](./accessibility.md) for the full WCAG 2.1 AA checklist.

---

## Related components

The published docs page lists these neighbours under **Related**:

- **Components → Calendar** — for date entry (year / month / day). See [Pair 1](#pair-1--reach-for-timeselector-when-the-input-is-a-time-of-day) for the inverse rule.
- **Patterns → Forms** — TimeSelector is most often used inside the broader Forms pattern (label + input + hint + error).

Editorial additions, based on the inverse rules in the "When not to use" table:

- **TextField** — for free-form duration entry (`90 minutes`, `2h 30m`) where wall-clock semantics don't apply.
- **Radio** / **Select** — when the time choice is a small, discrete set (`9 AM` / `12 PM` / `5 PM`).

---

## Gaps & open questions

| Item | Type | Description |
|------|------|-------------|
| Figma Do/Don't examples | SOURCE_GAP | No `↳ TimeSelector examples` Figma page with Do/Don't card frames was located. Pairs above are editorially derived from the docs page intent + extracted artifacts. Re-run `figma-extract-usage` if such a page is created. |
| `Size=Large` API alignment | CONFLICT | **GAP-001 / GAP-002** in [timeselector-audit.md](./timeselector-audit.md): Figma exposes `Size=Large` as the **Figma default**; code API only accepts `"small"`/`"default"`, with `"default"` ≡ Medium. Size guidance above documents the code reality; designers should treat Large as design-only until resolved. |
| `timeDisplayFormat` syntax | SOURCE_GAP | **GAP-004**: the accepted format-string syntax for `timeDisplayFormat` is undocumented (moment? date-fns? custom?). Verify any format against the live Storybook before relying on it. |
| Callbacks `onChange` / `onOpen` / `onClose` | SOURCE_GAP | **GAP-003**: callbacks appear in Storybook stories but are absent from the published OX MCP props list. Signatures inferred from usage. |
| Accessibility inference | SOURCE_GAP | **GAP-008**: all ARIA / keyboard / focus guidance is inferred from time-picker conventions — OX MCP returned no a11y docs and Figma annotations contain no a11y notes ([timeselector-figma.md:236](./timeselector-figma.md)). Verify the rendered DOM. |
| Disabled-state contrast | WARN-001 | Disabled state combines `--interactive/disabled04` (#8D8B7E) text on `--interactive/disabled01` (#C8C8BD) background — ratio may fall below 4.5:1. Verify before shipping unless a decorative exemption applies. |
| `ClockIcon` import path | WARN-002 | The left-icon example imports `ClockIcon` from `@8x8/oxygen-icons` ([examples.md:100](./examples.md)) — the package name is unverified. Confirm before publishing the example. |
| Border-radius / spacing tokens | DOC_GAP | The 6 px input radius, the 4 px inter-row gaps, and the 8 px intra-row gap are all hardcoded in Figma ([timeselector-figma.md:191](./timeselector-figma.md), [timeselector-figma.md:197](./timeselector-figma.md)). No design-token bindings observed. |

---

_Source: Published Oxygen docs page (`https://oxygen.8x8.com/components/timeselector/usage`, fetched 2026-05-15 via Claude_in_Chrome MCP) · Cross-referenced with Oxygen MCP extraction (`@8x8/oxygen-time-selector`) and the Figma design context already captured in [timeselector-figma.md](./timeselector-figma.md), [tokens.md](./tokens.md), and [accessibility.md](./accessibility.md) · Editorial draft 2026-05-15_
