---
parent: "[[Checkbox]]"
section: platform
---

## Platform

<!-- NO RELEVANT PUI CONTEXT -->

No Platform UI requirements. Checkbox is a pure Oxygen design-system component with no
application-layer concerns — no notification, navigation, session, or event-bus integration. A PUI
MCP search for `checkbox` returned 0 matches (Platform UI is an infrastructure layer and contains no
UI component packages).

Selection state is owned by the consuming surface (`isChecked` + `onChange`); Checkbox holds no
platform-managed state of its own.
