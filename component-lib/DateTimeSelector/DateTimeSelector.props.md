---
parent: "[[DateTimeSelector]]"
section: props
---

## Props

| Name | Type | Default | Required | Description | Accepts |
|---|---|---|---|---|---|
| `closeOnDateChange` | `boolean` | `false` | No | Close the picker overlay when a date is selected | — |
| `finishButtonLabel` | `string` | — | No | Label text for the finish/confirm button | — |
| `isClearable` | `boolean` | `false` | No | Whether the component is clearable | — |
| `isLoading` | `boolean` | `false` | No | Whether the component is loading | — |
| `loadingMessage` | `string` | — | No | Message to display while loading | — |
| `onBlur` | `() => void` | — | No | Handler for blur event | — |
| `onDateChange` | `(date: Date) => void` | — | No | Handler for date change event | — |
| `onFocus` | `() => void` | — | No | Handler for focus event | — |
| `titleFormatPattern` | `string` | — | No | Format pattern for the title display (date-fns pattern) | — |
| `value` | `Date` | — | No | The currently selected date value | — |

<!-- STUB:GAP-006 source="Verify inferred descriptions against @8x8/oxygen-date-time-selector source JSDoc or Storybook argTypes for: closeOnDateChange, finishButtonLabel, titleFormatPattern, value, loadingMessage" -->

## Notes

- `titleFormatPattern` follows [date-fns format tokens](https://date-fns.org/docs/format) (e.g. `"EEE, d MMM yyyy"`)
- `onDateChange` fires with a `Date` object representing the selected date/time
- `isLoading` + `loadingMessage` pair together — supply `loadingMessage` whenever `isLoading` is `true`
