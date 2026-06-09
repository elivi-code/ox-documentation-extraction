---
parent: "[[SkeletonCircle]]"
section: composition
component: SkeletonCircle
role: spoke
pipeline_stage: draft
tags:
  - oxygen
  - component/SkeletonCircle
  - role/composition
  - stage/draft
---

## Subcomponents

`SkeletonCircle` has no subcomponents. Each variant is a single leaf node with no child elements, nested components, or slots.

---

## Used alongside

`SkeletonCircle` is most commonly combined with [[SkeletonBlock]] to skeleton complete layout rows.

| Pattern | SkeletonCircle role | SkeletonBlock role |
|---------|-------------------|-------------------|
| Contact row (avatar + name + status) | Avatar placeholder | Name line + status/timestamp lines |
| Chat message (sender + text) | Sender avatar | Message body lines |
| Comment card | Author avatar | Author name + comment text lines |
| Profile header | Large avatar (80px) | Display name + handle lines |

### Contact row pattern

```tsx
import { SkeletonBlock, SkeletonCircle } from '@8x8/oxygen-skeletons';

<div style={{ display: 'flex', alignItems: 'center', gap: '12px' }}>
  <SkeletonCircle size="40px - medium" />
  <div style={{ flex: 1, display: 'flex', flexDirection: 'column', gap: '8px' }}>
    <SkeletonBlock size="20px - body01" />
    <SkeletonBlock size="16px - label01" />
  </div>
</div>
```

---

## Sibling component

[[SkeletonBlock]] is the rectangular counterpart to `SkeletonCircle`. Both:
- Belong to `@8x8/oxygen-skeletons`
- Share the `--ui/ui02` fill token
- Animate between `ui01` and `ui02`
- Are purely presentational (no props beyond `size` and `mode`)

Use `SkeletonCircle` for round elements (avatars, icons); use `SkeletonBlock` for rectangular elements (text lines, images, buttons).

---

## Consumer responsibility

`SkeletonCircle` has no awareness of loading state. The consuming component is responsible for:
- Conditionally rendering the skeleton while data is loading
- Replacing it with the real component once data is available
- Setting `aria-busy` on the parent container

---

_Source: Figma design context · SkeletonCircle-usage.md (editorial) · Extracted 2026-05-05_
