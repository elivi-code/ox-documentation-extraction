---
parent: "[[Card]]"
section: anatomy
---

# Card — Anatomy

> ⚠️ **DEPRECATED** — `@8x8/oxygen-card` is deprecated. Anatomy preserved for reference.

Element structure extracted from the Figma layer tree (file `5YihJ5WuDvnvrlrRMC4sBp`, component set `18077:30676`). All 6 variants share the same internal child structure; exceptions noted per variant.

## Variant: Mode=Light/Dark, State=Rest & Hover

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | `Header` | structural | 320×22px; contains title text + icon button |
| 1a | text | `Widget Name` | content element | Controlled by `Add title` text property |
| 1b | instance | `dots-vertical` | optional slot | Controlled by `Show icon` boolean toggle |
| 2 | instance | `Slot` | optional slot | Content area; accepts any content; shown/hidden pattern not confirmed from API |
| 3 | instance | `_Cta` | optional slot | Call-to-action area; controlled by `Show actions` boolean toggle |

## Variant: Mode=Light/Dark, State=Focus

Identical to Rest/Hover plus one additional child:

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 4 | instance | `Focus ring` (`81045:233208`) | structural | Focus indicator overlay; present only in Focus state variants |

---

## Variant axes

| Property | Values | Default |
|----------|--------|---------|
| `Mode` | `Light`, `Dark` | `Light` |
| `State` | `Rest`, `Hover`, `Focus` | `Rest` |

### Boolean toggles

| Property | Default | Notes |
|----------|---------|-------|
| `Show actions` | `true` | Shows/hides the `_Cta` instance (call-to-action area) |
| `Show icon` | `true` | Shows/hides the `dots-vertical` icon in the Header frame |

### Text properties

| Property | Default | Notes |
|----------|---------|-------|
| `Add title` | `"Widget Name"` | Sets the text content of the `Widget Name` text node in Header |

### Instance swap slots

| Slot | Accepted types | Default node ID |
|------|---------------|-----------------|
| `Select Light icon` | COMPONENT_SET key `7e4d2d45750792f034ea1b8154c10fe106ce9573` | `84716:247786` |
| `Select Dark Icon` | COMPONENT_SET key `7e4d2d45750792f034ea1b8154c10fe106ce9573` | `84716:247790` |

> Both slots reference the same icon component set. Separate slots allow different icon choices per mode.

### Persistent states

All three State variants (Rest, Hover, Focus) are transient interaction states. No disabled, selected, loading, or error states exist in the component set.

---

## Interaction states

| State | Trigger | Visual change |
|-------|---------|---------------|
| `Rest` | Default / pointer not over | Background: `#FFFFFF` (Light) / `#171719` (Dark); border: `ui01` |
| `Hover` | Pointer over card | Background changes to `#F4F3EE` (Light / `ui02`); border unchanged |
| `Focus` | Keyboard focus | Background same as Rest; `Focus ring` instance added as overlay |

---

## Structure & spacing

### Container

| Property | Token | Value | Variant |
|----------|-------|-------|---------|
| Width | — | `352px` | All variants |
| Height | — | `226px` | All variants |
| Border | `20136:253` (`ui01`) | `1px solid #EBEAE1` (Light) / `#666666` (Dark) | All states |

### Header frame

| Property | Token | Value | Notes |
|----------|-------|-------|-------|
| Width | — | `320px` | 16px inset from card left edge |
| Height | — | `22px` | — |

<!-- STUB:GAP-007 source="With Figma Desktop open on the Card component set, call get_design_context (fileKey 5YihJ5WuDvnvrlrRMC4sBp, nodeId 18080:28136 — Light/Rest variant) to retrieve padding, gap, and auto-layout data. Update the Structure & spacing section." -->
> **SOURCE_GAP (GAP-007)** — Padding (horizontal/vertical), gap between child elements, and auto-layout direction for the Card container were not returned by the REST API. The `get_design_context` call failed because no node was selected in Figma Desktop at extraction time. Card (352×226) and Header (320×22) dimensions are captured, but internal spacing is unknown.

### Density / size variants

No size/density axis — the component set only varies Mode and State.

---

## Design decisions & annotations

<!-- STUB:GAP-010 source="With Desktop Bridge running, call figma_get_component (nodeId 18077:30676) — the enriched REST API warning will resolve and the description field will populate. Update this section." -->
> **SOURCE_GAP (GAP-010)** — The component description could not be retrieved (known Figma REST API bug where description fields are missing from responses). The Desktop Bridge plugin provides reliable description data; it was not running during extraction.
