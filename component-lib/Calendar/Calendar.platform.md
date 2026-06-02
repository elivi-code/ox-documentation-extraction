---
parent: "[[Calendar]]"
section: platform
---

## Platform

<!-- NO RELEVANT PUI CONTEXT -->

No Platform UI requirements. Calendar is a presentational date-selection component with no application-layer concerns — no notification, navigation, session, or event-bus integration. A PUI MCP search confirmed zero results (no `Calendar-pui.md` source).

Selection state is owned by the consuming surface (`date` / `range` props + `onDateChange` / `onRangeChange` handlers); Calendar holds no platform-managed state of its own.
