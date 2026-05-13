---
component: Input
package: "@8x8/oxygen-input"
category: form_inputs
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - figma
  - pui
  - audit
siblings:
  - "[[Input/examples]]"
  - "[[Input/tokens]]"
  - "[[Input/accessibility]]"
  - "[[Input/Input-figma]]"
  - "[[Input/Input-pui]]"
  - "[[Input/Input-audit]]"
  - "[[Input/Input-usage]]"
tags:
  - oxygen
  - component/Input
  - role/props
  - stage/blocked
  - category/form_inputs
---
# Input — Props

> **See also:** [Input-figma.md](./Input-figma.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

---

## Installation

```bash
# yarn
yarn add @8x8/oxygen-input

# npm
npm install @8x8/oxygen-input
```

**Registry prerequisite** — configure `.npmrc` or `.yarnrc.yml` to point `@8x8` scope at the private Artifactory registry before installing:

```
# .npmrc
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```

> VPN connection to 8x8 network is required to access the registry.

---

## Import

```tsx
import { Input } from '@8x8/oxygen-input';
```

---

## Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `size` | `InputSize` | No | — | Size variant. See [InputSize](#inputsize) |
| `suffix` | `string` | No | — | Suffix text displayed at the end of the input |
| `iconLeft` | `React.ComponentType<IconProps>` | No | — | Icon component rendered to the left of the input text |
| `iconRight` | `React.ComponentType<IconProps>` | No | — | Icon component rendered to the right of the input text |
| `focus` | `boolean` | No | — | Programmatically force focused state |
| `fixed` | `boolean` | No | — | Fixed width mode |
| `hasError` | `boolean` | No | — | Puts the input in error state (red border + error styling) |
| `isDisabled` | `boolean` | No | — | Disables the input — no interaction, visually muted |
| `isReadOnly` | `boolean` | No | — | Makes input read-only — shows value but not editable |
| `isRequired` | `boolean` | No | — | Marks the field as required |
| `fullWidth` | `boolean` | No | — | Stretches the input to 100% of its container width |
| `inputRef` | `React.MutableRefObject<HTMLInputElement \| null> \| ((element: HTMLInputElement \| null) => void)` | No | — | Ref forwarded to the underlying `<input>` element |
| `testId` | `string` | No | — | `data-testid` attribute for automated testing |
| `autoSuffixWidth` | `boolean` | No | — | Automatically sizes the suffix width to content |
| `autoPrefixWidth` | `boolean` | No | — | Automatically sizes the prefix width to content |
| `inputProps` | `React.InputHTMLAttributes<HTMLInputElement>` | No | — | Spread-applied to the native `<input>` element. Use for `type`, `placeholder`, `aria-*`, `name`, `id`, etc. |

> `Input` also accepts all standard HTML input event handlers: `onChange`, `onKeyDown`, `onKeyUp`, etc.

---

## InputSize

```ts
type InputSize = 'small' | 'medium' | 'large';
```

Maps to Figma variant axis `Size`:

| OX value | Figma value | Height (text input) | Height (text area) |
|----------|-------------|---------------------|---------------------|
| `'small'` | Small | 76px | 90px |
| `'medium'` | Medium | 84px | 124px |
| `'large'` | Large | 92px | 156px |

---

## State mapping (Figma → OX API)

| Figma variant | OX prop | Notes |
|---------------|---------|-------|
| State=Disabled | `isDisabled={true}` | |
| Read Only=True | `isReadOnly={true}` | Not available on Search input in Figma |
| Error=True | `hasError={true}` | Pair with error message via `inputProps` or wrapper component |
| Filled=True | *(value prop)* | Controlled externally via `value` + `onChange` |

---

## Related components

- `TextField` (`@8x8/textField`) — higher-level form field wrapping Input with label, hint, and error message
- `DateTimeRangeSelector` (`@8x8/dateTimeRangeSelector`) — uses Input internally
- `Radio` (`@8x8/radio`) — uses `inputProps` pattern

---

_Source: Oxygen MCP · Extracted 2026-04-29_
