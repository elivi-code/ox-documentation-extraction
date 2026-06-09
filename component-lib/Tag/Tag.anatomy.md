---
parent: "[[Tag]]"
section: anatomy
component: Tag
package: "@8x8/oxygen-tag"
role: anatomy
pipeline_stage: doc_rewrite
audit_verdict: YES
siblings:
  - "[[Tag]]"
  - "[[Tag.props]]"
  - "[[Tag.tokens]]"
  - "[[Tag.usage]]"
  - "[[Tag.accessibility]]"
  - "[[Tag.platform]]"
  - "[[Tag.composition]]"
tags: [component, data_display, role/anatomy]
---

## Component sets

The Tag Figma node (`8083:8359`) contains two independent component sets:

| Component set | Node ID | Description |
|---|---|---|
| Standard Tag | `16334:16412` | Pill tag with optional leading icon and optional remove action |
| Avatar Tag | `16390:16896` | Pill tag with a fixed avatar photo and optional remove action |

Both share a 24 px height and a fully-rounded (pill) shape. They differ in anatomy, available color variants, and `type` values.

---

## Standard Tag anatomy

| # | Type | Name | Role | Notes |
|---|---|---|---|---|
| 1 | frame | Container | Structural | Auto-layout horizontal; `h-24px`; `gap-4px`; `py-2px`; `border-radius: 15px`; background token applied here |
| 2 | instance | Leading icon | Optional slot | Controlled by `icon?` boolean (default: `true`). Instance-swap slot; default `face-smile` (84161:245102). Rendered at `iconSizeXS` (16×16 px). |
| 3 | text | Label | Content element | Default "Tag"; uses `$label01` text style (12 px, weight 400, Inter). Color varies by `color` + `mode`. |
| 4 | instance | Close button (×) | Optional slot | Present only when `type=withAction`. Maps to the `CloseButton` component (`packages/tag/src/components/CloseButton.tsx`). |
| 5 | frame | Focus ring | Transient state | `size-24px`, `rounded-1000px`, `border-2`; visible only when `type=withAction` and `focus?=true`. |

**Examples page annotation:** `Leading icon (optional) · Label · Remove button (optional)`

---

## Avatar Tag anatomy

| # | Type | Name | Role | Notes |
|---|---|---|---|---|
| 1 | frame | Container | Structural | Same pill shape; padding asymmetric — no left padding (avatar sits flush), `pr-8px` (default) or `pr-4px` (withAction/withActionError). Error border added when `type=withActionError`. |
| 2 | instance | Avatar | Fixed sub-component | `size-24px`, `rounded-1000px`; circular photo. Uses the [[Avatar]] component (`packages/avatar`). Always present. |
| 3 | text | Label | Content element | Default "Josephine Lu"; same `$label01` style as Standard Tag. |
| 4 | instance | Close button (×) | Optional slot | Present when `type=withAction` or `type=withActionError`. Same `CloseButton` component. |
| 5 | frame | Error border | State indicator | `border-2 border-[var(--error/error01)]`; only when `type=withActionError`. |
| 6 | frame | Focus ring | Transient state | Same structure as Standard Tag focus ring; only when `type=withAction`/`withActionError` and `focus?=true`. |

**Examples page annotation:** `Avatar · Label · Remove button (optional)`

---

## Standard Tag — variant axes

| Property | Values | Default |
|---|---|---|
| `mode` | `light`, `dark` | `light` |
| `color` | `default`, `blue`, `grey`, `red`, `yellow`, `green`, `yellow-emphasis` | `default` |
| `type` | `default`, `withAction` | `default` |

### Boolean toggles

| Property | Default | Notes |
|---|---|---|
| `icon?` | `true` | Shows/hides the leading icon slot |
| `focus?` | `false` | Shows/hides the focus ring — transient; only relevant when `type=withAction` |

### Instance swap slot

| Slot | Default component | Notes |
|---|---|---|
| `↪ icon` | `84161:245102` (face-smile) | Accepts any icon; rendered at `iconSizeXS` (16×16 px) |

**Variant matrix:** 28 components total (2 modes × 7 colors × 2 types)

---

## Avatar Tag — variant axes

| Property | Values | Default |
|---|---|---|
| `mode` | `light`, `dark` | `light` |
| `color` | `default`, `blue`, `grey`, `red`, `yellow-emphasis` | `default` |
| `type` | `default`, `withAction`, `withActionError` | `default` |

<!-- STUB:GAP-008 source="Confirm with component owner whether the omission of yellow and green from Avatar Tag is intentional. If intentional, add a design rationale note. If an oversight, request the designer add the missing variants." -->

> Avatar Tag omits the `yellow` and `green` color variants present in Standard Tag (5 colors vs 7). No Figma annotation explains the exclusion — intentionality is unconfirmed.

> Avatar Tag adds `withActionError` type not present in Standard Tag.

### Boolean toggles

| Property | Default | Notes |
|---|---|---|
| `focus?` | `false` | Shows/hides focus ring; only when `type=withAction` or `type=withActionError` |

**Variant matrix:** 30 components total (2 modes × 5 colors × 3 types)

---

## Persistent vs transient states

| State | Classification | Notes |
|---|---|---|
| `type=withAction` | Persistent API property | Determines structural layout (adds close button) |
| `type=withActionError` | Persistent API property (Avatar Tag only) | Adds error border + close button |
| `focus?=true` | Transient state | Focus ring visibility; not a direct code prop — mapped to `isFocused` |
| `icon?=true/false` | Boolean slot toggle | Toggles leading icon slot in Figma; not a direct code prop |

---

## Interaction states

| State | Trigger | Visual change | Applies to |
|---|---|---|---|
| Focused | Keyboard focus on close button | 2 px border + 4 px inset shadow focus ring | `type=withAction`; `type=withActionError` (Avatar Tag) |
| Error | `hasError` prop | Red `error01` 2 px solid border on container | Avatar Tag only — `withActionError` |

<!-- STUB:GAP-009 source="Request designer to add hover and pressed states to the Figma component sets. Alternatively, verify hover/active styling in CloseButton.tsx and document in accessibility.md and Tag-figma.md." -->

> No hover or active/pressed states are modelled in Figma for Tag. Neither component set includes hover/pressed variant axes. These interaction states may exist in implementation only.

---

## Structure and spacing

### Standard Tag container

| Property | Value | Notes |
|---|---|---|
| Height | `24px` | Fixed across all variants — hardcoded, no token binding |
| Border radius | `15px` | Pill shape — hardcoded, no token binding |
| Padding vertical | `2px` top + bottom | Conceptually maps to `spacing01` |
| Padding horizontal (`type=default`) | `8px` left + right | Conceptually maps to `spacing03` |
| Padding horizontal (`type=withAction`) | `8px` left, `4px` right | Reduced right padding for close button |
| Gap | `4px` | Between icon, label, close button — conceptually maps to `spacing02` |
| Auto-layout direction | Horizontal | `items-center` |

### Avatar Tag container

| Property | Value | Notes |
|---|---|---|
| Height | `24px` | Fixed |
| Border radius | `15px` | Pill shape |
| Padding vertical | `2px` | |
| Left padding | `0px` | Avatar sits flush left inside pill |
| Right padding (`type=default`) | `8px` | |
| Right padding (`type=withAction`/`withActionError`) | `4px` | Reduced for close button |
| Gap | `4px` | Between avatar, label, close button |
| Error border (`type=withActionError`) | `2px solid error01` | Applied to container |

### Sub-component sizing

| Sub-component | Size | Notes |
|---|---|---|
| Leading icon (Standard Tag) | `iconSizeXS` — 16×16 px | Via Code Connect — not from token data |
| Avatar (Avatar Tag) | 24×24 px | Rounded-1000px; fills the full tag height |
| Focus ring | 24×24 px | Absolutely positioned over the close button area |
| Close button | ~16×16 px | `CloseButton` component; exact size from sub-component source |

> All padding and gap values are hardcoded px — no Figma Variables binding confirmed for these spacing values.

---

## Text and effect styles

<!-- STUB:GAP-010 source="Re-run figma_get_styles with the Desktop Bridge plugin active to retrieve named text and effect styles. Confirm that label01 is the correct style name." -->

| Element | Style name | Size | Weight | Line height | Letter spacing |
|---|---|---|---|---|---|
| Label | `$label01` | 12 px | 400 (normal) | 16 px | 0 px |
| Font family | `typography/font-family/sans` | — | — | — | Inter |

> `figma_get_styles` returned 0 styles during extraction — names inferred from design context. Re-run with Desktop Bridge active to confirm.

---

## Examples page (node 52829:11107)

### Avatar tags section
- Anatomy: Avatar · Label · Remove button (optional)
- Types: Default | With remove action

### Standard tags section
- Anatomy: Leading icon (optional) · Label · Remove button (optional)
- Types: Default | With remove action
- RAG tags: Red · Amber (yellow) · Green — named status pattern

### Tags inside Select section
> "The tags used inside the select component when multiple selection is on."
- Standard and Avatar Tags shown inside a Select component
- Both forms support multi-select usage

---

## Design notes

<!-- SKIP:GAP-007 manual="Request designer or component owner to update the Figma component description URL from the contribution guide placeholder to the correct Tag usage page." -->

> **Standard Tag Figma description:** links to `https://oxygen.8x8.com/docs/Contribution/intro` — a placeholder/incorrect URL. Correct URL should point to the Tag usage page.
>
> **Component status:** Stable (from `_Information & support` panel in canvas).
>
> **Figma Variables API unavailable** during extraction — all token names inferred from CSS fallback variable paths (e.g. `var(--ui/ui01, #ebeae1)`). See [[Tag.tokens]] for full token reference.

---

_Source: Figma MCP · figma-console MCP · Tag node 8083:8359 · Extracted 2026-05-01_
