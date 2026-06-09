---
parent: "[[List]]"
section: accessibility
pipeline_stage: draft
tags:
  - component/List
  - role/accessibility
---

## ARIA roles and semantics

| Element | Role / Tag | Notes |
|---------|-----------|-------|
| `<List>` (unordered) | `<ul>` with `role="list"` | Semantic list landmark |
| `<List isOrdered>` | `<ol>` | Ordered list semantics |
| `<List isGroup>` | Group-styled `<ul>` | Visually distinct group; semantics unchanged |
| `<ListItem>` | `<li>` | Child of the list container |

> **Note:** Explicit ARIA data was not returned by the Oxygen MCP. The above is inferred from the component's HTML list semantics. Verify against the rendered DOM in Storybook or a real implementation.

## Keyboard interaction

| Key | Behaviour |
|-----|-----------|
| `Tab` | Moves focus to the next focusable element. `ListItem` is focusable when `onClick` is provided. |
| `Enter` / `Space` | Triggers `onClick` when a `ListItem` is focused |

> Items without an `onClick` handler are not interactive and should not receive keyboard focus.

## Disabled state

- `ListItem isDisabled` items should be visually de-emphasised (via `opacity` or `color`).
- Disabled items with no `onClick` should not be reachable via `Tab`.
- If a disabled item must remain in the tab order for discoverability, use `aria-disabled="true"` and suppress the click handler rather than removing focus.

## Screen reader guidance

- `<List>` renders a semantic `<ul>` / `<ol>`; screen readers announce "list, N items" automatically.
- Use `ListItem title` to supply an accessible name when visible text is truncated (`shouldWrapText={false}`).
- Active items (`isActive`) convey state visually; add `aria-current="true"` (navigation lists) or `aria-selected="true"` (listbox-style selection) via a custom wrapper if the component does not handle this automatically.

## WCAG 2.1 AA checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.3.1 Info and Relationships | Verify | Semantic `<ul>`/`<ol>` structure should satisfy this |
| 1.4.3 Contrast (Minimum) | Verify | Token values (`ui01`, `ui02`) must meet 4.5:1 for text |
| 2.1.1 Keyboard | Verify | Clickable `ListItem` must be operable by keyboard |
| 2.4.3 Focus Order | Verify | Focus order must follow visual order in the list |
| 4.1.2 Name, Role, Value | Verify | Active/selected items need programmatic state (aria-current or aria-selected) |

<!-- STUB:GAP-003 source="Verify DOM output via Storybook or running application: confirm ARIA attributes emitted by isActive (aria-current? aria-selected?) and isDisabled (aria-disabled?), and confirm focus ring implementation (browser default vs custom outline); update ARIA table and WCAG checklist with verified findings" -->

_Source: Oxygen MCP (inferred — no explicit a11y data returned) · Extracted 2026-05-08_
