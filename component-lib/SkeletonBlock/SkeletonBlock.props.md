---
parent: "[[SkeletonBlock]]"
section: props
---

## Props — SkeletonBlock

<!-- STUB:GAP-002 source="Check @8x8/oxygen-skeletons source for all exported prop names, types, and defaults. Replace Figma-axis props with confirmed React props. If `mode` is not a React prop, remove it and add a note explaining theme-provider-driven mode switching." -->

> **SOURCE GAP (GAP-002 + GAP-007):** `get-component-props` returned no prop definitions for `SkeletonBlock`. The rows below are Figma variant axes — React prop names, types, and defaults are unconfirmed. `mode` in particular is likely not a React prop (see GAP-007).

| Name | Type | Default | Required | Description | Accepts |
|---|---|---|---|---|---|
| `size` | enum | `"40px - heading02"` | false | Height of the skeleton block. Use the value whose name matches the text style or element being replaced. | — |
| `mode` | `"Light" \| "Dark"` | `"Light"` | false | Theme mode. In Oxygen apps, typically driven by the theme provider rather than set directly on the component. May not be a React prop — verify against package source. | — |

<!-- STUB:GAP-007 source="Confirm via @8x8/oxygen-skeletons source whether `mode` is a React prop. If not, remove it and add a note that mode switching is handled by the Oxygen theme provider." -->

### `size` values — SkeletonBlock

| Value | Height | Intended use |
|---|---|---|
| `40px - heading02` | 40px | Replaces a `heading02` text element |
| `28px - heading01` | 28px | Replaces a `heading01` text element |
| `24px - bulletList01` | 24px | Replaces a `bulletList01` text element |
| `22px - body02` | 22px | Replaces a `body02` text element |
| `20px - body01` | 20px | Replaces a `body01` text element |
| `16px - label01` | 16px | Replaces a `label01` text element |
| `custom - image` | 240px | Replaces an image or block-level element |

---

## Props — SkeletonCircle

<!-- CONFLICT:GAP-001 finding="SkeletonBlock/props.md uses short labels (xlarge, large, medium, small, xsmall) for SkeletonCircle size; SkeletonCircle/props.md uses Figma axis format (80px - xlarge, 48px - large, 40px - medium). The actual React prop enum is unknown — @8x8/oxygen-skeletons source must be checked to determine which format is correct." HUMAN DECISION REQUIRED -->

> **CONFLICT (GAP-001):** The `size` values below use **short labels** (this folder's convention, sourced from OX usage docs). `SkeletonCircle/props.md` uses Figma axis format (`"80px - xlarge"`, `"40px - medium"`). The correct React enum is unknown until the `@8x8/oxygen-skeletons` package source is checked. All four files (`SkeletonBlock/props.md`, `SkeletonBlock/examples.md`, `SkeletonCircle/props.md`, `SkeletonCircle/examples.md`) must be aligned once the format is confirmed.

| Name | Type | Default | Required | Description | Accepts |
|---|---|---|---|---|---|
| `size` | enum | — | false | Diameter of the circle skeleton. | — |

### `size` values — SkeletonCircle

| Value | Diameter | Intended use |
|---|---|---|
| `xlarge` | 80px | Extra-large avatar |
| `large` | 48px | Large avatar |
| `medium` | 40px | Medium avatar |
| `small` | 32px / 28px | Small avatar / icon |
| `xsmall` | 24px / 22px / 20px / 16px | Extra-small icon (multiple sub-sizes) |

---

## Slots / events

No slots or event callbacks. Both `SkeletonBlock` and `SkeletonCircle` are purely presentational.

---

## Installation

```
@8x8/oxygen-skeletons
```

**Components exported:** `SkeletonBlock`, `SkeletonCircle`

```bash
yarn add @8x8/oxygen-skeletons
# Requires 8x8 VPN + @8x8 registry in .npmrc
# @8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```
