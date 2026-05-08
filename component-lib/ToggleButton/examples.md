---
component: ToggleButton
package: "@8x8/oxygen-toggleButton"
category: form_inputs
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[ToggleButton/props]]"
  - "[[ToggleButton/tokens]]"
  - "[[ToggleButton/accessibility]]"
  - "[[ToggleButton/ToggleButton-figma]]"
  - "[[ToggleButton/ToggleButton-pui]]"
  - "[[ToggleButton/ToggleButton-audit]]"
tags:
  - oxygen
  - component/ToggleButton
  - role/examples
  - stage/blocked
  - category/form_inputs
---
# ToggleButton — Examples

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md) · [ToggleButton-figma.md](./ToggleButton-figma.md)

---

## Basic controlled toggle

```tsx
import { useState } from 'react';
import ToggleButton from '@8x8/oxygen-toggle-button';

function Example() {
  const [isChecked, setIsChecked] = useState(false);

  return (
    <ToggleButton
      label="Enable notifications"
      name="notifications"
      value="notifications"
      isChecked={isChecked}
      onChange={() => setIsChecked(prev => !prev)}
    />
  );
}
```

---

## Disabled state

```tsx
<ToggleButton
  label="Unavailable feature"
  name="feature"
  value="feature"
  isChecked={false}
  isDisabled
/>
```

---

## Indeterminate state

```tsx
<ToggleButton
  label="Mixed selection"
  name="selection"
  value="selection"
  isIndeterminate
/>
```

---

## With info tooltip

```tsx
<ToggleButton
  label="Advanced mode"
  name="advanced"
  value="advanced"
  isChecked={isChecked}
  onChange={handleChange}
  infoBoxText="Enabling this will expose additional configuration options."
  infoBoxButtonLabel="More information about advanced mode"
/>
```

---

## Toggle switch without label (Toggle Input)

Use the input-only variant when context makes the toggle's function obvious (e.g. inside a table cell or list item).

```tsx
{/* Toggle Input is the switch-only sub-component — 40×24px */}
{/* Available as the inner component within the ToggleButton package */}
<ToggleButton
  label={null}
  name="toggle-input"
  value="on"
  isChecked={isChecked}
  onChange={handleChange}
/>
```

> **Figma guidance:** When no label is needed, use the "Toggle Input" component variant (switch only). Ensure the toggle's purpose is clear from surrounding context.

---

## Multiple toggles (ToggleButtonGroup)

```tsx
import ToggleButton, { ToggleButtonGroup } from '@8x8/oxygen-toggle-button';

<ToggleButtonGroup>
  <ToggleButton label="Option A" name="group" value="a" isChecked={a} onChange={handleA} />
  <ToggleButton label="Option B" name="group" value="b" isChecked={b} onChange={handleB} />
  <ToggleButton label="Option C" name="group" value="c" isChecked={c} onChange={handleC} />
</ToggleButtonGroup>
```

> **Figma guidance:** Gap between stacked Toggle items is 8px (`$spacing03`).

---

## Horizontal group

```tsx
<ToggleButtonGroup isHorizontal>
  <ToggleButton label="Option A" name="group" value="a" isChecked={a} onChange={handleA} />
  <ToggleButton label="Option B" name="group" value="b" isChecked={b} onChange={handleB} />
</ToggleButtonGroup>
```

---

## Toggle + Icon Button (Figma pattern)

When an info icon button is placed beside a toggle as a separate interactive element:

```tsx
{/* Per Figma: place Icon Button to the RIGHT of Toggle, gap = 4px ($spacing02) */}
<div style={{ display: 'flex', alignItems: 'center', gap: '4px' }}>
  <ToggleButton label="Setting" name="setting" value="on" isChecked={isChecked} onChange={handleChange} />
  <IconButton aria-label="Learn more about this setting" icon={<InfoIcon />} size="iconSizeM" />
</div>
```

---

## Documentation story (from Storybook)

The only Storybook story available is the documentation story. No isolated clean snippets were returned by the MCP.

```tsx
// ToggleButton.documentation.stories.tsx
export const ToggleButtonDocumentation = ({ isControlled, ...args }) => {
  const [isChecked, setIsChecked] = useState(false);

  const handleOnChange = (value) => {
    setIsChecked(prev => !prev);
  };

  const passedDownProps = {
    ...args,
    ...(isControlled ? { isChecked, onChange: handleOnChange } : {}),
  };

  return <ToggleButton {...passedDownProps} />;
};
```

---

_Source: Oxygen MCP · Extracted 2026-04-29_
