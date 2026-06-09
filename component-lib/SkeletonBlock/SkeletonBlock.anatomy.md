---
parent: "[[SkeletonBlock]]"
section: anatomy
---

## Anatomy

SkeletonBlock is a **single-element component** — a styled `div` with a rounded rectangle background fill and no child elements. There are no nested components, no slots, no boolean toggles, and no instance swap slots.

The Figma component set (node `31984:56109`, named "Block") arranges **14 variant symbols** in a two-column grid: 7 size variants × 2 mode variants (Light left, Dark right). This grid is a Figma documentation layout, not a component layout constraint.

| # | Node ID | Variant key | Dimensions |
|---|---------|-------------|------------|
| 1 | `31984:56110` | `Mode=Light, Size=40px - heading02` | 362×40px |
| 2 | `31984:56111` | `Mode=Dark, Size=40px - heading02` | 362×40px |
| 3 | `31984:56112` | `Mode=Light, Size=28px - heading01` | 362×28px |
| 4 | `31984:56113` | `Mode=Dark, Size=28px - heading01` | 362×28px |
| 5 | `46034:4` | `Mode=Light, Size=24px - bulletList01` | 362×24px |
| 6 | `46034:5` | `Mode=Dark, Size=24px - bulletList01` | 362×24px |
| 7 | `31984:56114` | `Mode=Light, Size=22px - body02` | 362×22px |
| 8 | `31984:56118` | `Mode=Dark, Size=22px - body02` | 362×22px |
| 9 | `31984:56115` | `Mode=Light, Size=20px - body01` | 362×20px |
| 10 | `31984:56117` | `Mode=Dark, Size=20px - body01` | 362×20px |
| 11 | `31984:56116` | `Mode=Light, Size=16px - label01` | 362×16px |
| 12 | `31984:56119` | `Mode=Dark, Size=16px - label01` | 362×16px |
| 13 | `50238:836` | `Mode=Light, Size=custom - image` | 362×240px |
| 14 | `50238:834` | `Mode=Dark, Size=custom - image` | 362×240px |

### Variant axes

| Property | Values | Default | Notes |
|----------|--------|---------|-------|
| `mode` | `Light`, `Dark` | `Light` | Theme mode — driven by theme provider in application context |
| `size` | `40px - heading02`, `28px - heading01`, `24px - bulletList01`, `22px - body02`, `20px - body01`, `16px - label01`, `custom - image` | `40px - heading02` | Height; value names reference the text style being replaced |

<!-- STUB:GAP-009 source="Open the Skeleton loader Figma page with Desktop Bridge running and re-run figma_get_component (format=metadata, enrich=true) on node 31984:56109 to capture component key, boolean toggles, and instance swap slots." -->

### Boolean toggles

<!-- Desktop Bridge offline during extraction — inner layer properties unavailable (GAP-009) -->

### Instance swap slots

<!-- Desktop Bridge offline during extraction — inner layer properties unavailable (GAP-009) -->

---

## Height by size variant

| Size | Height | Replaces |
|------|--------|----------|
| `40px - heading02` | 40px | `heading02` text style |
| `28px - heading01` | 28px | `heading01` text style |
| `24px - bulletList01` | 24px | `bulletList01` text style |
| `22px - body02` | 22px | `body02` text style |
| `20px - body01` | 20px | `body01` text style |
| `16px - label01` | 16px | `label01` text style |
| `custom - image` | 240px | Image or block-level element |

---

## Interaction states

SkeletonBlock has **no interactive states**. It is a passive, animated display element.

| State | Trigger | Visual change |
|-------|---------|---------------|
| Animating (default) | Mount | Background fades between `ui01` and `ui02` |

No hover, focus, pressed, disabled, or error states exist.

---

## Design decisions

- **Size values mirror text style names:** Each `size` value encodes both the height in pixels and the Oxygen text style it replaces (e.g. `20px - body01`). This removes ambiguity for engineers and keeps skeleton and loaded state at the same height, eliminating layout shift on content paint.
- **`custom - image` at 240px:** The image/block variant uses 240px as a representative height in the component set. In practice, height should match the image or block being replaced.
- **Two-column Figma layout:** Light and Dark variants are arranged side-by-side for visual comparison — they are independent symbols, not nested.
