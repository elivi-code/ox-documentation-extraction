---
parent: "[[List]]"
section: tokens
pipeline_stage: draft
tags:
  - component/List
  - role/tokens
---

## Component tokens (Figma-confirmed)

All fill, text, and typography values are bound to variables — 100% token coverage confirmed via Desktop Bridge.

### Item background by state

Background token is identical for `selected?=true` and `selected?=false` at each state. Selection is communicated by trailing icon visibility only, not background colour.

| Element | rest | hover | active | focus | disabled |
|---------|------|-------|--------|-------|----------|
| Item bg token | `ui/ui06` | `ui/ui02` | `ui/ui01` | `ui/ui06` | `ui/ui06` |
| Light value | `#FFFFFF` | `#F4F3EE` | `#EBEAE1` | `#FFFFFF` | `#FFFFFF` |
| Light palette ref | `color/pure/white` | `color/offWhite/offWhite10` | `color/offWhite/offWhite09` | `color/pure/white` | `color/pure/white` |
| Dark value | `#171719` | `#3D3D3D` | `#666666` | `#171719` | `#171719` |
| Dark palette ref | `color/purple/purple01` | `color/gray/gray03` | `color/gray/gray05` | `color/purple/purple01` | `color/purple/purple01` |

<!-- GAP-001 RESOLVED 2026-06-08: ui01 = active/pressed state background. MCP registry description "selected state" is incorrect. Selection is icon-only; no background change occurs for selected?=true. -->

### Text and icon

| Element | Token | Light hex | Dark |
|---------|-------|-----------|------|
| Primary text (List Label) | `text/textColor01` | `#26252A` (`color/offWhite/offWhite02`) | Alias not resolved — see GAP-005 |
| Secondary text (Sub List Label) | `text/textColor02` | `#6C6862` (`color/offWhite/offWhite05`) | Alias not resolved — see GAP-005 |
| Leading icon fill | `icon/icon01` | `#26252A` | Shares alias chain with `textColor01` |
| Trailing selection icon | `icon/icon01` | `#26252A` | Same |

<!-- STUB:GAP-005 source="Run figma_execute with getVariableByIdAsync on dark-mode alias IDs for textColor01, textColor02, and icon01 to obtain resolved dark hex values; update this table" -->

### Typography

| Token | Value | Description |
|-------|-------|-------------|
| `bulletList01` | `{ fontFamily: "Inter, sans-serif", fontSize: "0.875rem", lineHeight: "1.5rem", fontWeight: 400, letterSpacing: "-0.006rem" }` | Typography set for bullet list items (shared between light and dark) |

---

## Spacing

Container padding (12 px left/right, 8 px top/bottom) and inter-child gap (8 px) are hardcoded in Figma with no variable binding.

<!-- STUB:GAP-006 source="Flag to Oxygen design team to tokenise container padding and gap values; document spacing tokens here once they exist" -->

---

## Related MCP tokens (SidebarMenu context — not owned by `@8x8/oxygen-list`)

Returned by Oxygen MCP token registry search for `"list"` but apply to `SidebarMenu` list items only:

| Token | Light value | Dark value | Actual context |
|-------|------------|-----------|----------------|
| `active12` | `#DEDED5` | `#666666` | SidebarMenu active-state list items; icon button active state |
| `hover12` | `#EBEAE1` | `#3D3D3D` | SidebarMenu main list item hover |
| `hover13` | `#EBEAE1` | `#525252` | SidebarMenu items inside floating menu; icon button hover |

_Source: Oxygen MCP · Figma MCP (Desktop Bridge) · Extracted 2026-05-08_
