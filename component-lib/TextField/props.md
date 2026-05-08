---
component: TextField
package: "@8x8/oxygen-textField"
category: form_inputs
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[TextField/examples]]"
  - "[[TextField/tokens]]"
  - "[[TextField/accessibility]]"
  - "[[TextField/figma]]"
  - "[[TextField/TextField-pui]]"
  - "[[TextField/TextField-audit]]"
tags:
  - oxygen
  - component/TextField
  - role/props
  - stage/spec_ready
  - category/form_inputs
---
# TextField — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [figma.md](figma.md)

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-text-field

# npm
$ npm install @8x8/oxygen-text-field
```

**Registry prerequisite** — add to `.npmrc` (or `.yarnrc.yml` for yarn):
```
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```
VPN connection required to access the private Artifactory registry.

## Import

```tsx
import { TextField } from '@8x8/oxygen-text-field';
```

## Props

| Prop | Type | Default | Description |
|------|------|---------|-------------|
| `inputRef` | `Ref` | — | Ref forwarded to the underlying `<input>` element |
| `id` | `string` | — | HTML `id` attribute on the input |
| `name` | `string` | — | HTML `name` attribute on the input |
| `placeholder` | `string` | — | Placeholder text shown when empty |
| `value` | `string` | — | Controlled input value |
| `label` | `string` | — | Label text displayed above (or beside) the input |
| `description` | `ReactNode` | — | Hint / helper text rendered below the input |
| `autoComplete` | `string` | — | HTML `autocomplete` attribute |
| `autoFocus` | `boolean` | `false` | Automatically focus the input on mount |
| `isDisabled` | `boolean` | `false` | Disables the input |
| `isReadOnly` | `boolean` | `false` | Makes the input read-only |
| `hasError` | `boolean` | `false` | Activates error visual state and shows error styling |
| `isRequired` | `boolean` | `false` | Marks the field as required (renders `*` beside label) |
| `maxLength` | `number` | — | Maximum number of characters allowed |
| `tabIndex` | `number` | — | HTML `tabindex` attribute |
| `labelOrientation` | `'row' \| 'column'` | `'column'` | Controls whether the label is placed above (`column`) or beside (`row`) the input |
| `fullWidth` | `boolean` | `false` | Input stretches to fill its container |
| `type` | `string` | `'text'` | HTML `type` attribute (e.g. `'email'`, `'password'`, `'number'`) |
| `size` | `'small' \| 'default' \| 'large'` | `'default'` | Visual size variant |
| `prefix` | `string` | — | Static text displayed inside the input before the value |
| `suffix` | `string` | — | Static text displayed inside the input after the value |
| `iconLeft` | `React.ComponentType<IconProps>` | — | Icon component rendered on the left inside the input |
| `iconRight` | `React.ComponentType<IconProps>` | — | Icon component rendered on the right inside the input |
| `focus` | `boolean` | — | Programmatically set focused state |
| `fixed` | `boolean` | — | Prevents input from collapsing when empty |
| `action` | `((event: React.MouseEvent) => void) \| string` | — | Inline action — pass a handler for a button or a URL string for a link |
| `actionLabel` | `string \| number` | — | Label text for the inline action |
| `actionTarget` | `ActionTarget` | — | Link target for when `action` is a URL string |
| `infoBoxText` | `ReactNode` | — | Content shown inside an info tooltip/box |
| `infoBoxButtonLabel` | `string` | — | Button label for the info box trigger |
| `inputProps` | `Partial<InputProps>` | — | Additional props spread onto the inner input element |
| `labelProps` | `Partial<LabelProps>` | — | Additional props spread onto the label element |
| `actionProps` | `Record<string, unknown>` | — | Additional props spread onto the action element |
| `otherInputProps` | `Partial<InputProps>` | — | Alternative pass-through for input props |
| `otherLabelProps` | `Partial<LabelProps>` | — | Alternative pass-through for label props |
| `otherActionProps` | `Record<string, unknown>` | — | Alternative pass-through for action props |
| `testId` | `string` | — | `data-testid` value for automated testing |
| `onChange` | `React.ChangeEventHandler<HTMLInputElement>` | — | Fires on every value change |
| `onBlur` | `React.FocusEventHandler<HTMLInputElement>` | — | Fires when the input loses focus |
| `onFocus` | `React.FocusEventHandler<HTMLInputElement>` | — | Fires when the input gains focus |
| `onKeyDown` | `React.KeyboardEventHandler<HTMLInputElement>` | — | Fires on key down |
| `onKeyUp` | `React.KeyboardEventHandler<HTMLInputElement>` | — | Fires on key up |

## Type references

```ts
type LabelOrientation = 'row' | 'column';

type ActionTarget = /* resolved from ActionTarget — likely '_blank' | '_self' | '_parent' | '_top' */;
```

_Source: Oxygen MCP · Extracted 2026-04-29_
