---
component: ProgressBar
package: "@8x8/oxygen-loaders"
category: feedback_status
role: usage
role_description: "Usage guidelines — editorially authored from extracted artifacts and the public Oxygen usage page; no Figma examples page exists"
pipeline_stage: editorial
pipeline_note: "Usage authored editorially from extracted artifacts + oxygen.8x8.com page — NOT from Figma Do/Don't frames. Re-run doc-audit after creation; replace pairs with figma-extract-usage output when a Figma examples page exists."
source_type: editorial
audit_verdict: null
siblings:
  - "[[ProgressBar/props]]"
  - "[[ProgressBar/examples]]"
  - "[[ProgressBar/tokens]]"
  - "[[ProgressBar/accessibility]]"
  - "[[ProgressBar/ProgressBar-figma]]"
  - "[[ProgressBar/ProgressBar-audit]]"
tags:
  - oxygen
  - component/ProgressBar
  - role/usage
  - stage/editorial
  - category/feedback_status
---
<!-- SOURCE: editorial — no Figma "↳ ProgressBar examples" page exists -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- REFERENCE PAGE: https://oxygen.8x8.com/components/progressbar/usage -->
<!-- GROUNDING: full — props.md, examples.md, accessibility.md, tokens.md, ProgressBar-figma.md, ProgressBar-audit.md, oxygen.8x8.com/components/progressbar/usage -->
<!-- DRAFTED: 2026-05-14 -->
<!-- MODE: open -->
<!-- PAIRS: 5 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma examples page is created -->

# Progress Bar — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [ProgressBar-figma.md](./ProgressBar-figma.md)

> **Editorial guidance — not Figma-sourced.** No `↳ ProgressBar examples` Figma page exists, so `figma-extract-usage` cannot run. The Do/Don't pairs below are inferred from `props.md`, `examples.md`, `accessibility.md`, `ProgressBar-figma.md`, and the public usage page at [oxygen.8x8.com/components/progressbar/usage](https://oxygen.8x8.com/components/progressbar/usage). Treat as provisional until a designer reviews them. Replace with `figma-extract-usage` output when a Figma examples page is created.

The Progress Bar communicates the status of an ongoing process through a determinate, horizontal fill. It is the right tool when progress can be expressed quantitatively (0–100%) — for example, a file upload, download, or multi-step job whose completion percentage is known to the application.

---

## When to use

- Progress can be described with quantitative information — a known percentage between 0% and 100%.
- The process is **forward-only**: the bar fills progressively without decreasing or resetting until completion (per [oxygen.8x8.com/components/progressbar/usage](https://oxygen.8x8.com/components/progressbar/usage)).
- The user benefits from seeing how close the process is to completing (uploads, downloads, multi-file imports, long-running jobs with measurable steps).
- A visible, persistent indicator of progress is desired — not a transient toast or a fully-blocking modal.

## When not to use

| Situation | Use instead |
|-----------|-------------|
| Progress cannot be quantified (loading time unknown, waiting on a remote response without a measurable step count) | [Spinner](../Spinner/) — indeterminate loading indicator |
| A whole region of UI is being populated and you want to communicate "content is coming" rather than "X% done" | [Skeleton loader](../SkeletonBlock/) — content placeholder |
| A small inline area (dropdown, menu cell, card body) is loading and a horizontal bar would dominate the layout | Small Spinner |
| Status is an event, not an ongoing process ("File saved", "Connection restored") | [Toast](../Toast/) |
| Multiple discrete steps need to be visualized with step labels and a current-step indicator | A stepper / wizard pattern (not provided by `@8x8/oxygen-loaders`) |

> Progress Bar has no indeterminate mode. If you don't have a real percentage to show, prefer Spinner.

---

## Do / Don't

<!-- SCREENSHOTS UNAVAILABLE — no Figma examples page exists for ProgressBar -->

### Pair 1 — Determinate-only: use Progress Bar when you have a real percentage

#### ✅ Do — Use Progress Bar when the application knows how much work is done and how much remains

> The `value` prop is a number between 0 and 100, exposed to assistive tech as `aria-valuenow` with `aria-valuemin="0"` and `aria-valuemax="100"`. The component only makes sense when the application can produce a meaningful number — for example, bytes uploaded ÷ total bytes, or completed steps ÷ total steps.

**Grounded in:** [`accessibility.md`](./accessibility.md) lines 29–34 (`role="progressbar"`, `aria-valuenow`, `aria-valuemin=0`, `aria-valuemax=100`); [`props.md`](./props.md) line 56 (`value` is "Percentage of completed progress (0–100)"); [oxygen.8x8.com/components/progressbar/usage](https://oxygen.8x8.com/components/progressbar/usage) — "when the progress can be described with quantitative information such as percentages (0% to 100%)".

#### ❌ Don't — Use Progress Bar to fake indeterminate loading

> Animating `value` in a loop, or driving it from a timer that doesn't reflect real progress, is dishonest feedback. The user reads the bar as a promise about how close they are to done. If you don't know that number, use a Spinner instead — it communicates "we're working on it" without claiming a percentage.

---

### Pair 2 — Accessible name: every bar needs one

#### ✅ Do — Always provide an accessible name, ideally as visible `text`

> Progress Bar has no implicit accessible name from its visual content. Set it via the `text` prop (preferred — visible to all users) or, when no visible label is possible, `aria-label`. Use `aria-labelledby` when a heading or label already exists elsewhere in the DOM.

**Grounded in:** [`accessibility.md`](./accessibility.md) lines 36–51 (Labelling table and code example: "an accessible name must always be provided through one of: `aria-label` / `aria-labelledby` / `text` prop"); [`examples.md`](./examples.md) lines 38–40 (every example pairs the bar with either `text` or `aria-label`).

#### ❌ Don't — Render `<ProgressBar value={progress} />` with no label

> An unlabelled progress bar fails WCAG 4.1.2 (Name, Role, Value). Screen reader users hear only the percentage, not what is loading — so "50%" carries no meaning. This also makes the bar harder to test and to localise.

---

### Pair 3 — Don't rely on colour alone for state

#### ✅ Do — Pair the visual fill change with text that confirms the state

> The bar's fill colour shifts from blue (`--actions/action04`) while loading to green (`--success/success01`) at completion. Some users — colourblind users, users in high-glare conditions, screen reader users — cannot rely on that colour shift. Update the `text` label to confirm the state in words ("Uploading…", then "Complete").

**Grounded in:** [`accessibility.md`](./accessibility.md) line 68 (WCAG 1.4.1 Use of Color: "Progress fill must not be the sole indicator of state — pair with `text` or `aria-label`"); [`ProgressBar-figma.md`](./ProgressBar-figma.md) lines 159–163 (status transition table: loading → blue fill; complete → green fill).

#### ❌ Don't — Treat the green fill as sufficient feedback that the process finished

> If "the bar turned green" is the only signal of completion, users who can't perceive that colour change will keep waiting. They will also miss it on a small bar or in a dense layout where the colour is not the focal element.

---

### Pair 4 — Update cadence: don't flood screen readers

#### ✅ Do — Throttle `value` updates to perceptible intervals (~every 5–10%)

> The browser will announce `aria-valuenow` on each change in most screen readers. Updating `value` on every animation frame, or on every byte received, produces a barrage of announcements that drowns out the rest of the page.

**Grounded in:** [`accessibility.md`](./accessibility.md) line 60: "Avoid updating `value` too rapidly (e.g. every render frame) as this can produce excessive announcements. Debounce updates to a perceptible interval (e.g. every 5–10%)."

#### ❌ Don't — Bind `value` directly to a high-frequency source without debouncing

> A `value={progress}` that re-renders 60 times a second from a websocket or `requestAnimationFrame` loop will make the component unusable for screen reader users. Debounce or snap the value to coarser steps before passing it in.

---

### Pair 5 — Completion label: switch the text when `value` reaches 100

#### ✅ Do — Replace the loading message with a completion message when `value` is 100

> When the process finishes, swap "Loading data…" (or "Uploading…", "Importing…") for "Complete" or a similarly specific success phrase. This gives screen reader users an audible confirmation and matches the green fill that the bar already shows.

**Grounded in:** [`accessibility.md`](./accessibility.md) line 61: "When progress completes (`value={100}`), update `text` to a completion message (e.g. `'Complete'`) so screen reader users receive confirmation." [`examples.md`](./examples.md) lines 60–62 — `Complete states` example pairs `value={100}` with `text="Complete"`.

#### ❌ Don't — Leave a "Loading…" label on a bar that has finished filling

> A green, full bar labelled "Loading…" sends contradictory signals: the visual says done; the text says still working. Screen reader users hear only the stale label. Update the `text` prop in the same render where `value` hits 100.

---

## Gaps & open questions

| ID | Type | Description |
|----|------|-------------|
| — | Editorial | These Do/Don't pairs are authored from extracted artifacts and the public oxygen.8x8.com usage page, not from a Figma examples page. They should be reviewed by a designer and replaced with Figma-sourced pairs once a `↳ ProgressBar examples` page is created. |
| GAP-USAGE-001 | Source gap | The public usage page ([oxygen.8x8.com/components/progressbar/usage](https://oxygen.8x8.com/components/progressbar/usage)) does not currently document explicit Do/Don'ts, accessibility guidance, or "When not to use" rules. The Spinner usage page is significantly more developed and contains the inverse rule ("when there is a determinate value, use a progress bar"). The Progress Bar page could be uplifted to match. |
| GAP-USAGE-002 | Source gap | No guidance exists on how to surface a **failure** state. The Figma component set models only `loading` and `complete` (see [`ProgressBar-figma.md`](./ProgressBar-figma.md) lines 159–163). Confirm whether failure should be communicated by leaving the bar at its last `value` and switching `text` to an error message, or by switching to a different component (Toast / AlertBanner). |
| GAP-USAGE-003 | Source gap | Behaviour for forward-only progress is documented prose-only on oxygen.8x8.com ("fills progressively without decreasing or resetting until completion"). The Oxygen API does not enforce this — `value` can be decremented freely. Confirm whether a Do/Don't pair against backwards / resetting progress should be added. |
| CONFLICT-001 | Conflict (inherited from `ProgressBar-figma.md`) | Figma exposes separate `loadingText` and `completeText` text properties; Oxygen exposes a single `text: string` prop. Pair 5 above resolves this for the editorial layer (consumers swap the string when `value` reaches 100), but the API mismatch persists and should be flagged in any future Figma examples page. |

---

_Source: editorial guidance authored from extracted artifacts (props.md, examples.md, accessibility.md, ProgressBar-figma.md, ProgressBar-audit.md) and the public usage page at oxygen.8x8.com/components/progressbar/usage · No Figma examples page available · 2026-05-14_
