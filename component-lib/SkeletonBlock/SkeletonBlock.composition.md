---
parent: "[[SkeletonBlock]]"
section: composition
---

## Composition

`SkeletonBlock` is a **leaf component** — a single styled `div` with no child elements, no subcomponents, and no nested structure. It cannot contain other components and exposes no slots.

---

## Subcomponents

None. Each variant is an independent leaf node.

---

## Sibling component

| Component | Relationship | Package |
|-----------|-------------|---------|
| [[SkeletonCircle]] | Companion — used alongside `SkeletonBlock` to skeleton circular elements (avatars, icons) in the same layout | `@8x8/oxygen-skeletons` |

`SkeletonBlock` and `SkeletonCircle` are exported from the same package and are designed to be composed together. Neither contains the other — they are placed as siblings in a wrapper element.

---

## Composition patterns

### Card / list-row skeleton

The most common composition pattern: a `SkeletonCircle` for the avatar, two `SkeletonBlock` lines for name and secondary text, wrapped in a flex container.

```tsx
import { SkeletonBlock, SkeletonCircle } from '@8x8/oxygen-skeletons';

<div style={{ display: 'flex', alignItems: 'center', gap: '12px' }}>
  <SkeletonCircle size="medium" />
  <div style={{ flex: 1, display: 'flex', flexDirection: 'column', gap: '8px' }}>
    <SkeletonBlock size="22px - body02" />
    <SkeletonBlock size="16px - label01" />
  </div>
</div>
```

### Paragraph / text block skeleton

Multiple `SkeletonBlock` components stacked with `spacing03` (8px) gaps to simulate a paragraph.

```tsx
<div style={{ display: 'flex', flexDirection: 'column', gap: '8px' }}>
  <SkeletonBlock size="28px - heading01" />
  <SkeletonBlock size="20px - body01" />
  <SkeletonBlock size="20px - body01" />
</div>
```

### Image + content skeleton

A `custom - image` block above text lines, simulating a card with a thumbnail.

```tsx
<div style={{ display: 'flex', flexDirection: 'column', gap: '8px' }}>
  <SkeletonBlock size="custom - image" />
  <SkeletonBlock size="22px - body02" />
  <SkeletonBlock size="16px - label01" />
</div>
```

---

## Usage in named patterns

`SkeletonBlock` appears as a loading-state ingredient in card, list row, and table patterns. No formally named pattern pages exist yet for these in the Oxygen design system documentation.
