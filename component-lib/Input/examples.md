---
component: Input
package: "@8x8/oxygen-input"
category: form_inputs
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Input/props]]"
  - "[[Input/tokens]]"
  - "[[Input/accessibility]]"
  - "[[Input/Input-figma]]"
  - "[[Input/Input-pui]]"
  - "[[Input/Input-audit]]"
tags:
  - oxygen
  - component/Input
  - role/examples
  - stage/blocked
  - category/form_inputs
---
# Input — Examples

> **See also:** [Input-figma.md](./Input-figma.md) · [props.md](./props.md) ·
> [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md)

---

## Basic usage

```tsx
import { Input } from '@8x8/oxygen-input';

<Input
  inputProps={{
    id: 'my-field',
    name: 'myField',
    placeholder: 'Enter a value',
    'aria-label': 'My field',
  }}
  onChange={(e) => console.log(e.target.value)}
/>
```

---

## With label and helper text (recommended pattern)

The `Input` component renders the raw input field only. Wrap with `TextField` for a complete form field with label, required indicator, help icon, and error message:

```tsx
import { Input } from '@8x8/oxygen-input';

// Using inputProps for accessibility attributes
<Input
  inputProps={{
    id: 'email',
    name: 'email',
    type: 'email',
    'aria-describedby': 'email-hint',
    'aria-required': 'true',
  }}
  isRequired
  onChange={handleChange}
/>
<p id="email-hint">Enter your work email address.</p>
```

---

## Sizes

```tsx
<Input size="small" inputProps={{ placeholder: 'Small' }} />
<Input size="medium" inputProps={{ placeholder: 'Medium' }} />
<Input size="large" inputProps={{ placeholder: 'Large' }} />
```

---

## States

### Error state

```tsx
<Input
  hasError
  inputProps={{
    'aria-invalid': 'true',
    'aria-describedby': 'email-error',
  }}
/>
<p id="email-error" role="alert">Please enter a valid email address.</p>
```

### Disabled

```tsx
<Input isDisabled inputProps={{ placeholder: 'Cannot edit' }} />
```

### Read-only

```tsx
<Input
  isReadOnly
  inputProps={{ value: 'Read only content', readOnly: true }}
/>
```

### Required

```tsx
<Input
  isRequired
  inputProps={{
    'aria-required': 'true',
    id: 'required-field',
    name: 'requiredField',
  }}
/>
```

---

## Full width

```tsx
<Input
  fullWidth
  inputProps={{ placeholder: 'Fills container width' }}
/>
```

---

## With icons

```tsx
import { SearchIcon } from '@8x8/oxygen-icons';

// Left icon (e.g. search)
<Input
  iconLeft={SearchIcon}
  inputProps={{ placeholder: 'Search...', type: 'search' }}
/>

// Right icon (e.g. clear / password reveal)
<Input
  iconRight={ClearIcon}
  inputProps={{ placeholder: 'Type here...' }}
/>
```

---

## With suffix

```tsx
<Input
  suffix="kg"
  autoSuffixWidth
  inputProps={{ type: 'number', placeholder: '0' }}
/>
```

---

## With ref

```tsx
import { useRef } from 'react';

const inputRef = useRef<HTMLInputElement>(null);

<Input
  inputRef={inputRef}
  inputProps={{ id: 'my-input' }}
/>
```

---

## Form validation pattern (from Figma examples page)

Figma documents two validation strategies for forms using Input:

### Real-time (on-blur) validation

```tsx
<Input
  hasError={hasError}
  inputProps={{
    onBlur: validateField,
    'aria-invalid': hasError ? 'true' : 'false',
    'aria-describedby': hasError ? 'field-error' : 'field-hint',
  }}
/>
{hasError
  ? <p id="field-error" role="alert">Invalid value</p>
  : <p id="field-hint">Helper text</p>
}
```

### Submit-time validation

Validate all fields on form submit. Show both:
1. Inline error states on affected `Input` fields (`hasError`)
2. Summary error component at the bottom of the form listing all issues

---

## hasPlaceholder accessibility pattern

```tsx
// ❌ Old pattern — placeholder as only label (not accessible)
<Input
  inputProps={{ placeholder: 'Enter your email' }}
/>

// ✅ New pattern — label + helper text, no placeholder
// Set hasPlaceholder={false} in Figma designs
<label htmlFor="email">Email address</label>
<Input
  inputProps={{
    id: 'email',
    type: 'email',
    'aria-describedby': 'email-hint',
  }}
/>
<p id="email-hint">We'll use this to send your receipt.</p>
```

> **From Figma:** "For all new designs and prototypes, we highly recommend setting `hasPlaceholder` to false and using a proper label and helper text combination."

---

> **Note:** The OX MCP returned 0 clean Storybook examples for this component. Examples above are derived from the prop API, Figma annotations, and Figma accessibility examples page (node `65777:2179`).

---

_Source: Oxygen MCP · Figma annotations · Extracted 2026-04-29_
