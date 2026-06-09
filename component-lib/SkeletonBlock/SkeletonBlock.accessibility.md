---
parent: "[[SkeletonBlock]]"
section: accessibility
---

## Accessibility

> **DOC_GAP (GAP-010 — SKIP):** All guidance below is inferred from component type (passive/display). The Oxygen MCP returned no accessibility data for `SkeletonBlock` / `SkeletonCircle`, and no ARIA annotations were found in Figma. Guidance is correct by convention but unverified against the actual `@8x8/oxygen-skeletons` implementation. Verify the rendered DOM in a browser (check for any `role`, `aria-*`, or `tabIndex` attributes) and confirm `prefers-reduced-motion` CSS behaviour before treating this as authoritative.

---

## ARIA role

`SkeletonBlock` and `SkeletonCircle` are **purely presentational** — they carry no interactive meaning and render as simple styled divs.

- The components themselves should **not** be focusable.
- The **parent container** wrapping skeleton content should use `aria-busy="true"` while loading, and `aria-busy="false"` (or removed) once content is ready.
- Optionally add `aria-label="Loading..."` or a `role="status"` element to announce the loading state to screen readers.

```html
<!-- Recommended pattern for the loading container -->
<div aria-busy="true" aria-label="Loading content">
  <SkeletonBlock size="28px - heading01" />
  <SkeletonBlock size="20px - body01" />
</div>
```

---

## Keyboard interactions

None. Skeleton components are non-interactive and do not receive focus.

| Key | Behaviour |
|-----|-----------|
| Tab | Skipped — not in tab order |

---

## Screen reader guidance

- Skeleton components render no visible text; screen readers will not announce them unless their parent carries an accessible label.
- Communicate the loading state via the parent: `aria-busy`, `aria-label`, or a visually-hidden live region (e.g. `role="status"` + `aria-live="polite"`).
- Once content loads, remove or replace skeleton components with real content — screen readers will announce the updated content automatically via live-region semantics on the parent.

---

## Animation considerations

The skeleton animation transitions between `ui01` and `ui02` tokens. Users who have configured **"reduce motion"** (via OS or browser preference) may be affected:

- Check `@media (prefers-reduced-motion: reduce)` — the animation should pause or be removed in this context.
- Verify that the Oxygen skeleton CSS respects `prefers-reduced-motion`.

---

## WCAG 2.1 AA checklist

| Criterion | Requirement | Status |
|-----------|-------------|--------|
| 1.4.3 Contrast (Minimum) | Not applicable — skeleton is a decorative placeholder, not text | N/A |
| 1.4.11 Non-text Contrast | Skeleton shape against background should meet 3:1 ratio | Verify with theme tokens |
| 2.1.1 Keyboard | Non-interactive; must not capture focus | ✓ (inferred) |
| 2.4.3 Focus Order | Not in tab order | ✓ (inferred) |
| 4.1.3 Status Messages | Loading state must be communicated programmatically | Requires `aria-busy` on parent |
| 2.3.3 Animation from Interactions | Skeleton animation should respect `prefers-reduced-motion` | Verify in CSS |
