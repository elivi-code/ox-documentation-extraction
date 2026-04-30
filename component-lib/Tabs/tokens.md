# Tabs — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md) · [Tabs-figma.md](Tabs-figma.md)

## MCP token search results

A search for `"tab"` in `get-theme-tokens` returned **no component-specific tab tokens** — only generic active-state tokens unrelated to the Tabs component.

<!-- No dedicated tab token namespace exists in the Oxygen theme token registry as of extraction date. -->

---

## Color variables observed in Figma variants

These variable bindings were observed directly on the `tabs` Figma component set (node `85651:78740`) and represent the actual design tokens applied per state:

| State | Property | Variable ID (partial) | Resolved value |
|-------|----------|----------------------|----------------|
| rest (unselected) | bottom border | `20136:253` | `#EBEAE1` — light offwhite gray |
| disabled | bottom border | `20136:324` | `#C8C7BD` — lighter muted gray |
| hover (unselected) | bottom border | `20136:265` | `#26253A` — near-black |
| selected / active | bottom border | `20136:286` | `#0057E0` — interactive blue |

> The selected state uses a **2px** bottom border; all other states use **1px**.

### Focus token

| Token | Value | Usage |
|-------|-------|-------|
| `$focus01` | `#0057E0` (2px solid blue) | Focus ring on tabs, disclosure button, and dropdown menu items |

---

## Spacing (from Figma layout)

| Element | Property | Value |
|---------|----------|-------|
| `tabs` (default tab) | Padding (all sides) | `16px` |
| `tabs` (default tab) | Height | `52px` (HUG) |
| `tabsDisclosure` | Padding (all sides) | `6px` |
| `tabsDisclosure` | Size | `52 × 52px` |

---

## No OX-registered tab-specific tokens

The Oxygen theme token search returned no entries scoped to the `tab` component namespace. The color values above are derived from Figma variable bindings and may correspond to shared semantic tokens (e.g. `border03`, `interactive01`) — the full token name resolution requires access to the Figma variable library.

---

_Source: Oxygen MCP + Figma (file `5YihJ5WuDvnvrlrRMC4sBp`) · Extracted 2026-04-30_
