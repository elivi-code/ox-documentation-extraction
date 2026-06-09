---
parent: "[[Tooltip]]"
section: tokens
---

## Design tokens

Token data synthesised from `Tooltip-figma.md` Color & token bindings (GAP-008 fix) and size constraints from `tokens.md`.

<!-- STUB:GAP-011 source="Token names (--ui/ui07, --text/textcolor04, --ui/shadow01) were extracted from Figma design context Tailwind output, not verified against the Variables API (Enterprise required). Verify against the UI-Foundations Figma library (fileKey: iVY5nI8JAxM05Apnnvozzs) using figma_execute + getVariableByIdAsync." -->
<!-- STUB:GAP-015 source="Figma Variables API requires Enterprise plan — figma_get_variables returned an error. Token names below are from design context output and may have drifted. Re-verify when Enterprise API is available." -->

---

## Color tokens

### Content container background

| Mode | Token | Collection | Resolved value |
|------|-------|------------|----------------|
| Light | `--ui/ui07` | UI | `#26252a` (dark gray) |
| Dark | `--ui/ui07` | UI | `#f1f1f1` (light gray) |

> Tooltip backgrounds are always inverted relative to the page mode — Light mode uses a dark tooltip, Dark mode uses a light tooltip. The same token resolves to opposite values per mode.

### Text

| Mode | Token | Collection | Resolved value |
|------|-------|------------|----------------|
| Light | `--text/textcolor04` | Text | `white` |
| Dark | `--text/textcolor04` | Text | `#292929` |

### Shadow / elevation

| Mode | Token | Collection | Resolved value |
|------|-------|------------|----------------|
| Light | `--ui/shadow01` | UI | `rgba(41, 41, 41, 0.25)` — `drop-shadow` filter |
| Dark | `--ui/shadow01` | UI | `#141414` — `box-shadow 0px 1px 2px 0px` |

<!-- STUB:GAP-012 source="Light mode uses CSS drop-shadow filter; Dark mode uses box-shadow. Both resolve to --ui/shadow01 but the CSS implementation differs. Confirm with design team whether this is intentional or a Figma artifact; align to a single implementation if it is an artifact." -->

---

## Typography tokens

| Element | Style name | Token | Value |
|---------|-----------|-------|-------|
| Tooltip text | `typography/body01` | `--typography/body01/font-size` | `14px` |
| Tooltip text | `typography/body01` | `--typography/body01/font-weight` | `400` |
| Tooltip text | `typography/body01` | `--typography/body01/line-height` | `20px` |
| Tooltip text | `typography/body01` | `--typography/body01/letter-spacing` | `-0.06px` |
| Tooltip text | `typography/body01` | `--typography/body01/font-family` | `'Inter:Regular', sans-serif` |

---

## Size constraints

| Property | Value | Source |
|----------|-------|--------|
| Min width | `40px` | Usage docs |
| Max width | `320px` (Top/Bottom) | Usage docs / Figma |
| Max width | `326px` (Left/Right) | Figma — `326px` observed for horizontal orientations |

> **WARN-002:** usage docs state `320px` universally; Figma shows `326px` for Left/Right orientations. The usage-docs value likely applies to Top/Bottom only. See audit WARN-002.

---

## Hardcoded spacing (no token bindings)

These values are hardcoded in Figma with no CSS variable binding.

<!-- STUB:GAP-010 source="Confirm with design team whether border-radius (6px), padding-x (8px), padding-y (4px), and max-width (320px/326px) should be tokenised. If yes, create tokens in the Figma library and update this table with token names." -->

| Property | Value | Notes |
|----------|-------|-------|
| `Content.border-radius` | `6px` | Should map to a `--radius/*` token |
| `Content.padding-x` | `8px` | No token binding found |
| `Content.padding-y` | `4px` | No token binding found |
| `Content.max-width` | `320px` / `326px` | Hardcoded px — no token binding |

---

## Behaviour constants (from usage docs)

| Property | Value |
|----------|-------|
| Default show delay | `300ms` (`delay` prop default — inferred) |
| Hide delay | None — hides immediately on cursor leave |
| Max content length | 140 characters (English) |

---

## Orientation × arrow interaction

| Prop | Effect on layout |
|------|-----------------|
| `orientation` | Controls which side the tooltip appears on relative to its trigger |
| `enableArrow` | Renders the `_Tip` directional pointer on the tooltip container |
| `offset` / `modifiers` | Fine-tune distance and alignment between trigger and tooltip |
