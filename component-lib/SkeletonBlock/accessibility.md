---
component: SkeletonBlock
package: "@8x8/oxygen-skeletons"
category: feedback_status
role: accessibility
role_description: "Accessibility — ARIA roles, keyboard interactions, and WCAG 2.1 AA guidance"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[SkeletonBlock/props]]"
  - "[[SkeletonBlock/examples]]"
  - "[[SkeletonBlock/tokens]]"
  - "[[SkeletonBlock/SkeletonBlock-figma]]"
  - "[[SkeletonBlock/SkeletonBlock-audit]]"
tags:
  - oxygen
  - component/SkeletonBlock
  - role/accessibility
  - stage/blocked
  - category/feedback_status
---
# SkeletonBlock — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md) · [SkeletonBlock-figma.md](SkeletonBlock-figma.md)

---

> **DATA GAP:** The Oxygen MCP returned no explicit accessibility documentation for `SkeletonBlock` / `SkeletonCircle`. The guidance below is inferred from component type (passive/display) and WCAG 2.1 AA requirements. No ARIA annotations were found in Figma.

---

## ARIA role

`SkeletonBlock` and `SkeletonCircle` are **purely presentational** components — they carry no interactive meaning and render as simple styled divs.

- The components themselves should **not** be focusable.
- The **parent container** that wraps skeleton content should use `aria-busy="true"` while loading, and `aria-busy="false"` (or removed) once content is ready.
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
- The loading state must be communicated via the parent: `aria-busy`, `aria-label`, or a visually-hidden live region (e.g. `role="status"` + `aria-live="polite"`).
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

---

_Source: Oxygen MCP (no a11y data returned) · Inferred from component type · Extracted 2026-05-05_
