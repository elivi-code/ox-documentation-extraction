---
component: Slider
parent: "[[Slider]]"
section: composition
role: spoke
pipeline_stage: spec_ready
audit_verdict: PARTIAL
siblings:
  - "[[Slider]]"
  - "[[Slider.props]]"
  - "[[Slider.anatomy]]"
  - "[[Slider.tokens]]"
  - "[[Slider.usage]]"
  - "[[Slider.accessibility]]"
  - "[[Slider.platform]]"
tags:
  - oxygen
  - component/Slider
  - role/spoke
  - section/composition
  - stage/spec_ready
---

## Subcomponents

No documented subcomponents — the Slider is a leaf component. Internal elements (track, thumb, focus ring) are implementation details, not exposed as separate Oxygen components.

## Patterns

### Audio Volume pattern

The canonical Slider usage is the **"Audio Volume"** pattern (Figma node `22902:37514`):

| Slot | Content |
|------|---------|
| Left | `volume-off` icon (20×20 px) |
| Center | Slider track (with optional label above) |
| Right | `volume-up` icon (20×20 px) |

This layout is the primary Figma reference for Slider and the pattern against which design tokens and states are documented.

### Range selection pattern

When `isMultiple` is set, the Slider becomes a range selector. The `isTrackDraggable` prop allows the entire filled band to be dragged as a unit.

```tsx
<Slider isMultiple isTrackDraggable value={[30, 70]} onChange={setRange} ariaLabel="Volume range" />
```

## Related components

| Component | Relationship |
|-----------|-------------|
| [[Dropdown]] | Alternative when the user is selecting from a few discrete named options (per OX usage guidelines) |
| [[Switch]] | Alternative for binary on/off controls |

## Props that accept components

| Prop | Description |
|------|-------------|
| _(none)_ | The Slider does not expose any prop that accepts a React component or element as its value. Left/right icon slots are layout conventions in the consuming layout, not a formal prop. |

_Source: derived from source/examples.md + source/Slider-usage.md · 2026-04-29 / 2026-05-15_
