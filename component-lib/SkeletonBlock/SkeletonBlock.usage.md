---
parent: "[[SkeletonBlock]]"
section: usage
---

<!-- source: figma-only -->
<!-- WARN-003: This usage file is an editorial draft — no Figma "↳ Skeleton loader examples" page exists. The 6 Do/Don't pairs are sourced from props.md, examples.md, accessibility.md, tokens.md, SkeletonBlock-figma.md, and oxygen.8x8.com/components/skeletonloader/usage. Replace with figma-extract-usage output when a Figma examples page is created. -->

## Usage

`SkeletonBlock` is a rectangular content placeholder that appears while text, images, or block-level elements are loading. Pair it with [[SkeletonCircle]] to skeleton avatars and icons in the same layout. Both components fade between the `ui01` and `ui02` tokens to convey activity until real content paints.

---

## When to use

- The general shape of the loaded content is **already known** — you can predict where text lines and images will appear.
- Filling **large container-based components** such as cards, list rows, or tables where multiple stacked elements need a placeholder.
- Content is loading **incrementally** — different parts of the page can paint at different times; the skeleton keeps the layout stable.
- Replacing **text lines** (use the size value matching the text style) or **images / block elements** (use `custom - image`).

## When not to use

| Situation | Use instead |
|-----------|-------------|
| Container content cannot be determined (you don't know what will appear) | [[Spinner]] — indeterminate loading indicator |
| You have a real percentage (0–100%) for the work | [[ProgressBar]] — determinate progress |
| Loading is happening inside a menu, dropdown, or modal | [[Spinner]] |
| The element being loaded is an avatar or individual icon | [[SkeletonCircle]] |
| You need to communicate a transient state ("Saved", "Sent") | [[Toast]] |

---

## Do / Don't

### Pair 1 — Match the size to the text style being replaced

#### ✅ Do — Pick the `size` value whose pixel height matches the text style the skeleton replaces

`SkeletonBlock` ships seven size values whose names encode both the height in pixels and the Oxygen text style they replace (e.g. `28px - heading01`, `20px - body01`, `16px - label01`). The naming is deliberate — it removes ambiguity and keeps loaded and unloaded states the same height, so the layout doesn't jump when content arrives.

```tsx
import { SkeletonBlock } from '@8x8/oxygen-skeletons';

// A heading + two body lines, sized to match the real text
<SkeletonBlock size="28px - heading01" />
<SkeletonBlock size="20px - body01" />
<SkeletonBlock size="20px - body01" />
```

#### ❌ Don't — Pick an arbitrary height ("looks about right") or reuse a single size for everything

Using `20px - body01` for a heading or `40px - heading02` for body copy makes the skeleton a different height than the text it stands in for. When real content paints, the page reflows visibly.

```tsx
// ❌ Same size for everything — layout will shift on load
<SkeletonBlock size="20px - body01" />   {/* will be replaced by a heading */}
<SkeletonBlock size="20px - body01" />
<SkeletonBlock size="20px - body01" />
```

---

### Pair 2 — Use `custom - image` for images and blocks, not for text

#### ✅ Do — Use `custom - image` (240px) only when the placeholder stands in for an image or block-level element

```tsx
import { SkeletonBlock } from '@8x8/oxygen-skeletons';

<SkeletonBlock size="custom - image" />
```

#### ❌ Don't — Use `custom - image` to fill the area where body text will load

A 240px-tall block standing in for a single paragraph misrepresents how much vertical space the real content will take and exaggerates perceived loading time.

---

### Pair 3 — Respect `spacing03` (8px) between stacked text-line skeletons

#### ✅ Do — Separate stacked text skeletons with `spacing03` (8px)

When multiple text skeletons stack to fake a paragraph, use the `spacing03` token (8px) as the gap. This matches the spacing in the loaded state, so the column height is the same before and after content paints.

```tsx
<div style={{ display: 'flex', flexDirection: 'column', gap: '8px' }}>
  <SkeletonBlock size="28px - heading01" />
  <SkeletonBlock size="20px - body01" />
  <SkeletonBlock size="20px - body01" />
</div>
```

#### ❌ Don't — Tighten or stretch the gap with hardcoded values

Pulling lines closer (`gap: 2px`) or spreading them apart (`gap: 24px`) gives the loading state a different rhythm from the loaded state — the column jumps when content paints.

---

### Pair 4 — Combine Block + Circle into one card skeleton

#### ✅ Do — Pair `SkeletonBlock` text lines with a `SkeletonCircle` avatar for cards and list rows

For a contact row or comment card (avatar + name + secondary line), combine one `SkeletonCircle` for the avatar with two `SkeletonBlock` lines sized to the text styles they replace. The loaded layout snaps in without reflow.

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

#### ❌ Don't — Try to replicate every detail of the loaded card (badges, icons, dividers)

A skeleton's job is to convey "this region is loading" with enough shape that the page doesn't feel empty. Modelling every secondary icon, divider, and badge produces a noisy placeholder that goes stale every time the real card design changes.

---

### Pair 5 — Communicate the loading state with `aria-busy`, not the shimmer alone

#### ✅ Do — Wrap the skeleton region in a container with `aria-busy="true"`

`SkeletonBlock` is purely presentational — it renders as a styled `div` with no text, no role, and no tab stop. Screen readers will not announce it. Communicate the loading state programmatically on the parent region.

```html
<div aria-busy="true" aria-label="Loading article">
  <SkeletonBlock size="28px - heading01" />
  <SkeletonBlock size="20px - body01" />
  <SkeletonBlock size="20px - body01" />
</div>
```

#### ❌ Don't — Rely on the shimmer animation as the only loading cue

The fade between `ui01` and `ui02` is purely visual. A non-sighted user, or a user who has disabled motion, receives no signal that the region is loading. Without `aria-busy` (or an equivalent live-region announcement) on the parent, the page reads as "empty" — not "loading".

---

### Pair 6 — Honour `prefers-reduced-motion`

#### ✅ Do — Verify the skeleton animation pauses (or is removed) when the user has requested reduced motion

The Oxygen skeleton animation transitions the fill between `ui01` and `ui02`. Looping animations can trigger vestibular discomfort. Confirm in `@media (prefers-reduced-motion: reduce)` that the skeleton renders as a static `ui02` rectangle with no fade.

#### ❌ Don't — Ship custom CSS that re-enables the shimmer for everyone

Wrapping the skeleton in a parent that re-applies its own `@keyframes` animation, or overriding Oxygen styles to force motion, undoes the package's reduced-motion behaviour. Any custom shimmer must itself be wrapped in `@media (prefers-reduced-motion: no-preference)`.
