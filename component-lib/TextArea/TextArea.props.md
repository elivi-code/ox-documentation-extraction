---
parent: "[[TextArea]]"
section: props
pipeline_stage: draft
audit_verdict: partial
tags:
  - oxygen
  - component/TextArea
  - section/props
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
| `aria-label` | `string` | — | No | Accessible name when no visible label is present |
| `aria-labelledby` | `string` | — | No | Space-separated ID(s) of external label element(s) |
| `aria-describedby` | `string` | — | No | Space-separated ID(s) of hint and/or error elements linked to this textarea |
| `aria-invalid` | `boolean \| "true" \| "false"` | — | No | Marks the field as invalid; set to `"true"` alongside `hasError={true}` |
| `aria-required` | `boolean \| "true" \| "false"` | — | No | Marks the field as required for assistive technology |
| `required` | `boolean` | `false` | No | HTML `required` attribute; announces the field as required to browsers and screen readers |

> The underlying `<textarea>` accepts all standard `HTMLTextAreaElement` attributes as pass-through props. Additional HTML attributes (e.g. `spellCheck`, `wrap`, `lang`) work without explicit typing.

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

> **Figma note:** The Figma design has a `Resize grip` boolean toggle that shows or hides a visual grip image in the bottom-right corner. This is a Figma-only design affordance and does **not** map to the `resize` prop. The `resize` prop controls CSS resize behaviour (whether the textarea box is user-resizable via the browser's drag handle), not grip visibility.

---

## Notes

- No props are marked as required; all have safe defaults.
- `hasError` toggles the error border (2px `--error/error01`). The Figma component includes an `Error Area` layer (error icon + error message text) in its visual anatomy, but **the Oxygen `Textarea` component does not render this Error Area**. Consumers must render error text externally and connect it via `aria-describedby`. See [[TextArea.accessibility]].
- Always pair `hasError={true}` with `aria-invalid="true"` so screen readers announce the invalid state.
- The `theme` prop follows the standard Oxygen theme override pattern; it is rarely needed when the Oxygen provider is set up globally.

<!-- CONFLICT:GAP-008 finding="Figma Mode variant axis (Light/Dark) has no 'mode' prop in Oxygen API — dark mode is almost certainly controlled at OxygenProvider theme-provider level, but this is not confirmed in the Oxygen source code" HUMAN DECISION REQUIRED -->

<!-- CONFLICT:GAP-007 finding="Figma Size variant axis (Large/Medium/Small) has no 'size' prop in Oxygen API — sizing is controlled via rows/cols; confirm with component owner whether size prop is planned or whether rows/cols is intentional" HUMAN DECISION REQUIRED -->

<!-- CONFLICT:GAP-009 finding="Figma Filled variant axis (False/True) has no Oxygen prop — likely a derived visual state when value !== '' but not confirmed from Oxygen source" HUMAN DECISION REQUIRED -->
