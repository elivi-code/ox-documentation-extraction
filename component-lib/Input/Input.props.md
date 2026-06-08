---
parent: "[[Input]]"
section: props
tags: [oxygen, component/Input, role/props]
---

## Props

<!-- STUB:GAP-002 source="Retrieve descriptions for size, suffix, focus, fixed, autoSuffixWidth, autoPrefixWidth from @8x8/oxygen-input README or source code" -->

| Name | Type | Default | Required | Description |
|---|---|---|---|---|
| `size` | `InputSize` | — | No | Size variant — `'small' \| 'medium' \| 'large'` (see InputSize). *No OX description returned — GAP-002* |
| `suffix` | `string` | — | No | Trailing text displayed at end of field. *No OX description — GAP-002* |
| `iconLeft` | `React.ComponentType<IconProps>` | — | No | Icon rendered left of input text |
| `iconRight` | `React.ComponentType<IconProps>` | — | No | Icon rendered right of input text |
| `focus` | `boolean` | `false` | No | Programmatically force focused state. *No OX description — GAP-002* |
| `fixed` | `boolean` | `false` | No | Fixed width mode. *No OX description — GAP-002* |
| `hasError` | `boolean` | `false` | No | Puts the input in error state (red border + error styling) |
| `isDisabled` | `boolean` | `false` | No | Disables the input — no interaction, visually muted |
| `isReadOnly` | `boolean` | `false` | No | Makes input read-only — shows value, not editable |
| `isRequired` | `boolean` | `false` | No | Marks the field as required |
| `fullWidth` | `boolean` | `false` | No | Stretches input to 100% of container width |
| `inputRef` | `React.MutableRefObject<HTMLInputElement \| null> \| ((el: HTMLInputElement \| null) => void)` | — | No | Ref forwarded to the underlying `<input>` element |
| `testId` | `string` | — | No | `data-testid` attribute for automated testing |
| `autoSuffixWidth` | `boolean` | `false` | No | Auto-sizes suffix container to content. *No OX description — GAP-002* |
| `autoPrefixWidth` | `boolean` | `false` | No | Auto-sizes prefix container to content. *No OX description — GAP-002* |
| `inputProps` | `React.InputHTMLAttributes<HTMLInputElement>` | — | No | Spread-applied to `<input>`. Use for `type`, `placeholder`, `aria-*`, `id`, `name`, `value`, `onChange` |

> `Input` also accepts standard HTML input event handlers: `onChange`, `onKeyDown`, `onKeyUp`, etc.

<!-- CONFLICT:CONFLICT-001 finding="isReadOnly: OX API exposes isReadOnly on Input globally but Figma Search input component set (node 25655:40530) has no Read Only variant axis — only Text input and Text area have it. Unclear if Search input intentionally omits read-only or Figma is incomplete." HUMAN DECISION REQUIRED -->

---

## InputSize

```ts
type InputSize = 'small' | 'medium' | 'large';
```

| OX value | Figma value | Text input height | Text area height |
|---|---|---|---|
| `'small'` | Small | 76 px | 90 px |
| `'medium'` | Medium | 84 px | 124 px |
| `'large'` | Large | 92 px | 156 px |

---

## State mapping (Figma → OX)

| Figma variant/axis | OX prop | Notes |
|---|---|---|
| State=Disabled | `isDisabled={true}` | — |
| Read Only=True | `isReadOnly={true}` | Not present on Search input Figma component set |
| Error=True | `hasError={true}` | Pair with error message via `inputProps` or wrapper |
| Filled=True | *(controlled via `inputProps.value` + `onChange`)* | No dedicated prop |

---

## Installation

```bash
yarn add @8x8/oxygen-input
# @8x8 scope requires Artifactory registry in .npmrc / .yarnrc.yml
```

```tsx
import { Input } from '@8x8/oxygen-input';
```
