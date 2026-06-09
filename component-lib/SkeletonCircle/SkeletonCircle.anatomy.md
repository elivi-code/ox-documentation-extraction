---
parent: "[[SkeletonCircle]]"
section: anatomy
component: SkeletonCircle
role: spoke
pipeline_stage: draft
tags:
  - oxygen
  - component/SkeletonCircle
  - role/anatomy
  - stage/draft
---

## Visual reference

<!-- source: figma-only -->

![SkeletonCircle](./source/figma-screenshot-SkeletonCircle.png)

Figma: [node 31984:56124](https://figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=31984:56124)

---

## Anatomy

The Figma node `31984:56124` is a component set frame named **"Circle"** (256×667px) on the "Skeleton loader" page. It contains **18 variant symbols** arranged in two columns (Light on left, Dark on right), covering 9 size variants × 2 modes.

| # | Node ID | Variant key | Dimensions | Notes |
|---|---------|-------------|------------|-------|
| 1 | `31984:56125` | `Mode=Light, Size=80px - xlarge` | 80×80px | Default variant |
| 2 | `31984:56126` | `Mode=Dark, Size=80px - xlarge` | 80×80px | |
| 3 | `31984:56127` | `Mode=Light, Size=48px - large` | 48×48px | |
| 4 | `31984:56128` | `Mode=Dark, Size=48px - large` | 48×48px | |
| 5 | `31984:56129` | `Mode=Light, Size=40px - medium` | 40×40px | |
| 6 | `31984:56130` | `Mode=Dark, Size=40px - medium` | 40×40px | |
| 7 | `31984:56131` | `Mode=Light, Size=32px - small` | 32×32px | |
| 8 | `31984:56132` | `Mode=Dark, Size=32px - small` | 32×32px | |
| 9 | `50238:4493` | `Mode=Light, Size=28px - small` | 28×28px | Added later (node prefix 50238) |
| 10 | `50238:4499` | `Mode=Dark, Size=28px - small` | 28×28px | |
| 11 | `31984:56133` | `Mode=Light, Size=24px - xsmall` | 24×24px | |
| 12 | `31984:56134` | `Mode=Dark, Size=24px - xsmall` | 24×24px | |
| 13 | `50238:4491` | `Mode=Light, Size=22px - xsmall` | 22×22px | Added later |
| 14 | `50238:4501` | `Mode=Dark, Size=22px - xsmall` | 22×22px | |
| 15 | `50238:4496` | `Mode=Light, Size=20px - xsmall` | 20×20px | Added later |
| 16 | `50238:4503` | `Mode=Dark, Size=20px - xsmall` | 20×20px | |
| 17 | `50238:4520` | `Mode=Light, Size=16px - xsmall` | 16×16px | Smallest; added later |
| 18 | `50238:4521` | `Mode=Dark, Size=16px - xsmall` | 16×16px | |

**Element classification:**

| Element | Type | Role |
|---------|------|------|
| Each variant symbol | Symbol (instance) | Single fully-rounded `div` representing a circular placeholder |

Each variant is a **single leaf node** with no child elements. There are no nested components, slots, or boolean toggles.

> **Node prefix note:** Variants with prefix `50238` (28px, 22px, 20px, 16px) were added after the original set (`31984`), consistent with the pattern in the Block component set.

---

## Variant axes

<!-- CONFLICT:GAP-001 finding="Size axis values use Figma format (80px - xlarge, 40px - medium, etc.); SkeletonBlock/props.md references SkeletonCircle using short labels (xlarge, medium). React size prop enum format unverified." HUMAN DECISION REQUIRED -->

| Axis | Values | Default | Notes |
|------|--------|---------|-------|
| `mode` | `Light`, `Dark` | `Light` | Theme mode — driven by theme provider in application context |
| `size` | `80px - xlarge`, `48px - large`, `40px - medium`, `32px - small`, `28px - small`, `24px - xsmall`, `22px - xsmall`, `20px - xsmall`, `16px - xsmall` | `80px - xlarge` | Determines diameter; value names reference the avatar/icon size context |

<!-- STUB:GAP-010 source="Re-run figma_get_component (format=metadata, enrich=true) on node 31984:56124 with Desktop Bridge running to retrieve component key, boolean toggles, and instance swap slots." -->

### Boolean toggles

No boolean toggles found. Desktop Bridge was offline during extraction — inner layer properties unavailable.

### Instance swap slots

No instance swap slots found. Desktop Bridge was offline during extraction.

---

## Interaction states

`SkeletonCircle` is non-interactive. No hover, focus, or pressed states exist.

| State | Trigger | Visual change |
|-------|---------|---------------|
| Animating (default) | Mount | Fill fades between `ui01` and `ui02` |
| (No other states) | — | — |

---

## Structure & spacing

| Property | Value | Token | Notes |
|----------|-------|-------|-------|
| Shape | Fully rounded circle | — | `border-radius: 100px` — hardcoded, no token binding found |
| Width = Height | Varies by `size` axis | — | Square aspect ratio; border-radius makes it circular |
| Layout | Single `div`, no children | — | `overflow-clip`, `relative` |

---

## Design decisions & annotations

> **Size names reference avatar/icon context:** Each size value encodes both the pixel dimension and the semantic size label (e.g. `40px - medium`), making it clear which avatar or icon slot the skeleton replaces.

> **Two "small" and four "xsmall" values:** The size labels don't map 1:1 to pixel values — both 32px and 28px are "small", and 24/22/20/16px are all "xsmall". This matches real-world avatar/icon sizing where multiple pixel sizes share a label tier.

> **Shared token with Block:** Both `SkeletonBlock` and `SkeletonCircle` use `--ui/ui02` as the fill token, ensuring visual consistency across skeleton types.

> **Documentation link:** `https://oxygen.8x8.com/docs/components/skeletonloader`

---

_Source: Figma MCP · figma-console MCP · Extracted 2026-05-05_
