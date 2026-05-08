# TimeSelector — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Basic usage

```tsx
import { TimeSelector } from "@8x8/oxygen-time-selector";
import { useState } from "react";

function BasicExample() {
  const [value, setValue] = useState({ hours: 16, minutes: 30, seconds: 0 });

  return (
    <TimeSelector
      value={value}
      onChange={setValue}
    />
  );
}
```

## With open/close callbacks

```tsx
<TimeSelector
  value={value}
  onChange={setValue}
  onOpen={() => console.log("Picker opened")}
  onClose={() => console.log("Picker closed")}
/>
```

## Small size

```tsx
<TimeSelector
  size="small"
  value={value}
  onChange={setValue}
/>
```

## With placeholder

```tsx
<TimeSelector
  placeholder="hh:mm AM"
  value={undefined}
  onChange={setValue}
/>
```

## Disabled state

```tsx
<TimeSelector
  isDisabled
  value={{ hours: 10, minutes: 30, seconds: 0 }}
  onChange={setValue}
/>
```

## Error state

```tsx
<TimeSelector
  hasError
  value={value}
  onChange={setValue}
/>
```

## With a left icon

```tsx
import { ClockIcon } from "@8x8/oxygen-icons";

<TimeSelector
  isLeftIconVisible
  iconLeft={ClockIcon}
  value={value}
  onChange={setValue}
/>
```

## Rendering into a portal

Use `portalRef` to control where the dropdown is rendered in the DOM — useful when the TimeSelector is inside a scrollable container or a dialog with `overflow: hidden`.

```tsx
const portalRef = useRef<HTMLDivElement>(null);

<div ref={portalRef} />
<TimeSelector
  portalRef={portalRef}
  value={value}
  onChange={setValue}
/>
```

---

> **Data note:** The OX MCP returned 0 clean code examples for this component. The examples above are reconstructed from the Storybook documentation story and Figma design context. Verify against the live Storybook at [oxygen.8x8.com/docs/components/timeselector/usage](https://oxygen.8x8.com/docs/components/timeselector/usage).

_Source: Oxygen MCP · Extracted 2026-05-07_
