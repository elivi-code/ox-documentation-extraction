---
component: Toast
parent: "[[Toast]]"
section: platform
role: spoke
pipeline_stage: spec_ready
audit_verdict: complete
siblings:
  - "[[Toast.props]]"
  - "[[Toast.anatomy]]"
  - "[[Toast.tokens]]"
  - "[[Toast.usage]]"
  - "[[Toast.accessibility]]"
  - "[[Toast.composition]]"
tags:
  - oxygen
  - component/Toast
  - role/spoke
  - stage/spec_ready
---

<!-- NO RELEVANT PUI CONTEXT -->

All Platform UI search candidates were reviewed and rejected by an engineer. The `Toast` / `Toaster` component manages its own notification queue via the `notify()` imperative API and does not depend on any PUI shell hooks, events, or MFE infrastructure.

## Candidates reviewed and rejected

| Path | Title | Score |
|------|-------|-------|
| `mfes/reusable-mfes/mfes/notifications.md` | Notifications | 2 |
| `mfes/hooks/use-notification.md` | Use Notification | 2 |
| `mfes/events/shell-notify.md` | Shell Notify | 1 |
| `mfes/communication.md` | Communication | 1 |
| `mfes/platform-ui-shell.md` | Platform UI Shell | 1 |

_Source: platform-ui-mcp · Extracted 2026-05-05_
