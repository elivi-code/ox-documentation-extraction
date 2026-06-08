---
parent: "[[Input]]"
section: composition
tags: [oxygen, component/Input, role/composition]
---

## Subcomponents (Figma atoms)

The `Input` component is composed of shared sub-component atoms across all three Figma component sets:

| Atom | Role | Notes |
|---|---|---|
| `_base_form_label` | Optional label slot | Controlled by `Show Label`. Contains label text, required `*`, and help icon button |
| `Icon Button (faq)` | Help icon | `iconSizeM`, separate keyboard focus stop |
| `Input Text` / `Text Field` | Field container | `bg=ui05`, inner text/placeholder |
| `_base_form_hint` | Optional hint slot | Controlled by `Show Hint`. Helper/hint text below field |
| `KeywordSearch` icon | Search affordance | Search input only — leads the field container |

The help icon button (`Icon Button`, size M) is a separate focus stop and should carry its own accessible name.

---

## Wrapping component

`Input` renders the raw field only. Pair with `TextField` (`@8x8/textField`) for a complete form row with label, required indicator, help icon, and error message:

```tsx
import { Input } from '@8x8/oxygen-input';

// Minimal accessible pattern (Input only)
<label htmlFor="email">Email address</label>
<Input
  inputProps={{ id: 'email', name: 'email', type: 'email', 'aria-describedby': 'email-hint' }}
  isRequired
  onChange={handleChange}
/>
<p id="email-hint">We'll use this to send your receipt.</p>
```

---

## Related components

| Component | Relationship |
|---|---|
| [[TextField]] | Higher-level wrapper that composes `Input` with label, hint, and error slot |
| [[TextArea]] | Multi-line sibling — shares the Figma Input canvas (separate component set `21562:34985`) |
| [[Select]] | Use instead of `Input` when values come from a known finite set |
| [[Radio]] | Uses `inputProps` pattern; `Input` feeds raw values that radio groups then constrain |
| [[Checkbox]] | Alternative when user must pick from a discrete set |
| [[DateTimeSelector]] | Use instead of `Input` for date/time values |
| [[DateTimeRangeSelector]] | Uses `Input` internally |
| [[Slider]] | Use instead of `Input` for bounded numeric ranges |

---

## Pattern membership

| Pattern | Role of Input |
|---|---|
| [[Forms]] | Primary atom — most form rows are `label + Input + hint + optional error` |

---

## Code examples

<!-- STUB:GAP-003 source="Retrieve live Storybook examples from oxygen.8x8.com or @8x8/oxygen-input source; OX MCP returned 0 clean snippets — all examples below are hand-derived from prop API and Figma annotations" -->

### Basic

```tsx
import { Input } from '@8x8/oxygen-input';

<Input
  inputProps={{ id: 'my-field', name: 'myField', placeholder: 'Enter a value', 'aria-label': 'My field' }}
  onChange={(e) => console.log(e.target.value)}
/>
```

### Error state

```tsx
<Input
  hasError
  inputProps={{ 'aria-invalid': 'true', 'aria-describedby': 'field-error' }}
/>
<p id="field-error" role="alert">Please enter a valid value.</p>
```

### Search input

```tsx
import { SearchIcon } from '@8x8/oxygen-icons';

<label htmlFor="site-search">Search contacts</label>
<Input
  iconLeft={SearchIcon}
  inputProps={{ id: 'site-search', type: 'search' }}
  onChange={handleSearch}
/>
```

### With suffix

```tsx
<Input suffix="kg" autoSuffixWidth inputProps={{ type: 'number', placeholder: '0' }} />
```

### Form validation (real-time, on-blur)

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
