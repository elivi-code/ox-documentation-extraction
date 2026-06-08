---
component: DateTimeSelector
package: "@8x8/oxygen-date-time-selector"
category: date_time
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: "YES"
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - figma
  - usage
  - audit
siblings:
  - "[[DateTimeSelector/examples]]"
  - "[[DateTimeSelector/tokens]]"
  - "[[DateTimeSelector/accessibility]]"
  - "[[DateTimeSelector/DateTimeSelector-figma]]"
  - "[[DateTimeSelector/DateTimeSelector-usage]]"
  - "[[DateTimeSelector/DateTimeSelector-audit]]"
tags:
  - oxygen
  - component/DateTimeSelector
  - role/props
  - stage/spec_ready
  - category/date_time
---

# DateTimeSelector — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```bash
npm install @8x8/oxygen-date-time-selector
```

```tsx
import { DateTimeSelector } from '@8x8/oxygen-date-time-selector';
```

---

## Props

| Prop | Type | Default | Required | Description |
|------|------|---------|:--------:|-------------|
| `closeOnDateChange` | `boolean` | `false` | No | Close the picker overlay when a date is selected |
| `finishButtonLabel` | `string` | — | No | Label text for the finish/confirm button |
| `isClearable` | `boolean` | `false` | No | Whether the component is clearable |
| `isLoading` | `boolean` | `false` | No | Whether the component is loading |
| `loadingMessage` | `string` | — | No | Message to display while loading |
| `onBlur` | `() => void` | — | No | Handler for blur event |
| `onDateChange` | `(date: Date) => void` | — | No | Handler for date change event |
| `onFocus` | `() => void` | — | No | Handler for focus event |
| `titleFormatPattern` | `string` | — | No | Format pattern for the title display (date-fns pattern) |
| `value` | `Date` | — | No | The currently selected date value |

---

## Notes

- `titleFormatPattern` follows [date-fns format tokens](https://date-fns.org/docs/format) (e.g. `"EEE, d MMM yyyy"`)
- `onDateChange` fires with a `Date` object representing the selected date/time
- `isLoading` + `loadingMessage` pair together — supply `loadingMessage` whenever `isLoading` is `true`

---

_Source: Oxygen MCP · Extracted 2026-05-08_
