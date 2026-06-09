---
parent: "[[TimeSelector]]"
section: props
component: TimeSelector
pipeline_stage: draft
tags:
  - oxygen
  - component/TimeSelector
  - role/spoke
  - section/props
  - category/date_time
---

## Props

| Name | Type | Default | Required | Description | Accepts |
|------|------|---------|----------|-------------|---------|
| `value` | `TimeValue` | — | No | Current time value (`{ hours, minutes, seconds }`) | — |
| `onChange` | `(value: TimeValue) => void` | — | No | Callback fired when the selected time changes | — |
| `onOpen` | `() => void` | — | No | Callback fired when the picker opens | — |
| `onClose` | `() => void` | — | No | Callback fired when the picker closes | — |
| `size` | `TimeSelectorSize` | `"default"` | No | Size variant — `"small"` or `"default"` (≡ Figma Medium) | — |
| `timeDisplayFormat` | `string` | — | No | Format string controlling how the time is displayed in the input | — |
| `placeholder` | `string` | — | No | Placeholder text shown when no value is selected | — |
| `hasError` | `boolean` | `false` | No | Puts the input into an error state (red border + error message slot) | — |
| `isDisabled` | `boolean` | `false` | No | Disables the component — prevents interaction | — |
| `isLeftIconVisible` | `boolean` | `false` | No | Shows/hides the leading icon inside the input | — |
| `iconLeft` | `React.ComponentType<IconProps>` | — | No | Icon component rendered on the left side of the input (requires `isLeftIconVisible: true`) | [[Icon]] |
| `id` | `string` | — | No | HTML `id` attribute on the input element | — |
| `testId` | `string` | — | No | `data-testid` attribute for automated testing | — |
| `portalRef` | `React.RefObject<HTMLElement>` | — | No | Ref to a DOM node where the dropdown portal should be rendered | — |

<!-- STUB:GAP-003 source="Verify callback signatures (onChange, onOpen, onClose) against the live component source or package type declarations; add official descriptions to source/props.md once confirmed. Currently inferred from Storybook usage patterns." -->
<!-- STUB:GAP-004 source="Retrieve official descriptions for hasError and timeDisplayFormat from package source or changelog; document accepted timeDisplayFormat pattern strings (moment? date-fns? custom?) with format examples." -->

## Type definitions

### `TimeSelectorSize`

```ts
type TimeSelectorSize = "small" | "default";
```

`"default"` corresponds to **Medium** in Figma design specs. Figma also exposes `Size=Large` which is absent from the code API — see [[TimeSelector.anatomy]] for the unresolved conflict (GAP-001 / GAP-002).

### `TimeValue`

```ts
type TimeValue = {
  hours: number;
  minutes: number;
  seconds: number;
};
```

## Installation

```bash
# yarn
yarn add @8x8/oxygen-time-selector

# npm
npm install @8x8/oxygen-time-selector
```

**Registry prerequisite** — must be on 8x8 VPN with the Artifactory registry configured:

`.npmrc`:
```
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```
