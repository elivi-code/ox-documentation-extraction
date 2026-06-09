---
component: SkeletonCircle
package: "@8x8/oxygen-skeletons"
category: feedback_status
role: usage
role_description: "Usage guidelines — editorially authored from extracted artifacts and the public Oxygen Skeleton loader usage page; no Figma examples page exists"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from extracted artifacts + oxygen.8x8.com/components/skeletonloader/usage — NOT from Figma Do/Don't frames. Re-run doc-audit after creation; replace pairs with figma-extract-usage output when a Figma examples page exists. Shared family with SkeletonBlock."
source_type: editorial
audit_verdict: null
siblings:
  - "[[SkeletonCircle/props]]"
  - "[[SkeletonCircle/examples]]"
  - "[[SkeletonCircle/tokens]]"
  - "[[SkeletonCircle/accessibility]]"
  - "[[SkeletonCircle/SkeletonCircle-figma]]"
  - "[[SkeletonCircle/SkeletonCircle-audit]]"
  - "[[SkeletonBlock/SkeletonBlock-usage]]"
tags:
  - oxygen
  - component/SkeletonCircle
  - role/usage
  - stage/editorial
  - category/feedback_status
---
<!-- SOURCE: editorial — no Figma "↳ Skeleton loader examples" page exists -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- REFERENCE PAGE: https://oxygen.8x8.com/components/skeletonloader/usage -->
<!-- GROUNDING: full — props.md, examples.md, accessibility.md, tokens.md, SkeletonCircle-figma.md, SkeletonCircle-audit.md, oxygen.8x8.com/components/skeletonloader/usage -->
<!-- DRAFTED: 2026-05-14 -->
<!-- MODE: open -->
<!-- PAIRS: 6 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma examples page is created -->

# Skeleton Circle — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [SkeletonCircle-figma.md](./SkeletonCircle-figma.md) ·
> [SkeletonBlock-usage.md](../SkeletonBlock/SkeletonBlock-usage.md)

> **Editorial guidance — not Figma-sourced.** No `↳ Skeleton loader examples` Figma page exists, so `figma-extract-usage` cannot run. The Do/Don't pairs below are inferred from `props.md`, `examples.md`, `accessibility.md`, `tokens.md`, `SkeletonCircle-figma.md`, and the public usage page at [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage). Treat as provisional until a designer reviews them. Replace with `figma-extract-usage` output when a Figma examples page is created.

`SkeletonCircle` is a fully-rounded content placeholder that appears while an **avatar** or **individual icon** is loading. It is one half of the Oxygen skeleton family — pair it with [`SkeletonBlock`](../SkeletonBlock/SkeletonBlock-usage.md) for text-line and image placeholders in the same layout. Both components fade between the `ui01` and `ui02` tokens to convey activity until the real content paints.

---

## When to use

- Replacing an **avatar** (xlarge / large / medium / small — 80px → 28px) while a user, contact, or profile loads ([oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — Circle: "used for avatars and individual icons").
- Replacing an **individual icon** in a small slot (24px → 16px) — toolbar, list-item leading icon, status indicator.
- The loaded element is **round** in the design — circle skeletons must visually match circular avatars, not square thumbnails.
- The page or list is **incrementally loading** and a circular placeholder keeps the row layout stable until the avatar arrives.

## When not to use

| Situation | Use instead |
|-----------|-------------|
| The element being loaded is an **image, thumbnail, or hero**, not an avatar | [`SkeletonBlock`](../SkeletonBlock/SkeletonBlock-usage.md) with `size="custom - image"` |
| The element is a **text line** | [`SkeletonBlock`](../SkeletonBlock/SkeletonBlock-usage.md) with the text-style size value |
| The container content cannot be predicted at all | [Spinner](../Spinner/) — indeterminate loading indicator (per [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — "When the container content cannot be determined.") |
| Loading is happening inside a **menu, dropdown, or modal** | Spinner — per [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — "To represent content in menus, dropdowns, or modals." |
| You have a real percentage (0–100%) | [Progress Bar](../ProgressBar/ProgressBar-usage.md) |

---

## Do / Don't

<!-- SCREENSHOTS UNAVAILABLE — no Figma examples page exists for Skeleton loader -->

### Pair 1 — Match the diameter to the avatar or icon size being replaced

#### ✅ Do — Pick the `size` value whose diameter matches the loaded avatar / icon slot

> `SkeletonCircle` ships nine diameter values: `80px - xlarge`, `48px - large`, `40px - medium`, `32px - small`, `28px - small`, and four `xsmall` variants at 24/22/20/16px. Use the one that matches the avatar tier the skeleton is replacing, so the row keeps its height when the real avatar paints.

```tsx
import { SkeletonCircle } from '@8x8/oxygen-skeletons';

// Profile header — extra-large avatar
<SkeletonCircle size="80px - xlarge" />

// Standard contact-list avatar
<SkeletonCircle size="48px - large" />

// Compact list / chat avatar
<SkeletonCircle size="40px - medium" />
```

**Grounded in:** [`props.md`](./props.md) lines 74–84 (size values table with "Intended use" column: xlarge avatar → 80px, large avatar → 48px, medium avatar → 40px, etc.); [`SkeletonCircle-figma.md`](./SkeletonCircle-figma.md) lines 172–174 ("Size names reference avatar/icon context: Each size value encodes both the pixel dimension and the semantic size label … making it clear which avatar or icon slot the skeleton replaces."); [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — Circle variant size list (9 variants from 80px down to 16px).

#### ❌ Don't — Default every avatar to the same diameter regardless of slot

> Rendering a 40px `medium` circle in a slot that will load an 80px header avatar means the page reflows when the real avatar paints — the header row visibly grows. Pick the size that matches the loaded slot, even if it means using a different value per region.

```tsx
// ❌ Same size everywhere — the header avatar will jump on load
<SkeletonCircle size="40px - medium" />   {/* header — should be 80px */}
<SkeletonCircle size="40px - medium" />   {/* list row — correct */}
```

---

### Pair 2 — Use Circle for avatars and individual icons only

#### ✅ Do — Reserve `SkeletonCircle` for **avatars** and **individual icons**

> The Oxygen Skeleton family has two shape primitives because real UI has two shape primitives: round avatars/icons (Circle) and rectangular text/images (Block). Use them the same way — never as interchangeable.

```tsx
import { SkeletonBlock, SkeletonCircle } from '@8x8/oxygen-skeletons';

// ✅ Avatar skeleton
<SkeletonCircle size="48px - large" />

// ✅ Square thumbnail / image — use SkeletonBlock instead
<SkeletonBlock size="custom - image" />
```

**Grounded in:** [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — Circle variant: "Circle skeleton loaders are used for avatars and individual icons."; Block variant: "Block skeleton loaders are typically used for images."; [`SkeletonCircle-figma.md`](./SkeletonCircle-figma.md) lines 176 ("Shared token with Block: Both `SkeletonBlock` and `SkeletonCircle` use `--ui/ui02` as the fill token") — the two are siblings, not substitutes.

#### ❌ Don't — Use a large `SkeletonCircle` to stand in for a square image or thumbnail

> Showing a circle where a square will paint misrepresents the shape of the loaded UI. The user will see the layout transform from round to square when the real content arrives — visually jarring and not what the design system intends.

---

### Pair 3 — Keep one diameter per list or grid

#### ✅ Do — Use a single, consistent diameter across every row of a list or grid

> A contact list or chat history renders all avatars at the same size. The skeleton should mirror that — every row uses the **same** `SkeletonCircle` size so the loading state reads as a single rhythmic column, not a noisy mix of bubble sizes.

```tsx
// ✅ Contact list — every row uses 40px - medium
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

**Grounded in:** [`examples.md`](./examples.md) lines 75–88 (Combined contact-row example — single `40px - medium` per row); [`SkeletonCircle-figma.md`](./SkeletonCircle-figma.md) lines 174–175 ("Two `small` and four `xsmall` values … pixel values are the disambiguating factor" — the same row should pick one and stick with it); [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — Best practices: "On large container-based components like tables or cards."

#### ❌ Don't — Mix sizes within one collection

> Rendering some rows with `48px - large` and others with `28px - small` produces a loading state that doesn't predict the loaded state. When the real avatars paint at one consistent size, every row reflows independently.

---

### Pair 4 — Pair Circle with adjacent Block lines for rows

#### ✅ Do — Combine `SkeletonCircle` with `SkeletonBlock` lines for contact rows, comment cards, and list items

> `SkeletonCircle` rarely stands alone — it represents the avatar slot in a row that also has a name and a secondary line. Wrap one circle and two blocks in a flex row to skeleton the entire pattern: avatar, name, status / timestamp.

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

**Grounded in:** [`examples.md`](./examples.md) lines 75–88 ("Combined with SkeletonBlock (contact row)" example); [`SkeletonBlock/examples.md`](../SkeletonBlock/examples.md) lines 76–89 (mirror Card-skeleton example combining both components); [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — Padding and spacing: "The spacing tokens used in the 'loaded' state will be used as default to separate different variants of skeleton loaders."

#### ❌ Don't — Use a lone `SkeletonCircle` where the loaded UI has a circle **and** text

> A row that loads as "avatar + name + status" but is skeletoned as a single circle leaves a large blank space to the right of the circle. The skeleton fails to preserve the row's layout, so the page jumps on load. Pair the circle with `SkeletonBlock` text lines to mirror the full row.

---

### Pair 5 — Announce loading on the parent, not on each skeleton

#### ✅ Do — Set `aria-busy="true"` (plus an accessible name) on the **parent container**, once per loading region

> `SkeletonCircle` is purely presentational — a styled `div` with no role, no text, and no tab stop. Screen readers will not announce it. Communicate loading on the **parent** that wraps the row (or the whole list) — once, not per skeleton.

```html
<ul aria-busy="true" aria-label="Loading contacts">
  <li>
    <SkeletonCircle size="40px - medium" />
    <SkeletonBlock size="20px - body01" />
  </li>
  <li>
    <SkeletonCircle size="40px - medium" />
    <SkeletonBlock size="20px - body01" />
  </li>
</ul>
```

**Grounded in:** [`accessibility.md`](./accessibility.md) lines 33–46 (ARIA role section — "parent container … should use `aria-busy='true'`" with code example); [`accessibility.md`](./accessibility.md) lines 60–64 (Screen reader guidance — "Communicate the loading state via the parent using `aria-busy`, `aria-label`, or a visually-hidden live region"); [`accessibility.md`](./accessibility.md) line 83 (WCAG 4.1.3 Status Messages — "Loading state must be communicated programmatically · Requires `aria-busy` on parent").

#### ❌ Don't — Add `aria-label="Loading"` or `role="status"` to every individual `SkeletonCircle`

> Putting a label on every skeleton causes screen readers to read "Loading. Loading. Loading. Loading. Loading…" across a 20-row list — drowning out the surrounding content and making the page unusable. One label on the parent region is correct; per-skeleton labels are noise.

---

### Pair 6 — Honour `prefers-reduced-motion`

#### ✅ Do — Verify the shimmer animation pauses (or is removed) when the user has requested reduced motion

> The skeleton animation fades the circle's fill between `ui01` and `ui02`. Looping animations can trigger vestibular discomfort, so the OS / browser preference `prefers-reduced-motion: reduce` exists to suppress them. Confirm in `@media (prefers-reduced-motion: reduce)` that the circle renders as a static `ui02` disc — no fade.

**Grounded in:** [`accessibility.md`](./accessibility.md) lines 68–72 (Animation considerations: "Verify the Oxygen skeleton CSS respects `@media (prefers-reduced-motion: reduce)`"); [`accessibility.md`](./accessibility.md) line 84 (WCAG 2.3.3 Animation from Interactions — "Skeleton animation should respect `prefers-reduced-motion`"); [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) — Behavior: "Skeleton loading has an animation that transitions from one color to another to look like a smooth in/out fade when alternating the colors from `ui01` to `ui02`."

#### ❌ Don't — Re-apply a custom shimmer in a parent stylesheet without gating on motion preferences

> Wrapping the skeleton in a parent that re-applies its own `@keyframes` overrides the Oxygen reduced-motion behaviour. Any custom shimmer animation must itself be wrapped in `@media (prefers-reduced-motion: no-preference)`.

---

## Gaps & open questions

| ID | Type | Description |
|----|------|-------------|
| — | Editorial | These Do/Don't pairs are authored from extracted artifacts and the public oxygen.8x8.com Skeleton loader usage page, not from a Figma examples page. They should be reviewed by a designer and replaced with Figma-sourced pairs once a `↳ Skeleton loader examples` page is created. |
| GAP-USAGE-001 | Source gap | No Figma examples page exists for the Skeleton loader family. The public usage page at [oxygen.8x8.com/components/skeletonloader/usage](https://oxygen.8x8.com/components/skeletonloader/usage) documents variants, spacing, and "When to use / not to use" but contains **no Do/Don't cards, no accessibility guidance, and no failure / timeout guidance**. A Figma examples page would let `figma-extract-usage` run and replace this editorial draft. |
| GAP-USAGE-002 | Source gap | The Circle variant ships **nine** sizes, but the `size` label vocabulary (`xlarge / large / medium / small / xsmall`) collapses them — two diameters share `small` (32px, 28px) and four share `xsmall` (24/22/20/16px). The Oxygen React API may have fewer enum values than the Figma axis exposes. Confirm against `@8x8/oxygen-skeletons` source. |
| GAP-USAGE-003 | Source gap | No guidance exists for **maximum / minimum display time**. If real content paints in <100ms, the skeleton flashes; if loading exceeds a few seconds, the user may interpret the shimmer as a frozen UI. Confirm whether the design system has a recommended threshold. |
| CONFLICT-001 | Conflict (inherited from [`SkeletonCircle-audit.md`](./SkeletonCircle-audit.md) GAP-001) | The `size` prop values for `SkeletonCircle` are documented in two incompatible formats across the SkeletonBlock and SkeletonCircle folders. This usage file uses the **Figma axis format** (`"40px - medium"`, `"80px - xlarge"`) consistently to match this folder's own `props.md` and `examples.md`. The CONFLICT remains open and must be resolved against the `@8x8/oxygen-skeletons` package source before doc-rewrite can proceed. |

---

_Source: editorial guidance authored from extracted artifacts (props.md, examples.md, accessibility.md, tokens.md, SkeletonCircle-figma.md, SkeletonCircle-audit.md) and the public usage page at oxygen.8x8.com/components/skeletonloader/usage · No Figma examples page available · 2026-05-14_
