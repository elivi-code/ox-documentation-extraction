---
component: TextField
package: "@8x8/oxygen-textField"
category: form_inputs
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[TextField/props]]"
  - "[[TextField/tokens]]"
  - "[[TextField/accessibility]]"
  - "[[TextField/figma]]"
  - "[[TextField/TextField-pui]]"
  - "[[TextField/TextField-audit]]"
tags:
  - oxygen
  - component/TextField
  - role/examples
  - stage/spec_ready
  - category/form_inputs
---
# TextField — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [figma.md](figma.md)

## Basic usage

```tsx
import { TextField } from '@8x8/oxygen-text-field';

<TextField
  label="Email"
  placeholder="Enter your email"
  onChange={(e) => setValue(e.target.value)}
/>
```

## With hint text

```tsx
<TextField
  label="Username"
  placeholder="Enter username"
  description="Must be 3–20 characters."
  onChange={(e) => setValue(e.target.value)}
/>
```

## Required field

```tsx
<TextField
  label="Full name"
  isRequired
  placeholder="First and last name"
  onChange={(e) => setValue(e.target.value)}
/>
```

## Error state

```tsx
<TextField
  label="Password"
  type="password"
  hasError
  description="Password must be at least 8 characters."
  onChange={(e) => setValue(e.target.value)}
/>
```

## Disabled

```tsx
<TextField
  label="Account ID"
  value="ACC-00123"
  isDisabled
/>
```

## Read-only

```tsx
<TextField
  label="Email"
  value="user@example.com"
  isReadOnly
/>
```

## Size variants

```tsx
<TextField label="Small" size="small" placeholder="Small input" />
<TextField label="Default" placeholder="Default input" />
<TextField label="Large" size="large" placeholder="Large input" />
```

## Full width

```tsx
<TextField
  label="Search"
  placeholder="Search..."
  fullWidth
  onChange={(e) => setValue(e.target.value)}
/>
```

## With icons

```tsx
import { SearchIcon } from '@8x8/oxygen-icons';

<TextField
  label="Search"
  iconLeft={SearchIcon}
  placeholder="Search..."
  onChange={(e) => setValue(e.target.value)}
/>
```

## With prefix / suffix

```tsx
<TextField
  label="Price"
  prefix="$"
  suffix="USD"
  placeholder="0.00"
  onChange={(e) => setValue(e.target.value)}
/>
```

## With inline action

```tsx
<TextField
  label="Referral code"
  value={code}
  action={() => copyToClipboard(code)}
  actionLabel="Copy"
  onChange={(e) => setCode(e.target.value)}
/>
```

## Horizontal label orientation

```tsx
<TextField
  label="Username"
  labelOrientation="row"
  placeholder="Enter username"
  onChange={(e) => setValue(e.target.value)}
/>
```

## Controlled with ref

```tsx
const inputRef = useRef<HTMLInputElement>(null);

<TextField
  label="Search"
  inputRef={inputRef}
  placeholder="Type to search"
  onChange={(e) => setValue(e.target.value)}
/>
```

## Storybook documentation story

> Raw story from Storybook — for reference only; wraps Doc/ComponentSection containers specific to Storybook.

```tsx
export const TextFieldDocumentation = (args: typeof argsConfig) => (
  <>
    <Doc markdown>{README}</Doc>
    <Doc markdown>{example}</Doc>
    <ComponentSection>
      <TextField
        {...args}
        onKeyUp={action('Input - onKeyUp event')}
        onChange={action('Input - onChange event')}
        onKeyDown={action('Input - onKeyDown event')}
      />
    </ComponentSection>
    <Doc markdown>{CHANGELOG}</Doc>
  </>
);

TextFieldDocumentation.storyName = 'Documentation';
TextFieldDocumentation.args = argsConfig;
TextFieldDocumentation.argTypes = argTypesConfig;
```

_Source: Oxygen MCP · Extracted 2026-04-29_
