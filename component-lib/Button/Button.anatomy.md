---
parent: "[[Button]]"
section: anatomy
component: Button
package: "@8x8/oxygen-button"
figma: "https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=15653:16329"
tags: [oxygen, component/Button, role/anatomy, section/anatomy]
---

# Button — Anatomy, Variants & States

Element structure, variant axes, and interaction states extracted from the Label Button component set (`15653:16329`).

---

## Anatomy

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | Container | Structural | Auto-layout horizontal; padding 16px H / 12px V; border-radius 6px; bg token applied here |
| 2 | instance | Swap Icon L | Optional slot | Controlled by `Icon L` boolean toggle (default: hidden). Instance-swap accepts any icon component. |
| 3 | text | Label | Content element | Default text "Button"; uses `$bodyBold02` text style (16px, semi-bold, Inter) |
| 4 | instance | Swap Icon R | Optional slot | Controlled by `Icon R` boolean toggle (default: hidden). Instance-swap accepts any icon component. |

### Sub-component: Icon Button Toggle

Separate component documented in the "Icon button toggle" section of the examples page. States observed: Rest-Unselected, Hover-Unselected, Rest-Selected, Hover-Selected, Active-Selected, Focus-Unselected, Focus-Selected, Disabled-Unselected, Disabled-Selected. Shown in both Light and Dark mode.

---

## Variant axes (Figma)

| Property | Values | Default |
|----------|--------|---------|
| `Mode` | `Light`, `Dark` | `Light` |
| `Type` | `Primary`, `Secondary`, `Text` | `Primary` |
| `Size` | `Large`, `Medium`, `Small` | `Large` |
| `State` | `Rest`, `Hover`, `Active`, `Focus`, `Disabled` | `Rest` |
| `Danger` | `False`, `True` | `False` |
| `Fluid 100%` | `False`, `True` | `False` |
| `isInverted` | `no`, `yes` | `no` |

> Figma `Type` covers only Primary/Secondary/Text. The Oxygen API variants `tertiary`, `tertiaryReversed`, `success`, `destructive` likely live in separate Figma component sets (Circular/Control Button). `Danger=True` maps to `isDestructive`; `Fluid 100%=True` maps to a full-width layout.

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

---

## Interaction states

| State | Trigger | Visual change |
|-------|---------|---------------|
| `Rest` | Default | Base appearance |
| `Hover` | Pointer over | Background changes to hover token (e.g. `hover15` for Primary) |
| `Active` | Pointer down / pressed | Background changes to active token (e.g. `active14` for Primary) |
| `Focus` | Keyboard tab | Focus ring visible; no background token change annotated |
| `Disabled` | `isDisabled=true` | Background → `disabled01`, text/icon → `disabled04`; still focusable |

### Icon Button Toggle — additional states

Rest-Unselected · Hover-Unselected · Rest-Selected · Hover-Selected · Active-Selected · Focus-Unselected · Focus-Selected · Disabled-Unselected · Disabled-Selected.

> **Toggle behaviour (Figma annotation):** "Clicking on the icon button will change the state to selected." / "Clicking on the selected icon button will change the state to unselected."

---

## Structure & spacing

### Container (Label Button, Large size)

| Property | Value | Variant |
|----------|-------|---------|
| Height | `48px` (inferred: 12+24+12) | Large |
| Padding horizontal | `16px` | All sizes (Large confirmed) |
| Padding vertical | `12px` | Large |
| Border radius | `6px` | All variants |

### Internal spacing

| Property | Value | Notes |
|----------|-------|-------|
| Gap (icon–label) | `8px` | Between icon slots and label |
| Icon size | `24×24px` | Both left and right icon slots |

### Auto-layout

- Direction: **horizontal**; alignment center on both axes (`justify-center`, `items-center`).
- `Fluid 100%=True` → width fills parent container (`w-full` equivalent).

### Text style

| Element | Style | Size | Weight | Line height | Letter spacing |
|---------|-------|------|--------|-------------|----------------|
| Label | `$bodyBold02` | 16px | 600 (semi-bold) | 24px | 0.0121px |

<!-- SKIP:GAP-016 manual="Medium and Small button dimensions NOT FOUND — only Large (48px H / 16px / 12px) extractable. Inspect Medium and Small child variants of node 15653:16329." -->
<!-- SKIP:GAP-017 manual="Figma Variables API returned empty — token bindings inferred from text annotations only; actual variable-to-token mapping unverified. Re-run figma_get_variables with includePublished=true." -->

> ⚠️ **WARN-003:** Figma Type axis covers only Primary/Secondary/Text. Variants `tertiary`, `tertiaryReversed`, `success`, `destructive` likely live in a separate circular/control button set — run `figma-extract` against those nodes to complete Figma coverage.
