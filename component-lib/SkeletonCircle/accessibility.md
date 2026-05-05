# SkeletonCircle — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md) · [SkeletonCircle-figma.md](SkeletonCircle-figma.md)

---

> **DATA GAP:** The Oxygen MCP returned no explicit accessibility documentation for `SkeletonCircle`. The guidance below is inferred from component type (passive/display) and WCAG 2.1 AA requirements. No ARIA annotations were found in Figma.

---

## ARIA role

`SkeletonCircle` is a **purely presentational** component — it renders as a single styled div and carries no interactive meaning.

- The component itself should **not** be focusable.
- The **parent container** wrapping skeleton content should use `aria-busy="true"` while loading, and `aria-busy="false"` (or removed) once content is ready.
- Optionally add `aria-label="Loading..."` or a `role="status"` element to announce the loading state to screen readers.

```html
<!-- Recommended pattern -->
<div aria-busy="true" aria-label="Loading contact">
  <SkeletonCircle size="40px - medium" />
</div>
```

---

## Keyboard interactions

None. `SkeletonCircle` is non-interactive and does not receive focus.

| Key | Behaviour |
|-----|-----------|
| Tab | Skipped — not in tab order |

---

## Screen reader guidance

- `SkeletonCircle` renders no visible text; screen readers will not announce it unless its parent carries an accessible label.
- Communicate the loading state via the parent using `aria-busy`, `aria-label`, or a visually-hidden live region (`role="status"` + `aria-live="polite"`).
- Once content loads, replace the skeleton with the real component — screen readers will announce the updated content automatically.

---

## Animation considerations

The skeleton animation fades between `ui01` and `ui02`. Users with **"reduce motion"** configured (OS or browser) may be affected:

- Verify the Oxygen skeleton CSS respects `@media (prefers-reduced-motion: reduce)` — the animation should pause or be removed.

---

## WCAG 2.1 AA checklist

| Criterion | Requirement | Status |
|-----------|-------------|--------|
| 1.4.11 Non-text Contrast | Circle shape against background should meet 3:1 ratio | Verify with theme tokens |
| 2.1.1 Keyboard | Non-interactive; must not capture focus | ✓ (inferred) |
| 2.4.3 Focus Order | Not in tab order | ✓ (inferred) |
| 4.1.3 Status Messages | Loading state must be communicated programmatically | Requires `aria-busy` on parent |
| 2.3.3 Animation from Interactions | Skeleton animation should respect `prefers-reduced-motion` | Verify in CSS |

---

_Source: Oxygen MCP (no a11y data returned) · Inferred from component type · Extracted 2026-05-05_
