---
parent: "[[Radio]]"
section: composition
---

## Containment

`Radio` components are **always used inside** a `RadioGroup`. The group manages checked state by comparing its own `value` prop against each child `Radio`'s `value` prop.

```tsx
<RadioGroup value={selected} onChange={setSelected}>
  <Radio name="group" label="Option 1" value="option1" testId="radio-1" />
  <Radio name="group" label="Option 2" value="option2" testId="radio-2" />
</RadioGroup>
```

---

## Form field pattern (Slot / FormField)

When building a Radio group inside a form, wrap it in a `FormField` using the Slot pattern:

```
1. Header  — group label / title
2. Slot    — replace with RadioGroup of Radio items
3. Footer  — hint text
4. Error   — error message
```

```tsx
<FormField label="Choose a plan" hint="Select the plan that fits your needs" error={errorMsg}>
  <RadioGroup value={selected} onChange={setSelected}>
    <Radio name="plan" label="Basic"      value="basic"      testId="radio-basic" />
    <Radio name="plan" label="Pro"        value="pro"        testId="radio-pro" />
    <Radio name="plan" label="Enterprise" value="enterprise" testId="radio-enterprise" />
  </RadioGroup>
</FormField>
```

---

## Info tooltip composition

When `infoBoxText` is set on a `Radio`, an info icon button is rendered alongside the label. Clicking it opens a Tooltip with the provided text. The info button is a separate focus stop with its accessible name from `infoBoxButtonLabel`.

```tsx
<Radio
  name="plan"
  label="Enterprise plan"
  value="enterprise"
  testId="radio-enterprise"
  infoBoxText="Includes advanced features and dedicated support."
  infoBoxButtonLabel="More info about Enterprise plan"
/>
```

---

## Radio Button Input (no-label variant)

Use `Radio` without a label when context makes the purpose clear (e.g., table row selectors). Provide an accessible name via surrounding context or `aria-label`.

```tsx
<Radio name="select-row" value="row1" testId="radio-row1" label="" />
```

---

<!-- STUB:GAP-001 source="Run /figma-extract Radio against UI-components nodes 51776:2800 and 50606:93474 to capture Figma-sourced composition relationships (subcomponent nesting, pattern membership)." -->
