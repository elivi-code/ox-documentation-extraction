---
parent: "[[SkeletonCircle]]"
section: usage
component: SkeletonCircle
role: spoke
pipeline_stage: draft
source_type: editorial
tags:
  - oxygen
  - component/SkeletonCircle
  - role/usage
  - stage/draft
---

<!-- SOURCE: editorial — no Figma "↳ Skeleton loader examples" page exists -->
<!-- REFERENCE PAGE: https://oxygen.8x8.com/components/skeletonloader/usage -->
<!-- DRAFTED: 2026-05-14 -->

> **WARN-003 — Editorial draft:** `SkeletonCircle-usage.md` is authored from extracted artifacts and the public [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) page. No Figma `↳ Skeleton loader examples` page exists, so `figma-extract-usage` cannot run. The 6 Do/Don't pairs are grounded and cited but designer-unreviewed. Replace with `figma-extract-usage` output when a Figma examples page is created.

`SkeletonCircle` is a fully-rounded content placeholder from `@8x8/oxygen-skeletons` that appears while an **avatar** or **individual icon** is loading. Pair with [[SkeletonBlock]] for text lines and images in the same layout. Both components fade between `ui01` and `ui02` to convey activity.

---

## When to use

- Replacing an **avatar** (xlarge / large / medium / small — 80px → 28px) while a user, contact, or profile loads.
- Replacing an **individual icon** in a small slot (24px → 16px) — toolbar, list-item leading icon, status indicator.
- The loaded element is **round** in the design — circle skeletons must visually match circular avatars, not square thumbnails.
- The page or list is **incrementally loading** and a circular placeholder keeps the row layout stable until the avatar arrives.

## When not to use

| Situation | Use instead |
|-----------|-------------|
| The element being loaded is an **image, thumbnail, or hero** | [[SkeletonBlock]] with an image size value |
| The element is a **text line** | [[SkeletonBlock]] with the text-style size value |
| The container content cannot be predicted at all | Spinner — indeterminate loading indicator |
| Loading is happening inside a **menu, dropdown, or modal** | Spinner |
| You have a real percentage (0–100%) | Progress Bar |

---

## Do / Don't

<!-- SCREENSHOTS UNAVAILABLE — no Figma examples page exists for Skeleton loader -->

### Pair 1 — Match the diameter to the avatar or icon size being replaced

#### ✅ Do — Pick the `size` value whose diameter matches the loaded avatar / icon slot

> `SkeletonCircle` ships nine diameter values. Use the one that matches the avatar tier the skeleton is replacing, so the row keeps its height when the real avatar paints.

```tsx
import { SkeletonCircle } from '@8x8/oxygen-skeletons';

// Profile header — extra-large avatar
<SkeletonCircle size="80px - xlarge" />

// Standard contact-list avatar
<SkeletonCircle size="48px - large" />

// Compact list / chat avatar
<SkeletonCircle size="40px - medium" />
```

#### ❌ Don't — Default every avatar to the same diameter regardless of slot

> Rendering a 40px `medium` circle in a slot that will load an 80px header avatar means the page reflows when the real avatar paints. Pick the size that matches the loaded slot.

```tsx
// ❌ Same size everywhere — the header avatar will jump on load
<SkeletonCircle size="40px - medium" />   {/* header — should be 80px */}
<SkeletonCircle size="40px - medium" />   {/* list row — correct */}
```

---

### Pair 2 — Use Circle for avatars and individual icons only

#### ✅ Do — Reserve `SkeletonCircle` for **avatars** and **individual icons**

> The Oxygen Skeleton family has two shape primitives. Use them the same way the real UI does — never as interchangeable.

```tsx
import { SkeletonBlock, SkeletonCircle } from '@8x8/oxygen-skeletons';

// ✅ Avatar skeleton
<SkeletonCircle size="48px - large" />

// ✅ Square thumbnail / image — use SkeletonBlock instead
<SkeletonBlock size="custom - image" />
```

#### ❌ Don't — Use a large `SkeletonCircle` to stand in for a square image or thumbnail

> Showing a circle where a square will paint misrepresents the shape. The user will see the layout transform from round to square when the real content arrives.

---

### Pair 3 — Keep one diameter per list or grid

#### ✅ Do — Use a single, consistent diameter across every row of a list or grid

> A contact list or chat history renders all avatars at the same size. The skeleton should mirror that — every row uses the same `SkeletonCircle` size.

```tsx
{Array.from({ length: 5 }).map((_, i) => (
  <div key={i} style={{ display: 'flex', alignItems: 'center', gap: '12px' }}>
    <SkeletonCircle size="40px - medium" />
    <div style={{ flex: 1, display: 'flex', flexDirection: 'column', gap: '8px' }}>
      <SkeletonBlock size="20px - body01" />
      <SkeletonBlock size="16px - label01" />
    </div>
  </div>
))}
```

#### ❌ Don't — Mix sizes within one collection

> Rendering some rows with `48px - large` and others with `28px - small` produces a loading state that doesn't predict the loaded state.

---

### Pair 4 — Pair Circle with adjacent Block lines for rows

#### ✅ Do — Combine `SkeletonCircle` with `SkeletonBlock` lines for contact rows, comment cards, and list items

> `SkeletonCircle` rarely stands alone — the row also has a name and a secondary line. Wrap one circle and two blocks in a flex row to skeleton the entire pattern.

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

#### ❌ Don't — Use a lone `SkeletonCircle` where the loaded UI has a circle **and** text

> A lone circle leaves a large blank space to the right. The skeleton fails to preserve the row's layout, so the page jumps on load.

---

### Pair 5 — Announce loading on the parent, not on each skeleton

#### ✅ Do — Set `aria-busy="true"` (plus an accessible name) on the **parent container**, once per loading region

> `SkeletonCircle` is purely presentational — no role, no text, no tab stop. Communicate loading on the **parent** that wraps the row or list, not per skeleton.

```html
<ul aria-busy="true" aria-label="Loading contacts">
  <li>
    <SkeletonCircle size="40px - medium" />
    <SkeletonBlock size="20px - body01" />
  </li>
</ul>
```

#### ❌ Don't — Add `aria-label="Loading"` or `role="status"` to every individual `SkeletonCircle`

> Per-skeleton labels cause screen readers to read "Loading. Loading. Loading. Loading…" across a 20-row list. One label on the parent region is correct.

---

### Pair 6 — Honour `prefers-reduced-motion`

#### ✅ Do — Verify the shimmer animation pauses (or is removed) when the user has requested reduced motion

> The skeleton animation fades the circle's fill between `ui01` and `ui02`. Confirm in `@media (prefers-reduced-motion: reduce)` that the circle renders as a static `ui02` disc — no fade.

#### ❌ Don't — Re-apply a custom shimmer in a parent stylesheet without gating on motion preferences

> Wrapping the skeleton in a parent that re-applies its own `@keyframes` overrides the Oxygen reduced-motion behaviour. Any custom shimmer must be wrapped in `@media (prefers-reduced-motion: no-preference)`.

---

_Source: editorial guidance authored from props.md, examples.md, accessibility.md, tokens.md, SkeletonCircle-figma.md, and oxygen.8x8.com/components/skeletonloader/usage · 2026-05-14_
