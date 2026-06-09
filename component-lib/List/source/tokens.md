---
component: List
package: "@8x8/oxygen-list"
category: data_display
role: tokens
role_description: "Design token bindings — colors, spacing, typography per component state"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
siblings:
  - "[[List/props]]"
  - "[[List/examples]]"
  - "[[List/accessibility]]"
  - "[[List/List-figma]]"
  - "[[List/List-pui]]"
  - "[[List/List-audit]]"
tags:
  - oxygen
  - component/List
  - role/tokens
  - stage/blocked
  - category/data_display
---

# List — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

## Theme tokens

Tokens are matched by searching for `"list"` in the Oxygen token registry. All tokens belong to both `light` and `dark` categories.

### Color tokens — `@8x8/oxygen-list` (Figma-confirmed)

| Token | Light value | Dark value | Palette reference (light) | Palette reference (dark) | Description |
|-------|------------|-----------|--------------------------|--------------------------|-------------|
| `ui01` | `#EBEAE1` | `#666666` | `colorPalette.offwhite09` | `colorPalette.gray05` | Active/pressed state background for list items (pointer-down state; MCP description "selected state" is incorrect — confirmed by designer 2026-06-08) |
| `ui02` | `#F4F3EE` | `#3D3D3D` | `colorPalette.offwhite10` | `colorPalette.gray03` | Hover state background for list items |

### Color tokens — SidebarMenu context (returned by MCP "list" search — not owned by `@8x8/oxygen-list`)

The following tokens were returned by the Oxygen MCP token registry search for `"list"` but apply to `SidebarMenu` list items, not to the `List`/`ListItem` component: <!-- GAP-011 applied -->

| Token | Light value | Dark value | Palette reference (light) | Palette reference (dark) | Description |
|-------|------------|-----------|--------------------------|--------------------------|-------------|
| `active12` | `#DEDED5` | `#666666` | `colorPalette.offwhite085` | `colorPalette.gray05` | Background for **SidebarMenu** active-state list items; active state for icon buttons — not used by `@8x8/oxygen-list` |
| `hover12` | `#EBEAE1` | `#3D3D3D` | `colorPalette.offwhite09` | `colorPalette.gray03` | Hover background for **SidebarMenu** main list items — not used by `@8x8/oxygen-list` |
| `hover13` | `#EBEAE1` | `#525252` | `colorPalette.offwhite09` | `colorPalette.gray04` | Hover background for **SidebarMenu** items inside floating menu — not used by `@8x8/oxygen-list` |

### Typography tokens

| Token | Value | Description |
|-------|-------|-------------|
| `bulletList01` | `{ fontFamily: "Inter, sans-serif", fontSize: "0.875rem", lineHeight: "1.5rem", fontWeight: 400, letterSpacing: "-0.006rem" }` | Typography set for bullet list items (shared between light and dark) |

---

> **Note:** These tokens are shared across the Oxygen token system and not exclusively owned by the List component. The `ListTheme` prop type (accepted by `<List theme={…} />`) wraps these into a component-scoped object provided by `@8x8/oxygen-config` and `@8x8/oxygen-constants` via the internal theme provider.

_Source: Oxygen MCP · Extracted 2026-05-08_
