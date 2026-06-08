---
component: TextArea
package: "@8x8/oxygen-textarea"
category: form_inputs
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: rewrite
audit_verdict: partial
siblings:
  - "[[TextArea/props]]"
  - "[[TextArea/tokens]]"
  - "[[TextArea/accessibility]]"
  - "[[TextArea/textarea-figma]]"
  - "[[TextArea/textarea-pui]]"
  - "[[TextArea/textarea-audit]]"
tags:
  - oxygen
  - component/TextArea
  - role/examples
  - stage/rewrite
  - category/form_inputs
---
# Textarea — Examples

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md) · [textarea-figma.md](./textarea-figma.md) · [textarea-pui.md](./textarea-pui.md)

---

## Basic usage

```tsx
import { Textarea } from '@8x8/oxygen-textarea';

<Textarea
  placeholder="Enter your message"
  onChange={(e) => setValue(e.target.value)}
/>
```

---

## Controlled textarea

```tsx
import { useState } from 'react';
import { Textarea } from '@8x8/oxygen-textarea';

function Example() {
  const [value, setValue] = useState('');

  return (
    <Textarea
      value={value}
      placeholder="Type here..."
      onChange={(e) => setValue(e.target.value)}
    />
  );
}
```

---

## With character limit

```tsx
<Textarea
  value={value}
  maxLength={500}
  minLength={10}
  rows={4}
  onChange={(e) => setValue(e.target.value)}
/>
```

---

## Error state (accessible)

```tsx
import { useState } from 'react';
import { Textarea } from '@8x8/oxygen-textarea';

function ErrorExample() {
  const [value, setValue] = useState('');
  const hasError = value.length > 0 && value.length < 20;

  return (
    <>
      <label htmlFor="message">Message</label>
      <Textarea
        id="message"
        value={value}
        hasError={hasError}
        aria-invalid={hasError ? 'true' : undefined}
        aria-describedby={hasError ? 'message-error' : undefined}
        onChange={(e) => setValue(e.target.value)}
      />
      {hasError && (
        <span id="message-error" role="alert">
          Message must be at least 20 characters.
        </span>
      )}
    </>
  );
}
```

---

## Disabled state

```tsx
<Textarea
  value="Pre-filled content"
  isDisabled={true}
/>
```

---

## Read-only state

```tsx
<Textarea
  value="Read-only content that cannot be edited."
  isReadOnly={true}
/>
```

---

## Custom resize behaviour

```tsx
{/* No resize handle */}
<Textarea resize="none" />

{/* Both directions */}
<Textarea resize="both" />

{/* No resize (fixed height) */}
<Textarea resize="none" rows={6} />
```

---

## With ref forwarding

```tsx
import { useRef } from 'react';
import { Textarea } from '@8x8/oxygen-textarea';

function Example() {
  const ref = useRef<HTMLTextAreaElement>(null);

  return (
    <Textarea
      ref={ref}
      placeholder="Focusable textarea"
      onFocus={() => console.log('focused')}
    />
  );
}
```

---

## Event handlers

```tsx
<Textarea
  onFocus={() => console.log('focused')}
  onBlur={() => console.log('blurred')}
  onChange={(e) => console.log('changed:', e.target.value)}
  onKeyDown={(e) => {
    if (e.key === 'Escape') e.currentTarget.blur();
  }}
  onKeyUp={(e) => console.log('key up:', e.key)}
/>
```

---

## Notes on examples

- The Storybook documentation story wraps this component in Storybook's `Doc`, `ComponentSection`, and `ComponentItem` utilities — those are removed in the clean snippets above.
- No additional standalone Storybook examples were registered in the MCP at extraction time (total: 0 clean examples returned). The snippets above are derived from the props API and design context.

---

_Source: Oxygen MCP · Extracted 2026-04-29 · DOC_GAP fix applied (GAP-005 — accessible error pattern) 2026-06-05_
