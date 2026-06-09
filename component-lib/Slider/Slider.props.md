---
component: Slider
parent: "[[Slider]]"
section: props
role: spoke
pipeline_stage: spec_ready
audit_verdict: PARTIAL
siblings:
  - "[[Slider]]"
  - "[[Slider.anatomy]]"
  - "[[Slider.tokens]]"
  - "[[Slider.usage]]"
  - "[[Slider.accessibility]]"
  - "[[Slider.platform]]"
  - "[[Slider.composition]]"
tags:
  - oxygen
  - component/Slider
  - role/spoke
  - section/props
  - stage/spec_ready
---

## Props

| Name | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | `RangeType` | — | ✅ | Current value(s). Single `number` for standard mode; `[number, number]` for range mode (`isMultiple`). |
| `minValue` | `number` | — | — | <!-- STUB:GAP-004 source="Add description from @8x8/oxygen-slider README or JSDoc" --> Minimum value on the track. |
| `maxValue` | `number` | — | — | <!-- STUB:GAP-004 source="Add description from @8x8/oxygen-slider README or JSDoc" --> Maximum value on the track. |
| `step` | `number` | — | — | <!-- STUB:GAP-004 source="Add description from @8x8/oxygen-slider README or JSDoc" --> Increment step between selectable values. |
| `isDisabled` | `boolean` | `false` | — | Disables interaction; applies disabled visual state. |
| `isMultiple` | `true` | — | — | Enables range (two-thumb) mode. When set, `value` must be `[number, number]`. Typed as the literal `true` — omit to use single-thumb mode. |
| `isTrackDraggable` | `boolean` | — | — | When `true`, the user can drag the entire filled track to shift the range. |
| `ariaLabel` | `string` | — | — | Accessible label for the thumb(s). Functionally required when there is no visible label nearby (see [[Slider.accessibility]]). |
| `onDragStart` | `() => void` | — | — | Fires when the user begins dragging a thumb. |
| `onDragEnd` | `() => void` | — | — | Fires when the user releases a thumb. |
| `onChange` | `(props: RangeType) => void` | — | — | Fires on every value change while dragging or after a click on the track. Receives the same shape as `value`. |
| `expandTrackAreaBy` | `string` | — | — | <!-- STUB:GAP-004 source="Add description from @8x8/oxygen-slider README or JSDoc" --> CSS length value that expands the invisible hit area of the track (e.g. `"8px"`). |
| `expandKnobAreaBy` | `string` | — | — | <!-- STUB:GAP-004 source="Add description from @8x8/oxygen-slider README or JSDoc" --> CSS length value that expands the invisible hit area of the thumb knob (e.g. `"8px"`). |
| `testId` | `string` | — | — | Data attribute for automated testing. |

> **Default values (GAP-003):** 13 of 14 props show no default. The OX MCP returned no defaults. Only `isDisabled=false` is confirmed. Inspect `@8x8/oxygen-slider` `argsConfig` in Storybook to recover defaults for `minValue`, `maxValue`, `step`, `isTrackDraggable`.
<!-- SKIP:GAP-003 manual="Default values not in MCP source — inspect @8x8/oxygen-slider argsConfig in Storybook" -->

## Type definitions

```ts
type RangeType = number | [number, number];
```

When `isMultiple` is `true`, `value` and `onChange` use the two-element tuple form `[number, number]`.

## Installation

```bash
yarn add @8x8/oxygen-slider
# or
npm install @8x8/oxygen-slider
```

Registry prerequisite — add to `.npmrc`:
```
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```
VPN connection required.

## Import

```tsx
import { Slider } from '@8x8/oxygen-slider';
```

## Notes

- `value` is the only required prop.
- `isMultiple` is typed as the literal `true` (not `boolean`) — use it as a flag; do not pass `false`.
- The `onChange` handler receives the same shape as `value`: a single number or a `[number, number]` tuple.
- `ariaLabel` is optional in the type system but functionally required when no visible label is associated — see [[Slider.accessibility]].

_Source: Oxygen MCP · Extracted 2026-04-29_
