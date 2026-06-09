---
component: Slider
package: "@8x8/oxygen-slider"
category: form_inputs
role: usage
role_description: "Usage guidelines — editorially authored from extracted artifacts and the public Oxygen Slider usage page; no Figma examples page exists"
pipeline_stage: editorial
pipeline_note: "Authored editorially from extracted artifacts + oxygen.8x8.com/components/slider/usage — NOT from Figma Do/Don't frames. Re-run doc-audit after creation; replace pairs with figma-extract-usage output when a Figma examples page is created."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Slider/props]]"
  - "[[Slider/examples]]"
  - "[[Slider/tokens]]"
  - "[[Slider/accessibility]]"
  - "[[Slider/slider-pui]]"
  - "[[Slider/slider-figma]]"
  - "[[Slider/slider-audit]]"
tags:
  - oxygen
  - component/Slider
  - role/usage
  - stage/editorial
  - category/form_inputs
---
<!-- SOURCE: editorial — no Figma "↳ Slider examples" page exists -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- REFERENCE PAGE: https://oxygen.8x8.com/components/slider/usage -->
<!-- GROUNDING: full — props.md, examples.md, accessibility.md, tokens.md, slider-pui.md, slider-audit.md, oxygen.8x8.com/components/slider/usage -->
<!-- DRAFTED: 2026-05-15 -->
<!-- MODE: open -->
<!-- PAIRS: 6 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma examples page is created -->

# Slider — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [slider-pui.md](./slider-pui.md) · [slider-audit.md](./slider-audit.md)

> **Editorial guidance — not Figma-sourced.** No `↳ Slider examples` Figma page exists, so `figma-extract-usage` cannot run. The Do/Don't pairs below are inferred from `props.md`, `examples.md`, `accessibility.md`, `tokens.md`, `slider-pui.md`, and the public usage page at [oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage). Treat as provisional until a designer reviews them. Replace with `figma-extract-usage` output when a Figma examples page is created.

`Slider` lets users select a value on a horizontal track by dragging the thumb or clicking the track. Its canonical use is **audio volume** — the Figma reference pattern is literally named "Audio Volume" ([examples.md](./examples.md) line 148) — and more broadly any continuous value where approximating ("loud enough", "around 60%") is acceptable. The component supports a single thumb, a two-thumb range (`isMultiple`), and a draggable filled track (`isTrackDraggable`).

---

## When to use

- The user needs to choose a value from **0 to 100 percent** ([oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage) — "When to use").
- **Volume control** — audio in / audio out, ringer, microphone gain ([oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage) — "When to use"; [examples.md](./examples.md) "Audio Volume" Figma pattern).
- **Range selection** with a meaningful min and max — price range, time window — using `isMultiple` with a `[number, number]` value ([examples.md](./examples.md) lines 71–91).
- The value is **bounded and continuous**, and the user is happy approximating to the nearest `step`.

## When not to use

| Situation | Use instead |
|-----------|-------------|
| There are only a few discrete options to choose from | [Dropdown](../Dropdown/) — per [oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage) — "When not to use: If there are a few options to choose from. Consider using a dropdown instead." |
| The range of values is **large** (e.g. 0–10 000) | A numeric input — per [oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage) — "When not to use: If there is a large range to choose from." |
| **High-precision** values are required (e.g. exact currency amounts, exact timestamps) | A numeric input — per [oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage) — "When not to use: When high-precision values are required." |
| The control is binary (on / off) | [Switch](../Switch/) (inferred — common Oxygen UX rule; not stated on the Slider usage page) |

---

## Do / Don't

<!-- SCREENSHOTS UNAVAILABLE — no Figma examples page exists for Slider -->

### Pair 1 — Use Slider for continuous, bounded values; reach for a different control for a few options

#### ✅ Do — Use Slider for 0–100% selection or volume control

> The Slider is the right control when the user is choosing a value on a continuous, bounded scale where "near enough" is acceptable. Volume is the canonical example — the user wants "louder" or "quieter", not exactly `73`. Bind `minValue` / `maxValue` to the percent range and pick a small `step` so movement feels smooth.

```tsx
import { Slider } from '@8x8/oxygen-slider';
import { useState } from 'react';

function VolumeControl() {
  const [value, setValue] = useState(50);

  return (
    <Slider
      value={value}
      minValue={0}
      maxValue={100}
      step={1}
      ariaLabel="Ring volume"
      onChange={setValue}
    />
  );
}
```

**Grounded in:** [oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage) — "When to use: Use a slider when the user needs to choose a value from 0 to 100 percent. Use the slider for volume control."; [examples.md](./examples.md) lines 27–47 (Basic — controlled single-thumb "Ring volume" example); [examples.md](./examples.md) lines 148–158 (Figma "Audio Volume" pattern reference).

#### ❌ Don't — Use Slider when the user is choosing between a handful of discrete options

> If the choices are "Low / Medium / High" or "1× / 2× / 4× / 8×", a slider forces the user to drag-and-snap to a value that maps to a label. A Dropdown lets them pick the named option directly, with no aiming.

```tsx
// ❌ A four-option playback speed — Slider is the wrong control
<Slider value={2} minValue={1} maxValue={4} step={1} ariaLabel="Speed" />

// ✅ Use Dropdown when there are a few labelled options
// <Dropdown options={[{ value: 1, label: '1×' }, ... ]} />
```

**Grounded in:** [oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage) — "When not to use: If there are a few options to choose from. Consider using a dropdown instead."

---

### Pair 2 — Slider for approximate values, numeric input for precision

#### ✅ Do — Use Slider when "approximately right" is good enough

> Sliders excel when the user can land on a value by feel — gain, brightness, opacity, volume. The fast drag motion lets them sweep across the range and stop where it sounds / looks / feels right. Combine the slider with a visible numeric readout if users want to confirm the value, but the **selection** is gestural.

```tsx
<Slider
  value={value}
  minValue={0}
  maxValue={100}
  step={1}
  ariaLabel="Microphone gain"
  onChange={setValue}
/>
```

**Grounded in:** [oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage) — Behavior: "Allows the user to control adjustable content by moving the thumb along the horizontal track between the minimum and maximum values."; [examples.md](./examples.md) lines 27–47 (volume example with `step={1}`).

#### ❌ Don't — Use Slider when the user must type / land on an exact value, or when the range is huge

> If the user is entering a dollar amount, a date, or any value where being off by a unit matters, the slider makes them aim instead of type. The OX usage page calls this out explicitly: large ranges and high-precision values are both anti-patterns. Use a numeric input or a stepper.

```tsx
// ❌ Exact-amount entry — Slider can't land on $1,247.50 reliably
<Slider value={value} minValue={0} maxValue={10000} step={0.01} ariaLabel="Amount" />

// ❌ Wide range — dragging across 0–10000 is coarse
<Slider value={value} minValue={0} maxValue={10000} ariaLabel="Bandwidth" />
```

**Grounded in:** [oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage) — "When not to use: If there is a large range to choose from."; "When not to use: When high-precision values are required."

---

### Pair 3 — Use `isMultiple` for genuine min/max ranges; don't stack two single sliders

#### ✅ Do — Use range mode (`isMultiple`) when the user picks a band, not a point

> When the user selects a window — a price range, a date range, a min/max volume — use the two-thumb mode by passing `isMultiple` and a `[number, number]` value. Both thumbs share one track, so the relationship between min and max is visually clear and a single drag can shift the band (`isTrackDraggable`).

```tsx
import { Slider } from '@8x8/oxygen-slider';
import { useState } from 'react';

function RangeSlider() {
  const [range, setRange] = useState<[number, number]>([20, 80]);

  return (
    <Slider
      isMultiple
      value={range}
      minValue={0}
      maxValue={100}
      step={5}
      onChange={setRange}
      ariaLabel="Volume range"
    />
  );
}
```

**Grounded in:** [props.md](./props.md) lines 73 (`isMultiple` — "Enables range (two-thumb) mode. When set, `value` must be `[number, number]`."); [props.md](./props.md) line 74 (`isTrackDraggable` — "the user can drag the entire filled track to shift the range"); [examples.md](./examples.md) lines 71–91 (Range two-thumb example); [examples.md](./examples.md) lines 93–103 (Track-draggable range example).

#### ❌ Don't — Render two single sliders side-by-side when the values are a min/max pair

> Two independent sliders let the user set `min > max` and force them to compare two separate tracks to understand the range. The two-thumb mode keeps the values on one axis and prevents min/max inversion automatically.

```tsx
// ❌ Two single sliders for a range — fragile and visually disconnected
<Slider value={min} onChange={setMin} ariaLabel="Minimum" />
<Slider value={max} onChange={setMax} ariaLabel="Maximum" />

// ✅ One range slider — see the Do example above
```

**Grounded in:** [props.md](./props.md) lines 73 (`isMultiple` exists precisely so two-thumb selection doesn't need two component instances); [examples.md](./examples.md) lines 71–91 (canonical range pattern).

---

### Pair 4 — Always label the slider

#### ✅ Do — Pair the Slider with a visible label, or supply `ariaLabel` when no label is present

> The thumb renders as `role="slider"` and screen readers will announce only `aria-valuenow` (a number) by default — "50", with no context. A visible `<label>` (or a label-adjacent text element) tells sighted users *what* they're adjusting; `ariaLabel` does the same for screen-reader users when no visible label is possible.

```tsx
// ✅ Visible label adjacent to the slider
<div>
  <label htmlFor="ring-volume">Ring volume</label>
  <Slider
    value={value}
    onChange={setValue}
    ariaLabel="Ring volume"
  />
</div>
```

**Grounded in:** [accessibility.md](./accessibility.md) lines 29–35 (ARIA role section — "The component uses the `ariaLabel` prop to set `aria-label` on the thumb element when no visible label is associated with it. … either pass `ariaLabel` or place a visible `<label>`."); [accessibility.md](./accessibility.md) lines 39–45 (Required ARIA attributes — `aria-label` derived from `ariaLabel` prop); [accessibility.md](./accessibility.md) line 99 (WCAG 2.5.3 Label in Name — "`ariaLabel` should match or contain the visible label text"); [props.md](./props.md) line 75 (`ariaLabel` — "Required when there is no visible label nearby").

#### ❌ Don't — Ship a Slider with no visible label *and* no `ariaLabel`

> Without either, screen readers announce a bare number when the thumb is focused — "Slider, 50, 0 to 100" with no clue what is being controlled. The slider is then unusable to assistive-tech users and fails WCAG 4.1.2 (Name, Role, Value).

```tsx
// ❌ No label and no ariaLabel — screen reader announces only the number
<Slider value={value} onChange={setValue} />
```

**Grounded in:** [accessibility.md](./accessibility.md) line 101 (WCAG 4.1.2 Name, Role, Value); [props.md](./props.md) line 75 (`ariaLabel` is conditionally required).

---

### Pair 5 — Expand the hit area on touch and dense layouts

#### ✅ Do — Use `expandKnobAreaBy` (and `expandTrackAreaBy`) to reach a 44×44 target on touch surfaces

> The visible thumb is `16×16 px` at rest ([tokens.md](./tokens.md) line 70). On touch, that's below the WCAG 2.5.5 Target Size minimum (44×44 CSS px). Both `expandKnobAreaBy` and `expandTrackAreaBy` enlarge the *invisible* hit region without changing the visual size — so the design stays compact but taps land.

```tsx
<Slider
  value={value}
  onChange={setValue}
  expandTrackAreaBy="8px"
  expandKnobAreaBy="8px"
  ariaLabel="Ring volume"
/>
```

**Grounded in:** [accessibility.md](./accessibility.md) lines 82–87 (Touch / pointer — "The `expandTrackAreaBy` and `expandKnobAreaBy` props increase the invisible hit area … use them on mobile to meet the WCAG 2.5.5 Target Size (44×44 CSS pixel) success criterion."); [accessibility.md](./accessibility.md) line 100 (WCAG 2.5.5 — "Default thumb is 16px; use `expandKnobAreaBy` on touch to reach 44px"); [props.md](./props.md) lines 79–80 (`expandTrackAreaBy`, `expandKnobAreaBy` — CSS length values); [tokens.md](./tokens.md) lines 67–72 (thumb geometry — 16px default).

#### ❌ Don't — Ship the 16px default thumb in a dense, touch-driven layout

> A dense list of sliders (an audio mixer, a per-channel volume column) with the default 16px thumb is unhittable on phones — users tap, miss, drag the wrong row. Set `expandKnobAreaBy` so the thumb's effective target is ≥44×44 regardless of the visual size.

```tsx
// ❌ Mixer column with default-size thumbs — taps will miss
{channels.map(c => (
  <Slider key={c.id} value={c.level} onChange={c.set} ariaLabel={c.name} />
))}
```

**Grounded in:** [accessibility.md](./accessibility.md) line 100 (WCAG 2.5.5 violation when default 16px thumb is used on touch); [tokens.md](./tokens.md) lines 67–72 (thumb sizes — 16px default, only 32px on Hover/Active which is mouse-only state).

---

### Pair 6 — Show the value when the user needs to confirm it

#### ✅ Do — Render the current numeric value alongside the slider when accuracy matters

> The OX usage page calls out high-precision selection as an anti-pattern, but most real sliders sit between "rough" and "exact". Showing the value as text next to the track lets the user **verify** what they landed on without taking the focus away from the gesture. Subscribe to `onChange` and render the value in a sibling element.

```tsx
import { Slider } from '@8x8/oxygen-slider';
import { useState } from 'react';

function VolumeWithReadout() {
  const [value, setValue] = useState(50);

  return (
    <div style={{ display: 'flex', alignItems: 'center', gap: '12px' }}>
      <Slider
        value={value}
        minValue={0}
        maxValue={100}
        step={1}
        ariaLabel="Ring volume"
        onChange={setValue}
      />
      <span aria-hidden="true">{value}%</span>
    </div>
  );
}
```

**Grounded in:** [oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage) — "When not to use: When high-precision values are required." (the readout closes the precision gap when the gesture is still right); [accessibility.md](./accessibility.md) lines 73–78 (Screen reader guidance — `aria-valuenow` already announces the value; `aria-hidden` on the visible readout avoids double-announcement); [props.md](./props.md) line 78 (`onChange` fires on every value change while dragging).

#### ❌ Don't — Hide the value entirely when the user needs to dial a specific number

> A slider with no readout asks the user to estimate where on the track corresponds to `75`. On dense or short tracks that's a guess. Either show the value or replace the slider with a numeric input — don't make the user infer the number from the thumb position.

```tsx
// ❌ No readout, user can't verify they landed on 75
<Slider value={value} onChange={setValue} ariaLabel="Volume" />
```

**Grounded in:** [oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage) — high-precision anti-pattern; [accessibility.md](./accessibility.md) line 76 ("When the value changes, screen readers announce the new `aria-valuenow` automatically" — sighted users deserve the same affordance).

---

## Gaps & open questions

| ID | Type | Description |
|----|------|-------------|
| — | Editorial | These Do/Don't pairs are authored from extracted artifacts and the public oxygen.8x8.com Slider usage page, not from a Figma examples page. They should be reviewed by a designer and replaced with Figma-sourced pairs once a `↳ Slider examples` page is created. |
| GAP-USAGE-001 | Source gap | No Figma examples page exists for Slider. The public usage page at [oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage) provides only behaviour text and a "When to use / When not to use" list — **no Do/Don't cards, no accessibility examples, no range-mode guidance**. A Figma examples page would let `figma-extract-usage` run and replace this editorial draft. |
| GAP-USAGE-002 | Source gap | `slider-figma.md` is **not yet extracted** (audit GAP-001, SOURCE_GAP). Once `figma-extract` runs against node `22902:37514`, the anatomy and variant references in pair 3 should be replaced with canonical citations. |
| GAP-USAGE-003 | Source gap | The OX usage page does not address **disabled state** ergonomics — when to disable vs. hide, whether a disabled slider should still show the current value, etc. Inferred guidance for "Switch instead of Slider for binary controls" is not stated on the OX page either. |
| GAP-USAGE-004 | Source gap | The OX usage page does not address **value-readout placement** (above the track, beside it, in a tooltip on drag). Pair 6's recommendation is editorial. |

---

_Source: editorial guidance authored from extracted artifacts (props.md, examples.md, accessibility.md, tokens.md, slider-pui.md, slider-audit.md) and the public usage page at oxygen.8x8.com/components/slider/usage · No Figma examples page available · 2026-05-15_
