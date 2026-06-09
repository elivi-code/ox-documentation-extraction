---
parent: "[[Radio]]"
section: props
---

## Props

### `Radio`

| Name | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `testId` | `string` | `'RADIO'` | yes | Test ID for the radio input element |
| `label` | `node` | `''` | yes | Label content for the radio input |
| `value` | `number \| string \| bool \| { id: string }` | `''` | yes | Radio input value — matched against the parent `RadioGroup`'s selected value |
| `name` | `string` | — | yes | `name` attribute for the native radio input |
| `isChecked` | `bool` | `false` | yes | Whether the radio input is checked |
| `isDisabled` | `bool` | `false` | yes | Disabled state |
| `onChange` | `func` | `noop` | yes | Change callback |
| `infoBoxText` | `node` | — | yes | Renders an info icon that shows this text inside a Tooltip on click |
| `infoBoxButtonLabel` | `string` | — | yes | Accessible `aria-label` for the info icon button; required when `infoBoxText` is used |

#### `value` type detail

```ts
value: number | string | boolean | { id: string }
```

Used to match against the `RadioGroup`'s `value` prop to determine checked state.

---

### `RadioGroup`

`RadioGroup` is the container that manages selection state across a set of `Radio` children.

| Name | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `ReactNode` | — | no | `Radio` components |
| `value` | `Value` | — | no | Currently selected value — matched against each child `Radio`'s `value` |
| `onChange` | `(value: string) => void` | — | no | Callback when selection changes |
| `isHorizontal` | `boolean` | `false` | no | Renders radios in a horizontal row instead of vertical stack |
| `name` | `string` | — | no | Shared `name` for all radio inputs in the group |

---

## Usage Pattern

`Radio` components are always used inside a `RadioGroup`. The group manages checked state by comparing its `value` prop against each child `Radio`'s `value` prop.

```tsx
import { Radio, RadioGroup } from '@8x8/oxygen-radio';
```
