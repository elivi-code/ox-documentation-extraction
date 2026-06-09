---
parent: "[[Tooltip]]"
section: platform
---

<!-- NO RELEVANT PUI CONTEXT -->

## Platform UI context

No Platform UI infrastructure packages are relevant to the Tooltip component.

---

## Search summary

| Query | Results |
|-------|---------|
| `tooltip` | 0 |
| `overlay` | 1 (`pui-use-session-expired` — references `@8x8/oxygen-overlay`, unrelated to Tooltip) |
| `popover floating` | 0 |

Tooltip is a pure presentational component. It has no application-layer hooks, event bus usage, MFE dependencies, or session/navigation/notification concerns.

---

## Candidates rejected

| Package | Reason |
|---------|--------|
| `@8x8/pui-use-session-expired` | Matched "overlay" in README but references `@8x8/oxygen-overlay`, not Tooltip. Not relevant. |
