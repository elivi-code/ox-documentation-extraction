---
component: DateTimeSelector
package: "@8x8/oxygen-date-time-selector"
category: date_time
role: examples
role_description: "Code usage examples from basic to advanced patterns"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: "YES"
siblings:
  - "[[DateTimeSelector/props]]"
  - "[[DateTimeSelector/tokens]]"
  - "[[DateTimeSelector/accessibility]]"
  - "[[DateTimeSelector/DateTimeSelector-figma]]"
  - "[[DateTimeSelector/DateTimeSelector-usage]]"
  - "[[DateTimeSelector/DateTimeSelector-audit]]"
tags:
  - oxygen
  - component/DateTimeSelector
  - role/examples
  - stage/spec_ready
  - category/date_time
---

# DateTimeSelector — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

<!-- NOTE: Oxygen MCP returned 0 canonical Storybook examples for @8x8/oxygen-date-time-selector.
     Snippets below are inferred from prop documentation. -->

---

## Basic usage

```tsx
import { DateTimeSelector } from '@8x8/oxygen-date-time-selector';

function App() {
  const [date, setDate] = React.useState<Date | undefined>();

  return (
    <DateTimeSelector
      value={date}
      onDateChange={setDate}
    />
  );
}
```

---

## With finish button label

```tsx
<DateTimeSelector
  value={date}
  onDateChange={setDate}
  finishButtonLabel="Apply"
/>
```

---

## Close on date change

```tsx
<DateTimeSelector
  value={date}
  onDateChange={setDate}
  closeOnDateChange
/>
```

---

## Clearable

```tsx
<DateTimeSelector
  value={date}
  onDateChange={setDate}
  isClearable
/>
```

---

## Custom title format

```tsx
<DateTimeSelector
  value={date}
  onDateChange={setDate}
  titleFormatPattern="EEE, d MMM yyyy"
/>
```

---

## Loading state

```tsx
<DateTimeSelector
  value={date}
  onDateChange={setDate}
  isLoading
  loadingMessage="Fetching available slots…"
/>
```

---

## Focus and blur handlers

```tsx
<DateTimeSelector
  value={date}
  onDateChange={setDate}
  onFocus={() => console.log('focused')}
  onBlur={() => console.log('blurred')}
/>
```

---

_Source: Oxygen MCP · Extracted 2026-05-08_
