---
component: Toast
parent: "[[Toast]]"
section: composition
role: spoke
pipeline_stage: spec_ready
audit_verdict: partial
siblings:
  - "[[Toast.props]]"
  - "[[Toast.anatomy]]"
  - "[[Toast.tokens]]"
  - "[[Toast.usage]]"
  - "[[Toast.accessibility]]"
  - "[[Toast.platform]]"
tags:
  - oxygen
  - component/Toast
  - role/spoke
  - stage/spec_ready
---

<!-- source: figma-only -->

## Package ecosystem

The Toast notification system spans two packages with three primary exports and a companion manager:

| Export | Package | Role |
|--------|---------|------|
| `Toast` | `@8x8/oxygen-toast` | Individual notification unit — renders a single toast with icon, title, description, actions, and close button |
| `ToastStack` | `@8x8/oxygen-toast` | Manual stacking container — wraps multiple `Toast` children for layout control |
| `InlineNotification` | `@8x8/oxygen-toast` | Inline (non-floating) notification — embedded in layout, non-inverted theme |
| `Toaster` | `@8x8/oxygen-toaster` | Portal-based manager — renders a floating stack; use with `notify()` for imperative dispatch |
| `notify()` | `@8x8/oxygen-toaster` | Imperative API to trigger a toast from anywhere in the tree without prop drilling |
| `DURATION` | `@8x8/oxygen-toaster` | Constant for standard display durations |

---

## Containment relationships

```
Toaster (portal, manages queue)
  └── Toast (each queued notification)
       ├── icon (status icon)
       ├── title (text)
       ├── description (optional text)
       ├── cta (optional action links)
       └── Icon Button (close button)

ToastStack (manual layout container)
  └── Toast × N (stacked children)
```

- **`Toaster` contains `Toast`** — automatically manages stacking, grouping (Group collapsed / Group expanded), and queue ordering. Stacking is handled by the Toaster system; there is no `style` prop on `Toast` itself.
- **`ToastStack` contains `Toast`** — for cases where the consumer controls stacking manually without the Toaster queue.
- **`Toast` is the composable unit** — it can be used standalone without either container.

---

## Related components

| Component | Relationship | When to choose |
|-----------|-------------|----------------|
| `[[AlertBanner]]` | Peer — persistent page-level feedback surface | Session expiry, outages, conditions that persist across navigation |
| `[[Modal]]` | Peer — blocking feedback surface | Decisions that require acknowledgement before proceeding |
| `[[Spinner]]` | Peer — inline indeterminate progress | In-context loading states next to a specific trigger |
| `[[ProgressBar]]` | Peer — inline determinate progress | Long-running operations where the user needs progress visibility |
| `[[Tag]]` | Peer — static status indicator | Status embedded in a list row or card without urgency |

---

## Pattern membership

Toast appears in these application-level patterns:

- **Action confirmation** — file save, message sent, copy-to-clipboard: emit a `type="success"` toast via `notify()` on operation completion.
- **Background job feedback** — show `type="loading"` while the job runs, then replace with `type="success"` or `type="error"` on resolution.
- **Non-blocking error reporting** — surface `type="error"` toasts for recoverable failures that don't block the current flow.

---

## Figma component relationships

The Figma "Notification" page (node `1823:0`) contains three component sets:

| Component set | Node | Domain |
|---------------|------|--------|
| Notification | `26764:41883` | Maps to `@8x8/oxygen-toast` `Toast` |
| InlineNotification | `5549:4130` | Maps to `@8x8/oxygen-toast` `InlineNotification` |
| Interaction | `9141:14534` | Separate domain — incoming calls, meetings, messages. Not mapped to `@8x8/oxygen-toast` |

> **WARN-002:** The relationship between the Interaction component set and `@8x8/oxygen-toast` / `@8x8/oxygen-toaster` is assumed to be none. Confirm with engineering that the Interaction component set has no connection to these packages.
