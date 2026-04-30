# Slider — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [slider-pui.md](slider-pui.md)

## Installation

```bash
# yarn
yarn add @8x8/oxygen-slider

# npm
npm install @8x8/oxygen-slider
```

**Registry prerequisite** — add to `.npmrc` (or `.yarnrc.yml`):
```
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```
VPN connection required.

## Import

```tsx
import { Slider } from '@8x8/oxygen-slider';
```

## Type definitions

```ts
type RangeType = number | [number, number];
```

When `isMultiple` is `true`, `value` and `onChange` use the two-element tuple form `[number, number]`.

## Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `value` | `RangeType` | ✅ | — | Current value(s). Single `number` for standard; `[number, number]` for range (`isMultiple`). |
| `minValue` | `number` | — | — | Minimum value on the track. |
| `maxValue` | `number` | — | — | Maximum value on the track. |
| `step` | `number` | — | — | Increment step between selectable values. |
| `isDisabled` | `boolean` | — | `false` | Disables interaction; applies disabled visual state. |
| `isMultiple` | `true` | — | — | Enables range (two-thumb) mode. When set, `value` must be `[number, number]`. Typed as the literal `true` — omit to use single-thumb mode. |
| `isTrackDraggable` | `boolean` | — | — | When `true`, the user can drag the entire filled track to shift the range. |
| `ariaLabel` | `string` | — | — | Accessible label for the thumb(s). Required when there is no visible label nearby. |
| `onDragStart` | `() => void` | — | — | Fires when the user begins dragging a thumb. |
| `onDragEnd` | `() => void` | — | — | Fires when the user releases a thumb. |
| `onChange` | `(props: RangeType) => void` | — | — | Fires on every value change while dragging or after a click on the track. |
| `expandTrackAreaBy` | `string` | — | — | CSS length value that expands the invisible hit area of the track (e.g. `"8px"`). |
| `expandKnobAreaBy` | `string` | — | — | CSS length value that expands the invisible hit area of the thumb knob (e.g. `"8px"`). |
| `testId` | `string` | — | — | Data attribute for automated testing. |

## Notes

- `value` is the only required prop.
- `isMultiple` is typed as the literal `true` (not `boolean`) — use it as a flag, do not pass `false`.
- The `onChange` handler receives the same shape as `value`: a single number or a `[number, number]` tuple.

_Source: Oxygen MCP · Extracted 2026-04-29_
