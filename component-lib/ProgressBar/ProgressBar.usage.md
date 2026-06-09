---
parent: "[[ProgressBar]]"
section: usage
component: ProgressBar
pipeline_stage: spec_ready
source_type: editorial
tags:
  - oxygen
  - component/ProgressBar
  - role/spoke
  - section/usage
---

<!-- source: editorial — no Figma "↳ ProgressBar examples" page exists (WARN-003) -->

> **Editorial guidance — not Figma-sourced.** No `↳ ProgressBar examples` Figma page exists; `figma-extract-usage` cannot run. Do/Don't pairs are inferred from `props.md`, `examples.md`, `accessibility.md`, `ProgressBar-figma.md`, and the public usage page at oxygen.8x8.com/components/progressbar/usage. Replace with `figma-extract-usage` output when a Figma examples page is created.

The Progress Bar communicates the status of an ongoing, determinate process through a horizontal fill. Use it when progress can be expressed as a percentage (0–100%) — for example, a file upload, download, or multi-step job whose completion percentage is known to the application.

## When to use

- Progress can be described with quantitative information — a known percentage between 0% and 100%.
- The process is **forward-only**: the bar fills progressively without decreasing or resetting until completion.
- The user benefits from seeing how close the process is to completing (uploads, downloads, multi-file imports, long-running jobs with measurable steps).
- A visible, persistent indicator of progress is desired — not a transient toast or a fully-blocking modal.

## When not to use

| Situation | Use instead |
|-----------|-------------|
| Progress cannot be quantified (loading time unknown, waiting on a remote response without a measurable step count) | [[Spinner]] — indeterminate loading indicator |
| A whole region of UI is being populated ("content is coming", not "X% done") | [[SkeletonBlock]] — content placeholder |
| A small inline area is loading and a horizontal bar would dominate the layout | Small [[Spinner]] |
| Status is an event, not an ongoing process ("File saved", "Connection restored") | [[Toast]] |
| Multiple discrete steps need to be visualized with step labels and a current-step indicator | Stepper / wizard pattern |

> Progress Bar has no indeterminate mode. If you don't have a real percentage to show, prefer [[Spinner]].

## Do / Don't

### Pair 1 — Determinate-only: use Progress Bar when you have a real percentage

**✅ Do** — Use Progress Bar when the application knows how much work is done and how much remains.

The `value` prop is a number between 0 and 100, exposed to assistive technology as `aria-valuenow`. The component only makes sense when the application can produce a meaningful number — for example, bytes uploaded ÷ total bytes, or completed steps ÷ total steps.

**❌ Don't** — Use Progress Bar to fake indeterminate loading.

Animating `value` in a loop, or driving it from a timer that doesn't reflect real progress, is dishonest feedback. If you don't know the completion percentage, use [[Spinner]] instead — it communicates "working on it" without claiming a percentage.

---

### Pair 2 — Accessible name: every bar needs one

**✅ Do** — Always provide an accessible name, ideally as visible `text`.

Progress Bar has no implicit accessible name from its visual content. Set it via the `text` prop (preferred — visible to all users) or, when no visible label is possible, `aria-label`. Use `aria-labelledby` when a heading or label already exists elsewhere in the DOM.

**❌ Don't** — Render `<ProgressBar value={progress} />` with no label.

An unlabelled progress bar fails WCAG 4.1.2 (Name, Role, Value). Screen reader users hear only the percentage, not what is loading — "50%" carries no meaning without context.

---

### Pair 3 — Don't rely on colour alone for state

**✅ Do** — Pair the visual fill change with text that confirms the state.

The bar's fill colour shifts from blue (`--actions/action04`) while loading to green (`--success/success01`) at completion. Colourblind users, users in high-glare conditions, and screen reader users cannot rely on that colour shift alone. Update the `text` label to confirm state in words ("Uploading…", then "Complete").

**❌ Don't** — Treat the green fill as sufficient feedback that the process finished.

If "the bar turned green" is the only signal of completion, users who cannot perceive that colour change will keep waiting.

---

### Pair 4 — Update cadence: don't flood screen readers

**✅ Do** — Throttle `value` updates to perceptible intervals (~every 5–10%).

The browser announces `aria-valuenow` on each change in most screen readers. Updating `value` on every animation frame or on every byte received produces excessive announcements that drown out the rest of the page.

**❌ Don't** — Bind `value` directly to a high-frequency source without debouncing.

A `value={progress}` that re-renders 60 times a second from a websocket or `requestAnimationFrame` loop will make the component unusable for screen reader users.

---

### Pair 5 — Completion label: switch the text when `value` reaches 100

**✅ Do** — Replace the loading message with a completion message when `value` is 100.

When the process finishes, swap "Loading data…" (or "Uploading…", "Importing…") for "Complete" or a specific success phrase. This gives screen reader users an audible confirmation and matches the green fill that the bar shows.

**❌ Don't** — Leave a "Loading…" label on a bar that has finished filling.

A green, full bar labelled "Loading…" sends contradictory signals: the visual says done; the text says still working. Update the `text` prop in the same render where `value` hits 100.

<!-- STUB:GAP-USAGE-002 source="Confirm with design whether failure state should be communicated via text-only swap on existing bar, or by switching to Toast/AlertBanner; add a 6th Do/Don't pair to ProgressBar.usage.md once decided" -->
