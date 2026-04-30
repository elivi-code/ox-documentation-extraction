# Breadcrumbs — Tokens

> **See also:** [props.md](props.md) | [examples.md](examples.md) | [accessibility.md](accessibility.md)

## Theme tokens

`get-theme-tokens` returned no results for the query `"breadcrumb"`. No Oxygen theme tokens are currently mapped to this component in the MCP.

The `Breadcrumbs` component accepts a `theme` prop (type `object`) for direct theming, but its shape is not documented by the MCP.

## Known visual states

The following states are documented in the design but their token mappings are unresolved:

| State | Description |
|-------|-------------|
| Rest | Default appearance of a breadcrumb link |
| Hover | Visual feedback when the cursor is over a link |
| Active | The current page item (`isActive`), rendered as plain text |
| Focus | Keyboard-focus ring on a focusable breadcrumb link |

> **SOURCE_GAP:** Token definitions for breadcrumb link colours, separator colour, and focus ring are not exposed via the Oxygen MCP. Check the component's source stylesheet or raise with the Oxygen team.

_Source: Oxygen MCP · Extracted 2026-04-30_
