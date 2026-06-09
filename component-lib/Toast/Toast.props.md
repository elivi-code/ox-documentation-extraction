---
component: Toast
parent: "[[Toast]]"
section: props
role: spoke
pipeline_stage: spec_ready
audit_verdict: partial
siblings:
  - "[[Toast.anatomy]]"
  - "[[Toast.tokens]]"
  - "[[Toast.usage]]"
  - "[[Toast.accessibility]]"
  - "[[Toast.platform]]"
  - "[[Toast.composition]]"
tags:
  - oxygen
  - component/Toast
  - role/spoke
  - stage/spec_ready
---

## Installation

```bash
$ yarn add @8x8/oxygen-toast
# or
$ npm install @8x8/oxygen-toast
```

> **Registry prerequisite:** Add `@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/` to `.npmrc`. Requires 8x8 VPN access.

## Package exports

The `@8x8/oxygen-toast` package exports:
- `Toast` — individual toast notification
- `ToastStack` — container for stacking multiple toasts
- `InlineNotification` — inline (non-floating) notification variant

Companion package `@8x8/oxygen-toaster`:
- `Toaster` — portal-based toast manager; pairs with the `notify()` helper
- `DURATION` — constant for toast display durations

---

## `Toast` props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `title` | `ReactNode` | No | — | Toast title content |
| `description` | `ReactNode` | No | — | Toast body content |
| `children` | `ReactNode` | No | — | Component content |
| `actions` | `Array<ActionType>` | No | — | Action buttons rendered in the toast |
| `type` | `ToastType` | No | — | Visual variant (see values below) |
| `size` | `ToastSize` | No | — | Size variant (see values below) |
| `hideCloseControl` | `boolean` | No | — | When `true`, hides the dismiss button |
| `onCloseControlClick` | `() => void` | No | — | Callback fired when the dismiss button is clicked |
| `isToast` | `boolean` | No | — | Whether the component is rendered as a floating toast vs. inline alert |
| `iconTitle` | `string` | No | — | Accessible label for the status icon |
| `closeButtonLabel` | `string` | No | — | Accessible label for the close button |

<!-- STUB:GAP-006 source="Populate Default column from @8x8/oxygen-toast component source or Storybook controls panel — not available via MCP" -->

### `ActionType` shape

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `label` | `string` | Yes | Button label text |
| `onClick` | `() => void` | Yes | Click handler |

_Shape derived from examples (`{ label: 'Download', onClick: () => handleDownload() }`). Confirm field names against @8x8/oxygen-toast source if additional fields are suspected._

### `ToastType` values

`"success"` · `"error"` · `"warning"` · `"info"` · `"loading"`

### `ToastSize` values

`"small"` · `"medium"` · `"large"`

---

## `ToastStack` props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `children` | `ReactNode` | **Yes** | — | Toast items to stack |

---

## `Toaster` props

No props exposed via MCP. `Toaster` is a portal-based manager; use the `notify()` imperative API. Install separately via `@8x8/oxygen-toaster`.

### `notify()` signature

```tsx
notify({
  content: string,       // toast body text (confirmed param name — not title/description)
  iconTitle?: string,    // accessible label for status icon
  onClose?: () => void,  // callback on dismissal
})
```

---

## `InlineNotification` props

<!-- SKIP:GAP-004 manual="InlineNotification props not returned by MCP — extract from @8x8/oxygen-toast component source or Storybook. Figma confirms Mode (Light/Dark) and Type (Success, Info, Error, Warning, Loading) variant axes plus a Title text prop." -->

No props available from MCP. Figma extraction confirms variant axes `Mode` (Light/Dark) and `Type` (Success, Info, Error, Warning, Loading) and a `Title` text prop. Code prop names and defaults require upstream source access.

<!-- STUB:GAP-007 source="Add an InlineNotification code example once GAP-004 (props) is resolved and prop names are confirmed" -->

---

## Code examples

### Basic Toast

```jsx
import { Toast } from '@8x8/oxygen-toast';

<Toast
  type="success"
  title="Action completed"
  description="Your changes have been saved."
  closeButtonLabel="Dismiss toast"
/>
```

### Toast types

```jsx
<Toast type="success" title="Success" closeButtonLabel="Dismiss toast" />
<Toast type="error" title="Error" closeButtonLabel="Dismiss toast" />
<Toast type="warning" title="Warning" closeButtonLabel="Dismiss toast" />
<Toast type="info" title="Info" closeButtonLabel="Dismiss toast" />
<Toast type="loading" title="Loading…" closeButtonLabel="Dismiss toast" />
```

### Toast sizes

```jsx
<Toast size="small" title="Small toast" closeButtonLabel="Dismiss toast" />
<Toast size="medium" title="Medium toast" closeButtonLabel="Dismiss toast" />
<Toast size="large" title="Large toast" closeButtonLabel="Dismiss toast" />
```

### With actions

```jsx
<Toast
  type="info"
  title="File ready"
  description="Your export is ready to download."
  actions={[{ label: 'Download', onClick: () => handleDownload() }]}
  closeButtonLabel="Dismiss toast"
/>
```

### Hiding the close control

```jsx
<Toast
  type="loading"
  title="Processing…"
  hideCloseControl
/>
```

### Programmatic toasts with `Toaster`

```jsx
import Toaster, { notify } from '@8x8/oxygen-toaster';

// At app root — render once
<Toaster />

// Trigger from anywhere in the tree
notify({
  content: 'The quick brown fox jumps over the lazy dog',
  iconTitle: 'Success',
  onClose: () => console.log('Toast closed'),
})
```

### `ToastStack` — manual stacking

```jsx
import { Toast, ToastStack } from '@8x8/oxygen-toast';

<ToastStack>
  <Toast type="success" title="First notification" closeButtonLabel="Dismiss" />
  <Toast type="info" title="Second notification" closeButtonLabel="Dismiss" />
</ToastStack>
```
