---
component: Select
package: "@8x8/oxygen-select"
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
  - pui
  - audit
siblings:
  - "[[Select/examples]]"
  - "[[Select/tokens]]"
  - "[[Select/accessibility]]"
  - "[[Select/select-pui]]"
  - "[[Select/Select-audit]]"
tags:
  - oxygen
  - component/Select
  - role/props
  - stage/blocked
  - category/form_inputs
---
# Select — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-select

# npm
$ npm install @8x8/oxygen-select
```

> **Registry prerequisite:** Add to `.npmrc`: `@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/`
> VPN connection to 8x8 network is required.

## Import

```tsx
import Select from '@8x8/oxygen-select';

// Named sub-component exports
import Select, {
  VirtualMenuList,
  ClearIndicator,
  DropdownIndicator,
  SingleValue,
  MultiValue,
  ValueContainer,
} from '@8x8/oxygen-select';
```

## Description

A select element used to select one or multiple options from a popover list. Built on top of [react-select](https://react-select.com/components) — all react-select props are supported via pass-through.

## Props

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `options` | `SelectOption[]` | `[]` | ✅ | List of options. Not required when `isAsync` is used — provide `loadOptions` instead |
| `action` | `(() => void) \| string` | `''` | — | Callback for onClick event on the action element |
| `actionLabel` | `string \| number` | `''` | — | Text rendered inside the action element |
| `components` | `object` | `{}` | — | Custom React components that override react-select internals. See [react-select docs](https://react-select.com/components) |
| `forwardedRef` | `React.Ref<any>` | `null` | — | Ref forwarded to the Select instance |
| `hasCheckbox` | `boolean` | `false` | — | Enables checkboxes in options (requires `isMulti`) |
| `hasError` | `boolean` | `false` | — | Puts the Select into error state |
| `hasIcons` | `boolean` | `false` | — | Enables icon rendering in options |
| `hasSelectableInput` | `boolean` | — | — | Renders a text input field when not `isMulti` |
| `hasShortMultiDisplay` | `boolean` | `false` | — | Displays multiple selections in compact/short mode. Only with `isMulti` |
| `hideSelectedOptions` | `boolean` | `false` | — | Removes selected options from the dropdown menu |
| `iconLeft` | `React.ComponentType \| React.ReactNode` | `null` | — | Icon rendered on the left side of the input field |
| `infoBoxText` | `string` | `'Dropdown info box'` | — | Text rendered inside the info Tooltip |
| `infoBoxButtonLabel` | `string` | — | — | Accessible `aria-label` for the info button |
| `isAsync` | `boolean` | `false` | — | Enables async data loading via `loadOptions`. See [react-select async](https://react-select.com/async) |
| `isClearable` | `boolean` | `true` | — | Renders the clear indicator (× button) |
| `isCreatable` | `boolean` | — | — | Allows creation of new options not in the list |
| `isDisabled` | `boolean` | `false` | — | Disables the Select |
| `isLoading` | `boolean` | `false` | — | Displays a loading spinner. See [react-select props](https://react-select.com/props) |
| `isMulti` | `boolean` | `false` | — | Allows multiple options to be selected |
| `isRequired` | `boolean` | `false` | — | Renders the required indicator (*) |
| `labelValue` | `string` | `'Dropdown label'` | — | Label text rendered above the select |
| `loadingMessage` | `string` | `'Loading...'` | — | Message shown while options are loading |
| `loadOptions` | `(inputValue: string, callback: Function) => void` | — | — | Async options loader. Used instead of `options` when `isAsync` is `true` |
| `multipleSelectMaxRows` | `number` | `1` | — | Max rows of chips before scrollbar appears. Only with `isMulti` |
| `noOptionsMessage` | `() => React.ReactNode` | `'No options...'` | — | Content rendered when no options match |
| `onBlur` | `() => void` | `noop` | — | Callback executed when the select loses focus / closes |
| `onChange` | `(value: any) => void` | `noop` | — | Callback executed when selection changes |
| `otherActionProps` | `object` | `{}` | — | Props passed to the `Action` component. Inherits `isDisabled` state |
| `placeholder` | `React.ReactNode` | `'Select...'` | — | Placeholder content shown when no value is selected |
| `shouldWrapLabel` | `boolean` | `false` | — | Allows label and action text to wrap to multiple lines |
| `size` | `'default' \| 'large' \| 'small'` | `'default'` | — | Size of the input box. `'default'` maps to Medium in Figma |
| `testId` | `string` | `'SELECT'` | — | `data-testid` DOM attribute value |
| `inputProps` | `React.InputHTMLAttributes<HTMLInputElement>` | `{}` | — | Props forwarded to the inner `<input>` element (e.g. `autoComplete`) |
| `theme` | `object` | — | — | Theme override. Default provided by Oxygen theme provider via `@8x8/oxygen-config` and `@8x8/oxygen-constants` |
| `menuPortalTarget` | `HTMLElement \| null` | `null` | — | Renders the dropdown menu through a React portal to the provided element. Required when using Select inside a Modal to prevent z-index and overflow clipping issues. |
| `menuPlacement` | `'auto' \| 'top' \| 'bottom'` | `'bottom'` | — | Controls where the dropdown menu opens relative to the input. `'auto'` switches to `'top'` when near the bottom of the viewport. |

## Sub-components

| Export | Description |
|--------|-------------|
| `Select` (default) | Main select component |
| `VirtualMenuList` | Virtualized menu list via `react-window` — use for large option datasets (1000+) |
| `ClearIndicator` | Customisable clear (×) button sub-component |
| `DropdownIndicator` | Customisable dropdown chevron sub-component |
| `SingleValue` | Customisable selected value display for single-select |
| `MultiValue` | Customisable chip display for multi-select |
| `ValueContainer` | Customisable container wrapping selected values |

## Figma Variants

| Property | Values |
|----------|--------|
| Mode | Light, Dark |
| Size | Large (92px height), Medium (84px height), Small (76px height) |
| State | Rest, Hover, Focus, Disabled, Read-only |
| Open | True, False |
| Error | True, False |

_Source: Oxygen MCP · Extracted 2026-04-29_
