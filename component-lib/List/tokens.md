# List — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

## Theme tokens

Tokens are matched by searching for `"list"` in the Oxygen token registry. All tokens belong to both `light` and `dark` categories.

### Color tokens

| Token | Light value | Dark value | Palette reference (light) | Palette reference (dark) | Description |
|-------|------------|-----------|--------------------------|--------------------------|-------------|
| `active12` | `#DEDED5` | `#666666` | `colorPalette.offwhite085` | `colorPalette.gray05` | Background color for sidebar active state list items; active state for icon buttons |
| `hover12` | `#EBEAE1` | `#3D3D3D` | `colorPalette.offwhite09` | `colorPalette.gray03` | Hover background for sidebar menu main list items |
| `hover13` | `#EBEAE1` | `#525252` | `colorPalette.offwhite09` | `colorPalette.gray04` | Hover background for sidebar menu list items inside floating menu; icon button hover |
| `ui01` | `#EBEAE1` | `#666666` | `colorPalette.offwhite09` | `colorPalette.gray05` | Primary border for cards/dividers; tertiary background; selected state background for list items |
| `ui02` | `#F4F3EE` | `#3D3D3D` | `colorPalette.offwhite10` | `colorPalette.gray03` | Secondary background surface; subtle border for cards/dividers; hover state background for list items |

### Typography tokens

| Token | Value | Description |
|-------|-------|-------------|
| `bulletList01` | `{ fontFamily: "Inter, sans-serif", fontSize: "0.875rem", lineHeight: "1.5rem", fontWeight: 400, letterSpacing: "-0.006rem" }` | Typography set for bullet list items (shared between light and dark) |

---

> **Note:** These tokens are shared across the Oxygen token system and not exclusively owned by the List component. The `ListTheme` prop type (accepted by `<List theme={…} />`) wraps these into a component-scoped object provided by `@8x8/oxygen-config` and `@8x8/oxygen-constants` via the internal theme provider.

_Source: Oxygen MCP · Extracted 2026-05-08_
