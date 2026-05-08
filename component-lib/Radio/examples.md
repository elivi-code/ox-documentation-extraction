---
component: Radio
package: "@8x8/oxygen-radio"
category: form_inputs
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: extracted
pipeline_note: "Core files present; audit not yet run"
siblings:
  - "[[Radio/props]]"
  - "[[Radio/tokens]]"
  - "[[Radio/accessibility]]"
tags:
  - oxygen
  - component/Radio
  - role/examples
  - stage/extracted
  - category/form_inputs
---
# Radio — Examples

> **See also:** [Props](props.md) · [Tokens](tokens.md) · [Accessibility](accessibility.md)

## Import

```tsx
import { Radio, RadioGroup } from '@8x8/oxygen-radio';
```

---

## Basic vertical group

```tsx
const [selected, setSelected] = useState('option1');

<RadioGroup value={selected} onChange={(value: string) => setSelected(value)}>
  <Radio name="group1" label="Option 1" value="option1" testId="radio-1" />
  <Radio name="group1" label="Option 2" value="option2" testId="radio-2" />
  <Radio name="group1" label="Option 3" value="option3" testId="radio-3" />
</RadioGroup>
```

> Default layout is vertical. One option should always be preselected.

---

## Horizontal group

```tsx
<RadioGroup value={selected} onChange={setSelected} isHorizontal>
  <Radio name="group2" label="Yes" value="yes" testId="radio-yes" />
  <Radio name="group2" label="No" value="no" testId="radio-no" />
</RadioGroup>
```

> Use horizontal layout when space is limited and options are short.
> Gap between Radio Button items is **8px** (`$spacing(2)`).

---

## With disabled option

```tsx
<RadioGroup value={selected} onChange={setSelected}>
  <Radio name="group3" label="Available" value="available" testId="radio-avail" />
  <Radio name="group3" label="Unavailable" value="unavailable" testId="radio-unavail" isDisabled />
  <Radio name="group3" label="Coming soon" value="soon" testId="radio-soon" isDisabled />
</RadioGroup>
```

---

## With info tooltip

```tsx
<RadioGroup value={selected} onChange={setSelected}>
  <Radio
    name="group4"
    label="Standard plan"
    value="standard"
    testId="radio-standard"
  />
  <Radio
    name="group4"
    label="Enterprise plan"
    value="enterprise"
    testId="radio-enterprise"
    infoBoxText="Includes advanced features and dedicated support."
    infoBoxButtonLabel="More info about Enterprise plan"
  />
</RadioGroup>
```

> `infoBoxText` triggers an info icon (ⓘ) next to the label. Clicking it opens a Tooltip.
> `infoBoxButtonLabel` provides the accessible label for the info button.

---

## Full documentation story (from Storybook)

```tsx
export const RadioDocumentation = (args: typeof argsConfig) => {
  const [selected, setSelected] = useState(args.r0Value);

  return (
    <RadioGroup
      isHorizontal={args.isHorizontal}
      value={selected}
      onChange={(value: string) => setSelected(value)}
    >
      <Radio
        name="radio0"
        testId={args.r0TestId}
        isDisabled={args.r0IsDisabled}
        label={args.r0Label}
        value={args.r0Value}
      />
      <Radio
        name="radio1"
        testId={args.r1TestId}
        isDisabled={args.r1IsDisabled}
        label={args.r1Label}
        value={args.r1Value}
      />
      <Radio
        name="radio2"
        testId={args.r2TestId}
        isDisabled={args.r2IsDisabled}
        label={args.r2Label}
        value={args.r2Value}
      />
      <Radio
        name="radio3"
        testId={args.r3TestId}
        isDisabled={args.r3IsDisabled}
        label={args.r3Label}
        value={args.r3Value}
        infoBoxText={args.r3InfoBoxText}
        infoBoxButtonLabel={args.r3InfoBoxButtonLabel}
      />
    </RadioGroup>
  );
};
```

---

## Using RadioGroup with Slot component (form field pattern)

From Figma: when building a Radio Button group inside a form, use the **Slot** component to define the group container structure:

```
1. Header    — group label / title
2. Slot      — replace with RadioGroup of Radio items
3. Footer    — hint text
4. Error     — error message
```

Example with hint and error:

```tsx
<FormField label="Choose a plan" hint="Select the plan that fits your needs" error={errorMsg}>
  <RadioGroup value={selected} onChange={setSelected}>
    <Radio name="plan" label="Basic" value="basic" testId="radio-basic" />
    <Radio name="plan" label="Pro" value="pro" testId="radio-pro" />
    <Radio name="plan" label="Enterprise" value="enterprise" testId="radio-enterprise" />
  </RadioGroup>
</FormField>
```

---

## Radio Button Input (no label)

Use the `Radio` component without a label when the context makes the purpose clear (e.g., a cell in a table or an item in a list). Ensure the radio has an accessible name via a surrounding element or `aria-label`.

```tsx
<Radio name="select-row" value="row1" testId="radio-row1" label="" />
```

---

## Overflow / multiline label

When a label wraps to multiple lines, the radio input icon stays top-aligned with the first line of text.

```tsx
<Radio
  name="group5"
  label="Example Label with a very long text and tiny icons"
  value="long"
  testId="radio-long"
/>
```

_Source: Oxygen MCP + Figma (UI-components · nodes 51776:2800, 50606:93474) · Extracted 2026-04-29_
