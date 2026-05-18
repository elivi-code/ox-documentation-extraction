---
component: Button
package: "@8x8/oxygen-button"
category: interaction
role: figma
role_description: "Figma design spec — anatomy, variant axes, token bindings, and spacing extracted from Figma"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Button/props]]"
  - "[[Button/examples]]"
  - "[[Button/tokens]]"
  - "[[Button/accessibility]]"
  - "[[Button/Button-usage]]"
  - "[[Button/Button-audit]]"
tags:
  - oxygen
  - component/Button
  - role/figma
  - stage/blocked
  - category/interaction
---
<!-- SOURCE: Figma MCP + figma-console MCP -->
<!-- FILE KEY: 5YihJ5WuDvnvrlrRMC4sBp -->
<!-- NODE ID: 78258:1843 (examples page) · 15653:16329 (Label Button component set) -->
<!-- EXTRACTED: 2026-04-28 -->
<!-- COMPONENT: Button -->
<!-- COLOR STRATEGY: B (states as columns, variants as rows — 5 variants × 4 states > 3 threshold) -->

# Button — Figma Design Spec

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md) · [Button-usage.md](./Button-usage.md)

---

## Visual reference

![Button examples page — Button Color Tokens Reference and Icon Button Toggle](figma-screenshot-button.png)

*Page "↳ Button examples" — node 78258:1843. Left section: Button Color Tokens Reference. Right section: Icon button toggle usage.*

---

## Anatomy

Element structure extracted from the Label Button component set (`15653:16329`).
Hidden elements represent boolean-toggled optional slots.

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Container | Structural | Auto-layout horizontal; padding 16px H / 12px V; border-radius 6px; bg token applied here |
| 2 | instance | Swap Icon L | Optional slot | Controlled by `Icon L` boolean toggle (default: hidden). Instance-swap accepts any icon component. |
| 3 | text | Label | Content element | Default text "Button"; uses `$bodyBold02` text style (16px, semi-bold, Inter) |
| 4 | instance | Swap Icon R | Optional slot | Controlled by `Icon R` boolean toggle (default: hidden). Instance-swap accepts any icon component. |

### Sub-component: Icon Button Toggle

Separate component documented in the "Icon button toggle" section of the examples page.
States observed: Rest-Unselected, Hover-Unselected, Rest-Selected, Hover-Selected,
Active-Selected, Focus-Unselected, Focus-Selected, Disabled-Unselected, Disabled-Selected.
Shown in both Light and Dark mode.

---

## API — Component properties

### Variant axes

| Property | Values | Default |
|----------|--------|---------|
| `Mode` | `Light`, `Dark` | `Light` |
| `Type` | `Primary`, `Secondary`, `Text` | `Primary` |
| `Size` | `Large`, `Medium`, `Small` | `Large` |
| `State` | `Rest`, `Hover`, `Active`, `Focus`, `Disabled` | `Rest` |
| `Danger` | `False`, `True` | `False` |
| `Fluid 100%` | `False`, `True` | `False` |
| `isInverted` | `no`, `yes` | `no` |

> **Note:** Figma `Type` covers only Primary/Secondary/Text. The Oxygen API variants
> `tertiary`, `tertiaryReversed`, `success`, `destructive` likely live in separate
> Figma component sets (e.g. Circular/Control Button) not captured at this node.
> `Danger=True` maps to Oxygen's `isDestructive` prop.
> `Fluid 100%=True` maps to a full-width layout — no corresponding prop documented in
> props.md for Button (present in DropdownButton only — potential props gap, see Gaps).

### Boolean toggles

| Property | Default | Notes |
|----------|---------|-------|
| `Icon L` | `false` | Shows/hides the left icon slot (`Swap Icon L`) |
| `Icon R` | `false` | Shows/hides the right icon slot (`Swap Icon R`) |

### Instance swap slots

| Slot | Accepted types | Default node ID |
|------|---------------|-----------------|
| `Swap Icon L` | Any icon component | `81045:146348` |
| `Swap Icon R` | Any icon component | `81045:146348` |

### Persistent states

| State | Property name | Notes |
|-------|--------------|-------|
| Disabled | `State=Disabled` | Visually distinct; maps to `isDestructive=false` + `isDisabled=true` in Oxygen API |

### Token coverage

- **Coverage:** Token coverage % not returned — Figma file does not use Figma Variables
  (variable API returned empty). Tokens are referenced by name in text annotations on the
  examples page only.
- **CSS variable naming discrepancy flagged:**
  - Design context emits `var(--actions/action09, #0056e0)` for Primary bg
  - tokens.md names this token `action01` (same hex `#0056E0` Light)
  - The CSS path format `actions/action09` does not match the semantic token name `action01`
  — possible dual naming convention between Figma CSS export and Oxygen token system.

---

## Color & token bindings

<!-- COLOR STRATEGY B: variants as rows, states as columns -->

Token names sourced from text annotations in the "Button Color Tokens Reference"
section of the examples page (node 78525:3716). Format: `$bgToken / $textToken`.

### Label Button — Background token

| Variant | Rest | Hover | Active | Disabled |
|---------|------|-------|--------|----------|
| Primary | `action01` | `hover15` | `active14` | `disabled01` |
| Secondary | `action01` ⚠️ | `hover16` | `active15` | `disabled01` |
| Danger (Primary+Danger) | `action03` | `hover17` | `active16` | `disabled01` |
| Text Primary | — (transparent) | `hover18` | `active17` ⚠️ | — (transparent) |
| Text Danger | — (transparent) | `hover19` | `active17` ⚠️ | — (transparent) |

> ⚠️ **Secondary Rest:** Figma shows `$action01` — conflicts with tokens.md which specifies `action02`. Likely a copy-paste error in the Figma reference page. See Gaps.
>
> ⚠️ **Text active:** Both Text Primary and Text Danger active show `$active17`. tokens.md defines `active17` as "Inverted primary button active" — unexpected for non-inverted text buttons. See Gaps.

### Label Button — Text token

| Variant | Rest | Hover | Active | Disabled |
|---------|------|-------|--------|----------|
| Primary | `textColor09` | `textColor09` | `textColor09` | `disabled04` |
| Secondary | `textColor09` | `textColor09` | `textColor09` | `disabled04` |
| Danger (Primary+Danger) | `textColor09` | `textColor09` | `textColor09` | `disabled04` |
| Text Primary | `action01` | `hover15` | `active14` | `disabled04` |
| Text Danger | `action03` | `hover17` | `active14` | `disabled04` |

### Disabled-state tokens (new — answers GAP-011)

| Token | Description from Figma annotations |
|-------|-------------------------------------|
| `disabled01` | Disabled button background (all solid variants) |
| `disabled04` | Disabled button text / icon color (all variants) |

> These tokens appear across all variant disabled states in the Figma reference.
> They are absent from tokens.md — this file is the first documentation of them.

### Text styles

| Element | Style name | Size | Weight | Line height | Letter spacing |
|---------|-----------|------|--------|-------------|----------------|
| Label | `$bodyBold02` | `var(--typography/bodyBold02/font-size, 16px)` | 600 (semi-bold) | `var(--typography/bodyBold02/line-height, 24px)` | `var(--typography/bodyBold02/letter-spacing, 0.0121px)` |

### Effect styles

<!-- NO EFFECT STYLES FOUND IN FIGMA RESPONSE -->

---

## Structure & spacing

### Container (Label Button, Large size)

| Property | Token | Value | Variant |
|----------|-------|-------|---------|
| Height | — | `48px` (inferred: 12+24+12) | Large |
| Height | — | <!-- NOT FOUND IN FIGMA RESPONSE --> | Medium |
| Height | — | <!-- NOT FOUND IN FIGMA RESPONSE --> | Small |
| Padding horizontal | — | `16px` | All sizes (Large confirmed) |
| Padding vertical | — | `12px` | Large |
| Border radius | — | `6px` | All variants |

### Internal spacing

| Property | Token | Value | Notes |
|----------|-------|-------|-------|
| Gap (icon–label) | — | `8px` | Between icon slots and label |
| Icon size | — | `24×24px` | Both left and right icon slots |

### Auto-layout

- Direction: **horizontal**
- Alignment: center (both axes — `justify-center`, `items-center`)
- `Fluid 100%=True` → width fills parent container (`w-full` equivalent)

### Density / size variants

| Variant | Height | Notes |
|---------|--------|-------|
| Large | `48px` | Confirmed from examples page instance dimensions |
| Medium | <!-- NOT FOUND --> | Not measured from available data |
| Small | <!-- NOT FOUND --> | Not measured from available data |

---

## Interaction states

States visible in the Figma Label Button variant structure.

| State | Trigger | Visual change |
|-------|---------|---------------|
| `Rest` | Default | Base appearance |
| `Hover` | Pointer over | Background changes to hover token (e.g. `hover15` for Primary) |
| `Active` | Pointer down / pressed | Background changes to active token (e.g. `active14` for Primary) |
| `Focus` | Keyboard tab | Focus ring visible; no background token change annotated |
| `Disabled` | `isDisabled=true` | Background → `disabled01`, text/icon → `disabled04`; still focusable |

### Icon Button Toggle — additional states

| State | Notes |
|-------|-------|
| Rest - Unselected | Default unselected |
| Hover - Unselected | Hover over unselected button |
| Rest - Selected | Toggle activated |
| Hover - Selected | Hover over selected button |
| Active - Selected | Press on selected button |
| Focus - Unselected | Keyboard focus, unselected |
| Focus - Selected | Keyboard focus, selected |
| Disabled - Unselected | Cannot interact |
| Disabled - Selected | Locked in selected state |

---

## Design decisions & annotations

> **Label Button component description:** [https://oxygen.8x8.com/docs/components/button/usage](https://oxygen.8x8.com/docs/components/button/usage)

> **Icon button toggle behaviour:** "Clicking on the icon button will change the state to selected." / "Clicking on the selected icon button will change the state to unselected."

> **Token reference page purpose:** "A comprehensive, single-source map of every semantic color token applied to the 8x8 Design System's button component—covering all visual variants (Primary, Secondary, Danger, Text) across every interaction state (Rest, Hover, Active, Disabled)—to ensure consistent theming and effortless hand-off between design and engineering."

<!-- NO FURTHER ANNOTATIONS FOUND IN FIGMA RESPONSE -->

---

## Accessibility (from Figma annotations only)

- **ARIA role:** <!-- NOT ANNOTATED IN FIGMA -->
- **Focus order:** <!-- NOT ANNOTATED IN FIGMA -->
- **Keyboard interactions:** <!-- NOT ANNOTATED IN FIGMA -->

> No accessibility annotations found in this Figma file. For full accessibility documentation
> see [accessibility.md](./accessibility.md) produced by oxygen-mcp-extract.

---

## Gaps & conflicts

| Type | ID | Description |
|------|----|-------------|
| **CONFLICT** | C-001 | **Secondary rest background token mismatch.** Figma reference page shows `$action01` (blue, `#0056E0`) for Secondary rest. tokens.md specifies `action02` (#26252A, near-black). These are visually different colors. Either the Figma reference has a copy-paste error, or tokens.md is stale. Needs designer confirmation. |
| **CONFLICT** | C-002 | **Text button active token unexpected.** Figma shows `$active17` for Text Primary and Text Danger active bg. tokens.md defines `active17` as "Inverted primary button active" — likely wrong for non-inverted text variants. tokens.md shows no active bg for Text buttons at all. Needs resolution. |
| **CONFLICT** | C-003 | **CSS variable naming vs semantic token naming.** Design context emits `var(--actions/action09)` for Primary bg; tokens.md names the same color `action01`. The path/index naming schemes diverge. Downstream tooling (Storybook, Docusaurus) must decide which name to surface. |
| **New data** | N-001 | **Disabled tokens `$disabled01` and `$disabled04` identified in Figma.** These are not in tokens.md (GAP-011 in the audit). Recommend adding them to tokens.md with the correct hex values — which require a separate token lookup since they are referenced by name only in this Figma file. |
| **New data** | N-002 | **`Fluid 100%` variant axis in Figma.** Label Button has a `Fluid 100%=True/False` axis for full-width layout. props.md does not document a `fullWidth` prop for the main Button component (only for DropdownButton). May be a props gap. |
| **Missing annotation** | M-001 | No Figma accessibility annotations found. ARIA roles, focus order, and keyboard interactions are undocumented at the design layer. |
| **Incomplete data** | I-001 | Medium and Small button dimensions/padding not measured — only Large size (48px height, 16px/12px padding) confirmed from examples page instances. |
| **Incomplete data** | I-002 | Figma Type axis covers only Primary/Secondary/Text. The Oxygen variants `tertiary`, `tertiaryReversed`, `success`, `destructive` are not represented here — they likely live in a separate Figma component set (circular/control buttons). |
| **Incomplete data** | I-003 | Figma Variables API returned empty — no variable bindings extractable. Tokens are inferred from text annotations only. Actual Figma variable → token mapping unavailable. |

---

_Source: Figma MCP · figma-console MCP · Extracted 2026-04-28_
