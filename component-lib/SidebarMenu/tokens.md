# SidebarMenu — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

## Theme tokens

The MCP returned 4 tokens with explicit sidebar references. All tokens have both light and dark mode values.

| Token | Role | Light value | Light palette ref | Dark value | Dark palette ref |
|---|---|---|---|---|---|
| `ui25` | Sidebar background | `#F4F3EE` | `offwhite10` | `#171719` | `purple01` |
| `hover12` | Main list item hover background | `#EBEAE1` | `offwhite09` | `#3D3D3D` | `gray03` |
| `active12` | Active item background (also icon button active) | `#DEDED5` | `offwhite085` | `#666666` | `gray05` |
| `hover13` | Floating sub-menu item hover background (also icon button hover) | `#EBEAE1` | `offwhite09` | `#525252` | `gray04` |

### Token descriptions

**`ui25`** — Background color for the sidebar menu shell, also used for the top bar and primary chat surface.

**`hover12`** — Hover background for the main sidebar list items (top-level `MenuItem`).

**`active12`** — Background color for the active state on sidebar list items and icon buttons that return to rest after activation.

**`hover13`** — Hover background for items inside the floating sub-menu panel (shown when the sidebar is collapsed), and for icon button hover states.

---

## Notes on token gaps

- No typography, spacing, or dimension tokens were returned by the MCP for this component. These are likely embedded in the component's internal styles rather than exposed as theme tokens.
- No border/shadow tokens were returned.
- The MCP search was scoped to `"sidebar"` — if additional tokens exist under other names (e.g. keyed to `menu`, `nav`), they would not appear in this list.

_Source: Oxygen MCP · Extracted 2026-05-07_
