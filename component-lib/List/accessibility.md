# List — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md)

## ARIA roles and semantics

| Element | Role / Tag | Notes |
|---------|-----------|-------|
| `<List>` (unordered) | `<ul>` with `role="list"` | Semantic list landmark |
| `<List isOrdered>` | `<ol>` | Ordered list semantics |
| `<List isGroup>` | Group-styled `<ul>` | Visually distinct group; semantics unchanged |
| `<ListItem>` | `<li>` | Child of the list container |

> **Note:** Explicit ARIA data was not returned by the Oxygen MCP. The above is inferred from the component's nature as a semantic HTML list structure. Verify against the rendered DOM in the Storybook or a real implementation.

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

- The `<List>` renders a semantic `<ul>` / `<ol>`, so screen readers will announce "list, N items" automatically.
- Use `ListItem title` to supply a tooltip-style accessible name when the visible text is truncated (`shouldWrapText={false}`).
- Active items (`isActive`) convey selection state visually; add `aria-current="true"` (e.g. for navigation lists) or `aria-selected="true"` (for listbox-style selection) via a custom wrapper if the component does not handle this automatically.

## WCAG 2.1 AA checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.3.1 Info and Relationships | Verify | Semantic `<ul>`/`<ol>` structure should satisfy this |
| 1.4.3 Contrast (Minimum) | Verify | Token values (`ui01`, `ui02`, `hover12`) must meet 4.5:1 for text |
| 2.1.1 Keyboard | Verify | Clickable `ListItem` must be operable by keyboard |
| 2.4.3 Focus Order | Verify | Focus order must follow visual order in the list |
| 4.1.2 Name, Role, Value | Verify | Active/selected items need programmatic state (aria-current or aria-selected) |

_Source: Oxygen MCP (inferred from component type — no explicit a11y data returned) · Extracted 2026-05-08_
