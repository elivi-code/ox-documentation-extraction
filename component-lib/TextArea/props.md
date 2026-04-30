# Textarea — Props

> **See also:** [examples.md](./examples.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md) · [textarea-figma.md](./textarea-figma.md) · [textarea-pui.md](./textarea-pui.md)

---

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-textarea

# npm
$ npm install @8x8/oxygen-textarea
```

**Registry prerequisite:** Add to `.npmrc` (project root):
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
VPN connection to 8x8 network required.

---

## Import

```tsx
import { Textarea } from '@8x8/oxygen-textarea';
```

---

## Props

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `theme` | `Partial<Theme>` | _(from OX theme provider)_ | No | Theme object; default provided via `@8x8/oxygen-config` and `@8x8/oxygen-constants` |
| `ref` | `React.Ref<HTMLTextAreaElement>` | `null` | No | Ref forwarded to the underlying `<textarea>` DOM element |
| `id` | `string` | — | No | HTML `id` attribute for the textarea |
| `name` | `string` | — | No | HTML `name` attribute for the textarea |
| `placeholder` | `string` | — | No | Placeholder text content |
| `autoComplete` | `string` | `'off'` | No | HTML `autocomplete` attribute |
| `autoFocus` | `boolean` | `false` | No | HTML `autofocus` attribute |
| `value` | `string` | — | No | Controlled textarea value |
| `rows` | `number` | `3` | No | Number of visible text rows |
| `cols` | `number` | — | No | Number of visible text columns |
| `minLength` | `number` | — | No | Minimum character count |
| `maxLength` | `number` | — | No | Maximum character count |
| `resize` | `Resize` | `'vertical'` | No | CSS resize behaviour (see values below) |
| `testId` | `string` | `'TEXTAREA'` | No | `data-testid` attribute for automated tests |
| `isDisabled` | `boolean` | `false` | No | Disables the textarea |
| `isReadOnly` | `boolean` | `false` | No | Makes the textarea read-only |
| `hasError` | `boolean` | `false` | No | Applies error styling (red border) |
| `onBlur` | `React.FocusEventHandler<HTMLTextAreaElement>` | `noop` | No | Called when textarea loses focus |
| `onChange` | `React.ChangeEventHandler<HTMLTextAreaElement>` | `noop` | No | Called when textarea value changes |
| `onFocus` | `React.FocusEventHandler<HTMLTextAreaElement>` | `noop` | No | Called when textarea gains focus |
| `onKeyUp` | `React.KeyboardEventHandler<HTMLTextAreaElement>` | `noop` | No | Called on key-up |
| `onKeyDown` | `React.KeyboardEventHandler<HTMLTextAreaElement>` | `noop` | No | Called on key-down |

---

## `resize` values

| Value | Description |
|-------|-------------|
| `'auto'` | Browser determines resize capability |
| `'vertical'` | _(default)_ User can resize vertically only |
| `'horizontal'` | User can resize horizontally only |
| `'both'` | User can resize in both directions |
| `'none'` | Resize handle is not shown |
| `'block'` | Resize in the block direction (writing-mode dependent) |
| `'inline'` | Resize in the inline direction (writing-mode dependent) |

---

## Notes

- No props are marked as required; all have safe defaults.
- `hasError` toggles the error border (2px `--error/error01`) — error message display is handled at the form-field wrapper level, not inside this component.
- The `theme` prop follows the standard Oxygen theme override pattern; it is rarely needed when the Oxygen provider is set up globally.

---

_Source: Oxygen MCP · Extracted 2026-04-29_
