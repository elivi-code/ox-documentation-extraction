---
component: Toast
package: "@8x8/oxygen-toast"
category: feedback_status
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Toast/examples]]"
  - "[[Toast/tokens]]"
  - "[[Toast/accessibility]]"
  - "[[Toast/Toast-figma]]"
  - "[[Toast/Toast-pui]]"
  - "[[Toast/Toast-audit]]"
tags:
  - oxygen
  - component/Toast
  - role/props
  - stage/spec_ready
  - category/feedback_status
---
# Toast — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```bash
# yarn
$ yarn add @8x8/oxygen-toast

# npm
$ npm install @8x8/oxygen-toast
```

> **Registry prerequisite:** Add `@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/` to `.npmrc`. Requires 8x8 VPN access.

## Package exports

The `@8x8/oxygen-toast` package exports:

- `Toast` — individual toast notification
- `ToastStack` — container for stacking multiple toasts
- `InlineNotification` — inline (non-floating) notification variant

A companion package `@8x8/oxygen-toaster` exports:

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

No props exposed via MCP. `Toaster` is a portal-based manager; use the `notify()` imperative API to trigger toasts. Install separately via `@8x8/oxygen-toaster`.

---

## `InlineNotification`

No props available from MCP. Part of the `@8x8/oxygen-toast` package; represents the inline (non-floating) notification variant.

---

_Source: Oxygen MCP · Extracted 2026-05-05_
