---
component: Label
package: "@8x8/oxygen-label"
category: data_display
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Label/props]]"
  - "[[Label/tokens]]"
  - "[[Label/accessibility]]"
  - "[[Label/Label-figma]]"
  - "[[Label/label-pui]]"
  - "[[Label/label-usage]]"
  - "[[Label/label-audit]]"
tags:
  - oxygen
  - component/Label
  - role/examples
  - stage/blocked
  - category/data_display
---
# Label — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [label-usage.md](label-usage.md)

## Basic label

```tsx
import Label from '@8x8/oxygen-label';
import Input from '@8x8/oxygen-input';

<Label value="Email address" htmlFor="email-input" />
<Input id="email-input" />
```

## Required field

```tsx
<Label value="Password" htmlFor="password-input" isRequired />
<Input id="password-input" type="password" />
```

## Disabled state

```tsx
<Label value="Username" htmlFor="username-input" isDisabled />
<Input id="username-input" isDisabled />
```

## With inline action link

```tsx
<Label
  value="Password"
  htmlFor="password-input"
  actionLabel="Forgot password?"
  action={() => console.log('action clicked')}
/>
<Input id="password-input" type="password" />
```

## With action link and `actionTarget`

> **Note (GAP-002):** `action` is typed as `ActionProps['action']` — the underlying signature is not yet documented. Verify against Storybook for the exact type before production use.

```tsx
<Label
  value="Documentation"
  htmlFor="doc-input"
  actionLabel="View guide"
  action={() => console.log('action clicked')}
  actionTarget="_blank"
/>
<Input id="doc-input" />
```

## With forwarded action props (`otherActionProps`)

`otherActionProps` accepts any `Record<string, unknown>` and forwards entries to the action element. Common use cases: `data-*` attributes, `rel`, or `aria-*` attributes not covered by the component's own props.

```tsx
<Label
  value="Password"
  htmlFor="password-input"
  actionLabel="Forgot password?"
  action={() => console.log('action clicked')}
  otherActionProps={{ 'data-analytics': 'forgot-password-link', rel: 'noopener' }}
/>
<Input id="password-input" type="password" />
```

## With info box

```tsx
<Label
  value="API Key"
  htmlFor="api-key-input"
  infoBoxText="Your API key can be found in your account settings."
  infoBoxButtonLabel="More information about API key"
/>
<Input id="api-key-input" />
```

## Text overflow tooltip

```tsx
<Label
  value="A very long label that might overflow its container"
  htmlFor="my-input"
  showTooltipOnOverflow
/>
<Input id="my-input" />
```

## Wrapped text

```tsx
<Label
  value="A label with longer text that needs to wrap across multiple lines"
  htmlFor="my-input"
  shouldWrapText
/>
<Input id="my-input" />
```

> **Note:** The MCP returned no clean Storybook snippets for this component. Examples above are derived from the documentation story and prop shapes. Verify against Storybook before production use.

_Source: Oxygen MCP · Extracted 2026-05-01_
