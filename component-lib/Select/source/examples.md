---
component: Select
package: "@8x8/oxygen-select"
category: form_inputs
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Select/props]]"
  - "[[Select/tokens]]"
  - "[[Select/accessibility]]"
  - "[[Select/select-pui]]"
  - "[[Select/Select-audit]]"
tags:
  - oxygen
  - component/Select
  - role/examples
  - stage/blocked
  - category/form_inputs
---
# Select — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Basic usage

```tsx
import Select from '@8x8/oxygen-select';

const options = [
  { value: 'one', label: 'Option One' },
  { value: 'two', label: 'Option Two' },
  { value: 'three', label: 'Option Three' },
];

<Select options={options} />
```

## Multi-select with checkboxes

```tsx
<Select isMulti multipleSelectMaxRows={2} options={options} />
```

## Menu placement (auto)

Use `menuPlacement="auto"` to prevent the dropdown from clipping at screen edges. When near the bottom of the viewport the menu will open upwards instead.

```tsx
<Select options={options} menuPlacement="auto" />
```

## Programmatic focus (e.g. React Hook Forms validation)

```tsx
import { useRef } from 'react';
import Select from '@8x8/oxygen-select';
import { SelectInstance } from 'react-select';

const selectRef = useRef<SelectInstance>(null);

const handleFocusSelect = () => {
  if (selectRef.current) {
    selectRef.current.focus();
  }
};

<Select ref={selectRef} options={options} />
<Button onClick={handleFocusSelect}>Focus Select</Button>
```

## Select inside a Modal

`react-select` renders the menu through a portal when given an `HTMLElement` via `menuPortalTarget`. Use a callback-style ref to capture the modal element.

```tsx
import Select from '@8x8/oxygen-select';
import Button from '@8x8/oxygen-button';
import Modal, {
  ModalHeader,
  ModalContent,
  ModalFooter,
} from '@8x8/oxygen-modal';

const [modalOpen, setModalOpen] = useState<boolean>(false);
const [portalTarget, setPortalTarget] = useState<HTMLElement | null>(null);

<Button onClick={() => setModalOpen(true)}>Open Modal</Button>
{modalOpen && (
  <Modal portalRef={el => setPortalTarget(el)}>
    <ModalHeader title="Select in Modal" />
    <ModalContent>
      <Select
        options={[
          { value: 'One', label: 'Option One' },
          { value: 'Two', label: 'Option Two' },
          ...
          { value: 'Eight', label: 'Option Eight' },
        ]}
        menuPortalTarget={portalTarget}
      />
    </ModalContent>
    <ModalFooter>
      <Button onClick={() => setModalOpen(false)}>Close</Button>
    </ModalFooter>
  </Modal>
)}
```

## Virtual menu for large datasets (VirtualMenuList)

Use `VirtualMenuList` with `components` for datasets with 1000+ options to avoid performance issues. Uses `react-window` for virtualised rendering.

```tsx
import Select, { VirtualMenuList } from '@8x8/oxygen-select';

let i = 0;
const options10k = Array.from({ length: 10000 }, () => {
  i += 1;
  return {
    value: i,
    label: `Option ${i}`,
  };
});

<Select
  options={options10k}
  components={{
    MenuList: VirtualMenuList,
  }}
/>
```

### Virtual menu with grouped options

```tsx
import Select, { VirtualMenuList } from '@8x8/oxygen-select';

const groupedOptions = [
  {
    label: 'Group 1',
    options: [
      { value: '1_1', label: 'G 1 Option 1' },
      { value: '1_2', label: 'G 1 Option 2' },
    ],
  },
  // ...
];

<Select
  options={groupedOptions}
  components={{
    MenuList: VirtualMenuList,
  }}
/>
```

```tsx
// Without VirtualMenuList — slow with large datasets
<Select options={groupedOptions} />
```

## Error state

Use `hasError={true}` to render the red error border and set `aria-invalid="true"`. Pair with a visible error message below the field to satisfy WCAG 3.3.1.

```tsx
const errorId = 'plan-error';

<>
  <Select
    labelValue="Plan"
    options={options}
    hasError={!selectedValue}
    inputProps={{ 'aria-describedby': errorId }}
  />
  {!selectedValue && (
    <p id={errorId} role="alert" className="error-text">
      Select a plan before continuing.
    </p>
  )}
</>
```

## Disabled state

Use `isDisabled={true}` to prevent interaction. Note that React Hook Forms may programmatically focus a disabled Select on validation error — the `FocusableSelect` pattern (see the programmatic focus example above) handles this edge case.

```tsx
<Select
  labelValue="Plan"
  options={options}
  isDisabled
/>
```

## Async loading

Use `isAsync={true}` with a `loadOptions` function to fetch options remotely. `options` is not required when using async mode — provide `loadOptions` instead.

```tsx
const loadUsers = (inputValue, callback) => {
  fetch(`/api/users?q=${encodeURIComponent(inputValue)}`)
    .then((r) => r.json())
    .then((rows) =>
      callback(rows.map((u) => ({ value: u.id, label: u.name })))
    );
};

<Select
  labelValue="Assignee"
  isAsync
  loadOptions={loadUsers}
  loadingMessage="Loading users…"
  placeholder="Search by name"
/>
```

## Size variants

The `size` prop controls the input height. The default value `'default'` maps to the Figma label "Medium".

```tsx
<Select labelValue="Small (76 px)" options={options} size="small" />
<Select labelValue="Default / Medium (84 px)" options={options} size="default" />
<Select labelValue="Large (92 px)" options={options} size="large" />
```

## Usage guidance

### When to use
- When there are more than five options to choose from
- To allow a user to select one or multiple values from a list

### When not to use
- When there are fewer than five options — use Radio button (single) or Checkbox (multiple) instead

### Placement
- Typically used inside form elements
- Width defaults to fixed; can be made fluid to fill parent container width

_Source: Oxygen MCP · Extracted 2026-04-29_
