---
parent: "[[Checkbox]]"
section: composition
---

## Composition

### Subcomponents (rendered inside Checkbox)

| Component | Role |
|-----------|------|
| [[Tooltip]] | Hosts `infoBoxText` content, shown on info-button activation. |
| [[Icon]] | The info icon trigger rendered when `infoBoxText` is set. |

### Composition with CheckboxGroup

`CheckboxGroup` (named export, same package) wraps two or more related `Checkbox` items, providing
visual + structural grouping and the `isHorizontal` layout option. The `header` / `footer` slots
(Figma) host an optional group label and footer. See [[Checkbox.props]] for the group API (GAP-008).

### Related components

- [[Radio]] — mutually-exclusive selection (one of N). See [[Checkbox.usage]] Pair 1.
- [[ToggleButton]] — instant-effect on/off settings. See [[Checkbox.usage]] Pair 2.
- **Forms** — Checkbox is most often used inside the broader Forms pattern (label + control + error + help text).

### Code examples

> Derived from prop definitions and usage documentation — no verified Storybook source available
> (see GAP-006 below).

```jsx
// Single checkbox — binary option
import { Checkbox } from '@8x8/oxygen-checkbox';

<Checkbox id="terms" name="terms" label="I agree to the terms and conditions"
  value="terms" isChecked={isChecked} onChange={(e) => setIsChecked(e.target.checked)} />
```

```jsx
// With info tooltip
<Checkbox id="option-with-info" name="optionWithInfo" label="Enable feature" value="feature"
  isChecked={isChecked}
  infoBoxText="This feature enables advanced processing"
  infoBoxButtonLabel="More information about this feature"
  onChange={(e) => setIsChecked(e.target.checked)} />
```

```jsx
// Indeterminate parent ("select all")
<Checkbox id="select-all" name="selectAll" label="Select all" value="all"
  isChecked={allSelected} isIndeterminate={someSelected && !allSelected} onChange={handleSelectAll} />
```

```jsx
// Vertical group (default) and horizontal group
import { Checkbox, CheckboxGroup } from '@8x8/oxygen-checkbox';

<CheckboxGroup>
  <Checkbox id="opt1" name="options" label="Option 1" value="opt1" isChecked={a} onChange={onA} />
  <Checkbox id="opt2" name="options" label="Option 2" value="opt2" isChecked={b} onChange={onB} />
</CheckboxGroup>

<CheckboxGroup isHorizontal>
  <Checkbox id="a" name="group" label="A" value="a" isChecked={a} onChange={onA} />
  <Checkbox id="b" name="group" label="B" value="b" isChecked={b} onChange={onB} />
</CheckboxGroup>
```

<!-- STUB:GAP-006 source="Obtain clean examples from Storybook source (Checkbox.documentation.stories.tsx) or from Oxygen documentation site." -->
> **Examples are prop-derived (GAP-006).** The Oxygen MCP returned 0 clean Storybook snippets
> (`cleanExamples: true`). The only story is a `CheckboxDocumentation` wrapper. The examples above
> are derived from prop definitions, not verified Storybook source. The `ControlledCheckbox` wrapper
> pattern is mentioned in Storybook but not shown.

<!-- STUB:GAP-007 source="Add CheckboxGroup error state example using isError prop (verify prop name against CheckboxGroup API; see GAP-008)." -->
> **No error-state example (GAP-007).** A `CheckboxGroup` `isError` example is not provided because
> the `isError` prop is not yet confirmed in the API (depends on GAP-008). See [[Checkbox.accessibility]]
> for the inline-error a11y pattern that works against the current API surface.
