---
component: Toast
package: "@8x8/oxygen-toast"
category: feedback_status
role: examples
role_description: "Code examples — usage patterns from basic to advanced"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Toast/props]]"
  - "[[Toast/tokens]]"
  - "[[Toast/accessibility]]"
  - "[[Toast/Toast-figma]]"
  - "[[Toast/Toast-pui]]"
  - "[[Toast/Toast-audit]]"
tags:
  - oxygen
  - component/Toast
  - role/examples
  - stage/spec_ready
  - category/feedback_status
---
# Toast — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Basic Toast

```jsx
import { Toast } from '@8x8/oxygen-toast';

<Toast
  type="success"
  title="Action completed"
  description="Your changes have been saved."
  closeButtonLabel="Dismiss toast"
/>
```

## Toast Types

```jsx
import { Toast } from '@8x8/oxygen-toast';

<Toast type="success" title="Success" closeButtonLabel="Dismiss toast" />
<Toast type="error" title="Error" closeButtonLabel="Dismiss toast" />
<Toast type="warning" title="Warning" closeButtonLabel="Dismiss toast" />
<Toast type="info" title="Info" closeButtonLabel="Dismiss toast" />
<Toast type="loading" title="Loading…" closeButtonLabel="Dismiss toast" />
```

## Toast Sizes

```jsx
import { Toast } from '@8x8/oxygen-toast';

<Toast size="small" title="Small toast" closeButtonLabel="Dismiss toast" />
<Toast size="medium" title="Medium toast" closeButtonLabel="Dismiss toast" />
<Toast size="large" title="Large toast" closeButtonLabel="Dismiss toast" />
```

## With Actions

```jsx
import { Toast } from '@8x8/oxygen-toast';

<Toast
  type="info"
  title="File ready"
  description="Your export is ready to download."
  actions={[{ label: 'Download', onClick: () => handleDownload() }]}
  closeButtonLabel="Dismiss toast"
/>
```

## Hiding the Close Control

```jsx
import { Toast } from '@8x8/oxygen-toast';

<Toast
  type="loading"
  title="Processing…"
  hideCloseControl
/>
```

## Programmatic Toasts with Toaster

`Toaster` is a portal-based manager. Render `<Toaster />` once at the application root, then call `notify()` anywhere in your app:

```jsx
import { Button } from '@8x8/oxygen-button';
import Toaster, { notify } from '@8x8/oxygen-toaster';

// At app root
<Toaster />

// Trigger imperatively from anywhere
<Button
  onClick={() =>
    notify({
      content: 'The quick brown fox jumps over the lazy dog',
      iconTitle: 'Success',
      onClose: () => console.log('Toast closed'),
    })
  }
>
  Show toast
</Button>
```

## ToastStack

`ToastStack` groups multiple Toast components for manual stacking:

```jsx
import { Toast, ToastStack } from '@8x8/oxygen-toast';

<ToastStack>
  <Toast type="success" title="First notification" closeButtonLabel="Dismiss" />
  <Toast type="info" title="Second notification" closeButtonLabel="Dismiss" />
</ToastStack>
```

---

> **Note:** Clean code examples are not available from the MCP (only a documentation story wrapper was returned). The examples above are derived from the Storybook story code and Toaster usage patterns from the component info.

_Source: Oxygen MCP · Extracted 2026-05-05_
