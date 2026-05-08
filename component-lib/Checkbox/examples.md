---
component: Checkbox
package: "@8x8/oxygen-checkbox"
category: form_inputs
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Checkbox/props]]"
  - "[[Checkbox/tokens]]"
  - "[[Checkbox/accessibility]]"
  - "[[Checkbox/checkbox-figma]]"
  - "[[Checkbox/checkbox-pui]]"
  - "[[Checkbox/checkbox-audit]]"
tags:
  - oxygen
  - component/Checkbox
  - role/examples
  - stage/spec_ready
  - category/form_inputs
---
# Checkbox — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

> **Data gap:** The Oxygen MCP returned 0 clean code snippets for Checkbox (`cleanExamples: true`).
> The only Storybook story available is a documentation wrapper (`CheckboxDocumentation`) — not a
> usage example. The patterns below are derived from the prop definitions and usage documentation
> returned by the MCP; no code was fabricated.

---

## Storybook entry point

The Storybook story is named `Documentation` and lives in:
`Checkbox.documentation.stories.tsx`

The story renders a `ControlledCheckbox` wrapper with args driven by `argsConfig` / `argTypesConfig`.
No standalone clean JSX snippet was returned by the MCP for this component.

---

## Usage patterns (from documentation content)

### Single checkbox — binary option

```jsx
import { Checkbox } from '@8x8/oxygen-checkbox';

<Checkbox
  id="terms"
  name="terms"
  label="I agree to the terms and conditions"
  value="terms"
  isChecked={isChecked}
  onChange={(e) => setIsChecked(e.target.checked)}
/>
```

### Checkbox with info tooltip

```jsx
<Checkbox
  id="option-with-info"
  name="optionWithInfo"
  label="Enable feature"
  value="feature"
  isChecked={isChecked}
  infoBoxText="This feature enables advanced processing"
  infoBoxButtonLabel="More information about this feature"
  onChange={(e) => setIsChecked(e.target.checked)}
/>
```

### Indeterminate state (parent checkbox in nested group)

```jsx
<Checkbox
  id="select-all"
  name="selectAll"
  label="Select all"
  value="all"
  isChecked={allSelected}
  isIndeterminate={someSelected && !allSelected}
  onChange={handleSelectAll}
/>
```

### Disabled checkbox

```jsx
<Checkbox
  id="locked-option"
  name="lockedOption"
  label="Locked option"
  value="locked"
  isChecked={true}
  isDisabled={true}
  onChange={() => {}}
/>
```

### Multiple checkboxes with group (vertical — default)

```jsx
import { Checkbox, CheckboxGroup } from '@8x8/oxygen-checkbox';

<CheckboxGroup>
  <Checkbox id="opt1" name="options" label="Option 1" value="opt1" isChecked={...} onChange={...} />
  <Checkbox id="opt2" name="options" label="Option 2" value="opt2" isChecked={...} onChange={...} />
  <Checkbox id="opt3" name="options" label="Option 3" value="opt3" isChecked={...} onChange={...} />
</CheckboxGroup>
```

### Horizontal group layout

```jsx
<CheckboxGroup isHorizontal>
  <Checkbox id="a" name="group" label="A" value="a" isChecked={...} onChange={...} />
  <Checkbox id="b" name="group" label="B" value="b" isChecked={...} onChange={...} />
</CheckboxGroup>
```

---

## Spacing notes (from documentation)

- Padding between group label and first checkbox: `$spacing04`
- Padding between checkbox labels in a vertical list: `$spacing03`

_Source: Oxygen MCP · Extracted 2026-04-29_
