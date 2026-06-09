---
component: SkeletonBlock
package: "@8x8/oxygen-skeletons"
category: feedback_status
role: usage
role_description: "Usage guidelines — editorially authored from extracted artifacts and the public Oxygen Skeleton loader usage page; no Figma examples page exists"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from extracted artifacts + oxygen.8x8.com/components/skeletonloader/usage — NOT from Figma Do/Don't frames. Re-run doc-audit after creation; replace pairs with figma-extract-usage output when a Figma examples page exists. Shared family with SkeletonCircle."
source_type: editorial
audit_verdict: null
siblings:
  - "[[SkeletonBlock/props]]"
  - "[[SkeletonBlock/examples]]"
  - "[[SkeletonBlock/tokens]]"
  - "[[SkeletonBlock/accessibility]]"
  - "[[SkeletonBlock/SkeletonBlock-figma]]"
  - "[[SkeletonBlock/SkeletonBlock-audit]]"
  - "[[SkeletonCircle/SkeletonCircle-usage]]"
tags:
  - oxygen
  - component/SkeletonBlock
  - role/usage
  - stage/editorial
  - category/feedback_status
---
<!-- SOURCE: editorial — no Figma "↳ Skeleton loader examples" page exists -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- REFERENCE PAGE: https://oxygen.8x8.com/components/skeletonloader/usage -->
<!-- GROUNDING: full — props.md, examples.md, accessibility.md, tokens.md, SkeletonBlock-figma.md, SkeletonBlock-audit.md, oxygen.8x8.com/components/skeletonloader/usage -->
<!-- DRAFTED: 2026-05-14 -->
<!-- MODE: open -->
<!-- PAIRS: 6 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma examples page is created -->

# Skeleton Block — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [SkeletonBlock-figma.md](./SkeletonBlock-figma.md) ·
> [SkeletonCircle-usage.md](../SkeletonCircle/SkeletonCircle-usage.md)

> **Editorial guidance — not Figma-sourced.** No `↳ Skeleton loader examples` Figma page exists, so `figma-extract-usage` cannot run. The Do/Don't pairs below are inferred from `props.md`, `examples.md`, `accessibility.md`, `tokens.md`, `SkeletonBlock-figma.md`, and the public usage page at [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage). Treat as provisional until a designer reviews them. Replace with `figma-extract-usage` output when a Figma examples page is created.

`SkeletonBlock` is a rectangular content placeholder that appears while text, images, or block-level elements are loading. It is one half of the Oxygen skeleton family — pair it with [`SkeletonCircle`](../SkeletonCircle/SkeletonCircle-usage.md) to skeleton avatars and icons in the same layout. Both components fade between the `ui01` and `ui02` tokens to convey activity until the real content paints.

---

## When to use

- The general shape of the loaded content is **already known** to the application — you can predict where text lines and images will appear ([oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — "On full pages where the general format of the loaded content is known.").
- You are filling **large container-based components** such as cards, list rows, or tables where multiple stacked elements need a placeholder ([oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — "On large container-based components like tables or cards.").
- The content is loading **incrementally** — different parts of the page can paint at different times, and the skeleton keeps the layout stable until the real content arrives.
- Replacing **text lines** (use the size value that mirrors the text style being replaced) or **images / block elements** (use `custom - image`).

## When not to use

| Situation | Use instead |
|-----------|-------------|
| The container content cannot be determined (you don't know what will appear) | [Spinner](../Spinner/) — indeterminate loading indicator (per [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — "When the container content cannot be determined. Use a spinner or progress bar.") |
| You have a real percentage (0–100%) for the work | [Progress Bar](../ProgressBar/ProgressBar-usage.md) — determinate progress |
| Loading is happening inside a **menu, dropdown, or modal** | Spinner — per [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — "To represent content in menus, dropdowns, or modals." |
| The element being loaded is an **avatar or individual icon** | [`SkeletonCircle`](../SkeletonCircle/SkeletonCircle-usage.md) |
| You need to communicate a transient state ("Saved", "Sent") | [Toast](../Toast/) |

---

## Do / Don't

<!-- SCREENSHOTS UNAVAILABLE — no Figma examples page exists for Skeleton loader -->

### Pair 1 — Match the size to the text style being replaced

#### ✅ Do — Pick the `size` value whose pixel height matches the text style the skeleton replaces

> `SkeletonBlock` ships seven size values whose names encode both the height in pixels **and** the Oxygen text style they replace (e.g. `28px - heading01`, `20px - body01`, `16px - label01`). The naming is deliberate — it removes ambiguity for engineers and keeps the loaded and unloaded states the same height, so the layout doesn't jump when content arrives.

```tsx
import { SkeletonBlock } from '@8x8/oxygen-skeletons';

// A heading + two body lines, sized to match the real text
<SkeletonBlock size="28px - heading01" />
<SkeletonBlock size="20px - body01" />
<SkeletonBlock size="20px - body01" />
```

**Grounded in:** [`props.md`](./props.md) lines 74–83 (size values table — every value names the text style it replaces); [`SkeletonBlock-figma.md`](./SkeletonBlock-figma.md) lines 167–169 ("Size values mirror text style names: Each `size` value is named after the Oxygen text style it replaces … This makes it explicit which text style the skeleton should match, removing ambiguity for engineers."); [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — Text variant maps to `heading02 / heading01 / bulletList01 / body02 / body01 / label01`.

#### ❌ Don't — Pick an arbitrary height ("looks about right") or reuse a single size for everything

> Using `20px - body01` for a heading or `40px - heading02` for body copy makes the skeleton taller or shorter than the text it stands in for. When the real content paints, the page reflows visibly — the worst-feeling moment of a loading state.

```tsx
// ❌ Same size for everything — layout will shift on load
<SkeletonBlock size="20px - body01" />   {/* will be replaced by a heading */}
<SkeletonBlock size="20px - body01" />
<SkeletonBlock size="20px - body01" />
```

---

### Pair 2 — Use `custom - image` for images and blocks, not for text

#### ✅ Do — Use `custom - image` (240px) only when the placeholder stands in for an image or a block-level element

> The seventh size value (`custom - image`) renders at 240px and is intended for thumbnails, hero images, and other block-level placeholders. The Oxygen Block variant exists precisely for "images" — text has its own dedicated size values.

```tsx
import { SkeletonBlock } from '@8x8/oxygen-skeletons';

// Image / thumbnail placeholder
<SkeletonBlock size="custom - image" />
```

**Grounded in:** [`props.md`](./props.md) line 82 (`custom - image` row — "Replaces an image or block-level element"); [`SkeletonBlock-figma.md`](./SkeletonBlock-figma.md) lines 171–172 ("`custom - image` at 240px … In practice, the height should match the image or block being replaced"); [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — Block variant: "Block skeleton loaders are typically used for images."

#### ❌ Don't — Use `custom - image` to fill the area where body text will load

> A 240px-tall block standing in for a single paragraph misrepresents how much vertical space the real content will take, and exaggerates the perceived loading time. Use the text-style size values for text and reserve `custom - image` for actual images and block-level visuals.

---

### Pair 3 — Respect `spacing03` (8px) between stacked text-line skeletons

#### ✅ Do — Separate stacked text skeletons with `spacing03` (8px)

> When multiple text skeletons stack to fake a paragraph, use the `spacing03` token (8px) as the gap between them. This is the same spacing tokens that the loaded state uses, so the column height matches before and after content paints.

```tsx
<div style={{ display: 'flex', flexDirection: 'column', gap: '8px' }}>
  <SkeletonBlock size="28px - heading01" />
  <SkeletonBlock size="20px - body01" />
  <SkeletonBlock size="20px - body01" />
</div>
```

**Grounded in:** [`tokens.md`](./tokens.md) lines 54–56 (Spacing tokens: "Gap between text skeleton lines · `spacing03` · 8px"); [`examples.md`](./examples.md) lines 49 + 55 ("Use `spacing03` (8px) between lines"); [`SkeletonBlock-figma.md`](./SkeletonBlock-figma.md) lines 145–148 (Spacing guidance: "Between stacked text skeleton lines: `spacing03` = 8px"); [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — Padding and spacing: "When using multiple text skeleton loaders to make a paragraph the lines must use the spacing token `spacing03` (8px) between each line."

#### ❌ Don't — Tighten or stretch the gap with hardcoded values

> Pulling lines closer together (e.g. `gap: 2px`) or spreading them apart (`gap: 24px`) gives the loading state a different rhythm from the loaded state, so the column visibly jumps when content paints. Use `spacing03` and let the layout snap into place naturally.

---

### Pair 4 — Combine Block + Circle into one card skeleton

#### ✅ Do — Pair `SkeletonBlock` text lines with a `SkeletonCircle` avatar for cards and list rows

> Skeletons are most effective when their shape mirrors the loaded UI. For a contact row or comment card — avatar + name + secondary line — combine one `SkeletonCircle` for the avatar with two `SkeletonBlock` lines sized to the text styles they replace. The loaded layout snaps in without reflow.

```tsx
import { SkeletonBlock, SkeletonCircle } from '@8x8/oxygen-skeletons';

<div style={{ display: 'flex', alignItems: 'center', gap: '12px' }}>
  <SkeletonCircle size="40px - medium" />
  <div style={{ flex: 1, display: 'flex', flexDirection: 'column', gap: '8px' }}>
    <SkeletonBlock size="22px - body02" />
    <SkeletonBlock size="16px - label01" />
  </div>
</div>
```

**Grounded in:** [`examples.md`](./examples.md) lines 76–89 (Card skeleton — combined Block + Circle); [`SkeletonCircle/examples.md`](../SkeletonCircle/examples.md) lines 75–88 (mirror example for a contact row); [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — Best practices: "On large container-based components like tables or cards."

#### ❌ Don't — Try to replicate every detail of the loaded card (badges, icons, dividers)

> A skeleton's job is to convey "this region is loading" with enough shape that the page doesn't feel empty. Modelling every secondary icon, divider, and badge produces a noisy placeholder that often takes more effort than the loaded UI itself — and goes stale every time the real card design changes.

---

### Pair 5 — Communicate the loading state with `aria-busy`, not the shimmer alone

#### ✅ Do — Wrap the skeleton region in a container with `aria-busy="true"` (and an accessible name)

> `SkeletonBlock` is purely presentational — it renders as a styled `div` with no text, no role, and no tab stop. Screen readers will not announce it. Communicate the loading state programmatically on the parent region: `aria-busy="true"` while loading, plus either an `aria-label` or a visually-hidden live region.

```html
<div aria-busy="true" aria-label="Loading article">
  <SkeletonBlock size="28px - heading01" />
  <SkeletonBlock size="20px - body01" />
  <SkeletonBlock size="20px - body01" />
</div>
```

**Grounded in:** [`accessibility.md`](./accessibility.md) lines 33–47 (ARIA role section — "parent container … should use `aria-busy='true'`" with code example); [`accessibility.md`](./accessibility.md) lines 60–65 (Screen reader guidance — "communicate via the parent: `aria-busy`, `aria-label`, or a visually-hidden live region"); [`accessibility.md`](./accessibility.md) line 86 (WCAG 4.1.3 Status Messages — "Loading state must be communicated programmatically · Requires `aria-busy` on parent").

#### ❌ Don't — Rely on the shimmer animation as the only loading cue

> The fade between `ui01` and `ui02` is purely visual. A non-sighted user, a user on a low-bandwidth connection where the animation stutters, or a user who has disabled motion will receive no signal at all that the region is loading. Without `aria-busy` (or an equivalent live-region announcement) on the parent, the page reads as "empty" — not "loading".

---

### Pair 6 — Honour `prefers-reduced-motion`

#### ✅ Do — Verify the skeleton animation pauses (or is removed) when the user has requested reduced motion

> The Oxygen skeleton animation transitions the fill between `ui01` and `ui02`. Animations that loop indefinitely can trigger vestibular discomfort for some users, which is why the OS / browser preference `prefers-reduced-motion: reduce` exists. Confirm in `@media (prefers-reduced-motion: reduce)` that the skeleton renders as a static `ui02` rectangle — no fade.

**Grounded in:** [`accessibility.md`](./accessibility.md) lines 70–74 (Animation considerations: "Check `@media (prefers-reduced-motion: reduce)` — the animation should pause or be removed in this context."); [`accessibility.md`](./accessibility.md) line 87 (WCAG 2.3.3 Animation from Interactions — "Skeleton animation should respect `prefers-reduced-motion`"); [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — Behavior: "Skeleton loading has an animation that transitions from one color to another to look like a smooth in/out fade when alternating the colors from `ui01` to `ui02`."

#### ❌ Don't — Ship custom CSS that re-enables the shimmer for everyone

> Wrapping the skeleton in a parent that re-applies its own `@keyframes` animation, or overriding the Oxygen styles to force motion, undoes the package's reduced-motion behaviour. Any custom shimmer must itself be wrapped in `@media (prefers-reduced-motion: no-preference)`.

---

## Gaps & open questions

| ID | Type | Description |
|----|------|-------------|
| — | Editorial | These Do/Don't pairs are authored from extracted artifacts and the public oxygen.8x8.com Skeleton loader usage page, not from a Figma examples page. They should be reviewed by a designer and replaced with Figma-sourced pairs once a `↳ Skeleton loader examples` page is created. |
| GAP-USAGE-001 | Source gap | No Figma examples page exists for the Skeleton loader family. The public usage page at [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) documents variants, spacing, and "When to use / not to use" but contains **no Do/Don't cards, no accessibility guidance, and no failure / timeout guidance**. A Figma examples page would let `figma-extract-usage` run and replace this editorial draft. |
| GAP-USAGE-002 | Source gap | No guidance exists for **maximum / minimum display time**. If real content paints in <100ms, the skeleton flashes and feels worse than a brief delay; if loading exceeds a few seconds, the user may interpret the shimmer as a frozen UI. Confirm whether the design system has a recommended threshold (e.g. show only after 200ms, hide after 5s and switch to an error state). |
| GAP-USAGE-003 | Source gap | The OX usage page treats Block, Circle and Text as three variants of one component, but the Oxygen React API exposes two components (`SkeletonBlock`, `SkeletonCircle`) — Text is handled by `SkeletonBlock` size values. The published page and the API drift on naming. Confirm whether a future API change introduces a separate `SkeletonText` export or whether the published page should be re-aligned. |
| CONFLICT-001 | Conflict (inherited from [`SkeletonBlock-audit.md`](./SkeletonBlock-audit.md) GAP-001) | The `size` prop values for `SkeletonCircle` are documented in two incompatible formats across the SkeletonBlock and SkeletonCircle folders. This usage file uses the **Figma axis format** (`"40px - medium"`) consistently to match this folder's own `props.md` and `examples.md`. The CONFLICT remains open and must be resolved against the `@8x8/oxygen-skeletons` package source before doc-rewrite can proceed. |

---

_Source: editorial guidance authored from extracted artifacts (props.md, examples.md, accessibility.md, tokens.md, SkeletonBlock-figma.md, SkeletonBlock-audit.md) and the public usage page at oxygen.8x8.com/components/skeletonloader/usage · No Figma examples page available · 2026-05-14_
