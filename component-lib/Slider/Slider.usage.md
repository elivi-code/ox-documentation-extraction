---
component: Slider
parent: "[[Slider]]"
section: usage
role: spoke
pipeline_stage: spec_ready
audit_verdict: PARTIAL
source_type: editorial
siblings:
  - "[[Slider]]"
  - "[[Slider.props]]"
  - "[[Slider.anatomy]]"
  - "[[Slider.tokens]]"
  - "[[Slider.accessibility]]"
  - "[[Slider.platform]]"
  - "[[Slider.composition]]"
tags:
  - oxygen
  - component/Slider
  - role/spoke
  - section/usage
  - stage/spec_ready
---

<!-- SOURCE: editorial — no Figma "↳ Slider examples" page exists -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- REFERENCE PAGE: https://oxygen.8x8.com/components/slider/usage -->
<!-- GROUNDING: full — props.md, examples.md, accessibility.md, tokens.md, slider-pui.md, slider-audit.md, oxygen.8x8.com/components/slider/usage -->
<!-- DRAFTED: 2026-05-15 -->
<!-- PAIRS: 6 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma examples page is created -->

> **Editorial guidance — not Figma-sourced.** No `↳ Slider examples` Figma page exists, so `figma-extract-usage` cannot run. The Do/Don't pairs below are inferred from `props.md`, `examples.md`, `accessibility.md`, `tokens.md`, `slider-pui.md`, and the public usage page at [oxygen.8x8.com/components/slider/usage](https://oxygen.8x8.com/components/slider/usage). Treat as provisional until a designer reviews them. Replace with `figma-extract-usage` output when a Figma examples page is created.

`Slider` lets users select a value on a horizontal track by dragging the thumb or clicking the track. Its canonical use is **audio volume** — the Figma reference pattern is literally named "Audio Volume" — and more broadly any continuous value where approximating is acceptable. The component supports a single thumb, a two-thumb range (`isMultiple`), and a draggable filled track (`isTrackDraggable`).

---

## When to use

- The user needs to choose a value from **0 to 100 percent**.
- **Volume control** — audio in / audio out, ringer, microphone gain.
- **Range selection** with a meaningful min and max — price range, time window — using `isMultiple` with a `[number, number]` value.
- The value is **bounded and continuous**, and the user is happy approximating to the nearest `step`.

## When not to use

| Situation | Use instead |
|-----------|-------------|
| There are only a few discrete options to choose from | [[Dropdown]] |
| The range of values is large (e.g. 0–10 000) | Numeric input |
| High-precision values are required (exact amounts, exact timestamps) | Numeric input |
| The control is binary (on / off) | [[Switch]] |

---

## Do / Don't

<!-- SCREENSHOTS UNAVAILABLE — no Figma examples page exists for Slider -->

### Pair 1 — Use Slider for continuous, bounded values; reach for a different control for a few options

#### ✅ Do — Use Slider for 0–100% selection or volume control

The Slider is the right control when the user is choosing a value on a continuous, bounded scale where "near enough" is acceptable. Volume is the canonical example — the user wants "louder" or "quieter", not exactly `73`. Bind `minValue` / `maxValue` to the percent range and pick a small `step` so movement feels smooth.

```tsx
function VolumeControl() {
  const [value, setValue] = useState(50);
  return (
    <Slider value={value} minValue={0} maxValue={100} step={1}
      ariaLabel="Ring volume" onChange={setValue} />
  );
}
```

**Grounded in:** oxygen.8x8.com — "When to use: Use a slider when the user needs to choose a value from 0 to 100 percent. Use the slider for volume control."

#### ❌ Don't — Use Slider when the user is choosing between a handful of discrete options

If the choices are "Low / Medium / High" or "1× / 2× / 4× / 8×", a slider forces the user to drag-and-snap. A Dropdown lets them pick the named option directly.

```tsx
// ❌ Four-option playback speed — Slider is the wrong control
<Slider value={2} minValue={1} maxValue={4} step={1} ariaLabel="Speed" />
```

**Grounded in:** oxygen.8x8.com — "When not to use: If there are a few options to choose from. Consider using a dropdown instead."

---

### Pair 2 — Slider for approximate values, numeric input for precision

#### ✅ Do — Use Slider when "approximately right" is good enough

Sliders excel when the user can land on a value by feel — gain, brightness, opacity, volume. The fast drag motion lets them sweep across the range and stop where it sounds / looks / feels right.

```tsx
<Slider value={value} minValue={0} maxValue={100} step={1}
  ariaLabel="Microphone gain" onChange={setValue} />
```

#### ❌ Don't — Use Slider when the user must land on an exact value, or when the range is huge

If the user is entering a dollar amount or any value where being off by a unit matters, the slider makes them aim instead of type.

```tsx
// ❌ Exact-amount entry — Slider can't land on $1,247.50 reliably
<Slider value={value} minValue={0} maxValue={10000} step={0.01} ariaLabel="Amount" />
```

**Grounded in:** oxygen.8x8.com — "When not to use: If there is a large range to choose from. When high-precision values are required."

---

### Pair 3 — Use `isMultiple` for genuine min/max ranges; don't stack two single sliders

#### ✅ Do — Use range mode (`isMultiple`) when the user picks a band, not a point

```tsx
function RangeSlider() {
  const [range, setRange] = useState<[number, number]>([20, 80]);
  return (
    <Slider isMultiple value={range} minValue={0} maxValue={100}
      step={5} onChange={setRange} ariaLabel="Volume range" />
  );
}
```

#### ❌ Don't — Render two single sliders side-by-side when the values are a min/max pair

Two independent sliders let the user set `min > max` and force them to compare two separate tracks to understand the range.

```tsx
// ❌ Two single sliders for a range — fragile and visually disconnected
<Slider value={min} onChange={setMin} ariaLabel="Minimum" />
<Slider value={max} onChange={setMax} ariaLabel="Maximum" />
```

---

### Pair 4 — Always label the slider

#### ✅ Do — Pair the Slider with a visible label, or supply `ariaLabel` when no label is present

The thumb renders as `role="slider"` and screen readers announce only a number by default. A visible label or `ariaLabel` tells users what they're adjusting.

```tsx
<div>
  <label htmlFor="ring-volume">Ring volume</label>
  <Slider value={value} onChange={setValue} ariaLabel="Ring volume" />
</div>
```

#### ❌ Don't — Ship a Slider with no visible label and no `ariaLabel`

Without either, screen readers announce a bare number — "Slider, 50, 0 to 100" with no context. Fails WCAG 4.1.2 (Name, Role, Value).

```tsx
// ❌ No label and no ariaLabel
<Slider value={value} onChange={setValue} />
```

---

### Pair 5 — Expand the hit area on touch and dense layouts

#### ✅ Do — Use `expandKnobAreaBy` (and `expandTrackAreaBy`) to reach a 44×44 target on touch surfaces

The visible thumb is 16×16 px at rest. On touch, that's below the WCAG 2.5.5 Target Size minimum. Both props enlarge the invisible hit region without changing the visual size.

```tsx
<Slider value={value} onChange={setValue}
  expandTrackAreaBy="8px" expandKnobAreaBy="8px" ariaLabel="Ring volume" />
```

#### ❌ Don't — Ship the 16px default thumb in a dense, touch-driven layout

A dense list of sliders with the default 16px thumb is unhittable on phones — users tap, miss, drag the wrong row.

```tsx
// ❌ Mixer column with default-size thumbs — taps will miss
{channels.map(c => (
  <Slider key={c.id} value={c.level} onChange={c.set} ariaLabel={c.name} />
))}
```

---

### Pair 6 — Show the value when the user needs to confirm it

#### ✅ Do — Render the current numeric value alongside the slider when accuracy matters

Subscribe to `onChange` and render the value in a sibling element. Use `aria-hidden` on the visible readout to avoid double-announcement — screen readers already track `aria-valuenow`.

```tsx
function VolumeWithReadout() {
  const [value, setValue] = useState(50);
  return (
    <div style={{ display: 'flex', alignItems: 'center', gap: '12px' }}>
      <Slider value={value} minValue={0} maxValue={100} step={1}
        ariaLabel="Ring volume" onChange={setValue} />
      <span aria-hidden="true">{value}%</span>
    </div>
  );
}
```

#### ❌ Don't — Hide the value entirely when the user needs to dial a specific number

A slider with no readout asks the user to estimate where on the track corresponds to 75. Either show the value or replace the slider with a numeric input.

```tsx
// ❌ No readout — user can't verify they landed on 75
<Slider value={value} onChange={setValue} ariaLabel="Volume" />
```

---

## Gaps & open questions

| ID | Description |
|----|-------------|
| GAP-USAGE-001 | No Figma examples page exists for Slider. These Do/Don't pairs should be replaced with Figma-sourced ones once a `↳ Slider examples` page is created. |
| GAP-USAGE-002 | `slider-figma.md` is not yet extracted (audit GAP-001). Once `figma-extract` runs, anatomy citations in pair 3 should be updated. |
| GAP-USAGE-003 | Disabled state ergonomics (when to disable vs. hide) are not addressed on the OX usage page. |
| GAP-USAGE-004 | Value-readout placement guidance (above track, beside it, tooltip-on-drag) is editorial — not from OX design system. |

_Source: editorial guidance authored from extracted artifacts and oxygen.8x8.com/components/slider/usage · No Figma examples page available · 2026-05-15_
