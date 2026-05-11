---
component: Radio
package: "@8x8/oxygen-radio"
category: form_inputs
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: extracted
pipeline_note: "Core files present; audit not yet run"
files_present:
  - props
  - examples
  - tokens
  - accessibility
siblings:
  - "[[Radio/examples]]"
  - "[[Radio/tokens]]"
  - "[[Radio/accessibility]]"
tags:
  - oxygen
  - component/Radio
  - role/props
  - stage/extracted
  - category/form_inputs
---
# Radio — Props

> **See also:** [Examples](examples.md) · [Tokens](tokens.md) · [Accessibility](accessibility.md)

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-radio

# npm
$ npm install @8x8/oxygen-radio
```

**Registry prerequisite** — add to `.npmrc` (project root):
```
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```
Or `.yarnrc.yml`:
```yaml
npmScopes:
  8x8:
    npmRegistryServer: "https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/"
nodeLinker: node-modules
```
> VPN connection to 8x8 is required to access the Artifactory registry.

---

## Package

`@8x8/oxygen-radio` · Category: **form** · Status: **Stable**

Exports two components: `Radio` and `RadioGroup`.

---

## `Radio` Props

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `testId` | `string` | `'RADIO'` | yes | Test ID for the radio input element |
| `label` | `node` | `''` | yes | Label content for the radio input |
| `value` | `number \| string \| bool \| { id: string }` | `''` | yes | Radio input value — matched against the parent `RadioGroup`'s selected value |
| `name` | `string` | — | yes | `name` attribute for the native radio input |
| `isChecked` | `bool` | `false` | yes | Whether the radio input is checked |
| `isDisabled` | `bool` | `false` | yes | Disabled state |
| `onChange` | `func` | `noop` | yes | Change callback |
| `infoBoxText` | `node` | — | yes | Renders an info icon that shows this text inside a Tooltip |
| `infoBoxButtonLabel` | `string` | — | yes | Accessible `aria-label` for the info button |

### `value` type detail

```ts
value: number | string | boolean | { id: string }
```

Used to match against the `RadioGroup`'s `value` prop to determine checked state.

---

## `RadioGroup` Props

`RadioGroup` is the container that manages selection state across a set of `Radio` children.

| Prop | Type | Default | Required | Description |
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

_Source: Oxygen MCP · Extracted 2026-04-29_
