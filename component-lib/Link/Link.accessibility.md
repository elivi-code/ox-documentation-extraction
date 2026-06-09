---
component: Link
parent: "[[Link]]"
section: accessibility
pipeline_stage: draft
siblings:
  - "[[Link.props]]"
  - "[[Link.anatomy]]"
  - "[[Link.tokens]]"
  - "[[Link.usage]]"
  - "[[Link.platform]]"
  - "[[Link.composition]]"
tags:
  - oxygen
  - component/Link
  - role/spoke-accessibility
---

<!-- STUB:GAP-019 source="Cross-reference this file against official Oxygen docs at https://oxygen.8x8.com/docs/components/textlink/usage for any official a11y guidance. Update any inferences that conflict with official statements." -->

## ARIA roles and semantics

| Element | Role | Notes |
|---------|------|-------|
| Root element | `link` (implicit via `<a>`) | Native `<a>` with `href` conveys `role="link"` automatically |
| Icon (if present) | Decorative | Icon should be `aria-hidden="true"` when paired with visible text |

## Keyboard interactions

| Key | Behavior |
|-----|----------|
| `Tab` | Moves focus to the link |
| `Shift + Tab` | Moves focus away from the link |
| `Enter` | Activates the link (follows `href`) |

## Focus management

- The link renders a native `<a>` element, natively focusable when `href` is provided.
- Focus ring is visible in the Focus and Active states — two concentric rings: inner border (`$ui06`/`$ui07`) matching the surface, outer 2px shadow (`$focus01`/`$focus02`).
- Do not suppress the focus outline via CSS; it must remain visible for keyboard users.

## Screen reader guidance

- Use descriptive link text. Avoid "click here", "read more", or "learn more" without context — screen readers may list links out of context.
- When the link opens a new tab/window (`target="_blank"`), add `aria-label` or visually hidden text: e.g. `"Getting started guide (opens in new tab)"`.
- If the link contains only an icon and no visible text, provide `aria-label` on the `<Link>` element.
- Visited links must remain identifiable — `$textColor08` provides the visited colour distinction.

## Color and contrast

| State | Token | Light contrast | Dark contrast |
|-------|-------|----------------|---------------|
| Default | `$action08` (`#0056E0` on white) | ≥ 4.5:1 | — |
| Hover | `$hover07` (`#246FE5`) | Check against surface | — |
| Visited | `$textColor08` (`#73348C`) | unverified | — |

<!-- SKIP:GAP-020 manual="Depends on GAP-012 resolution — compute contrast ratios for action08/hover15/textColor08 on ui01 once hover token conflict is resolved." -->

## WCAG 2.1 AA checklist

| Criterion | Requirement | Status |
|-----------|-------------|--------|
| 1.4.1 Use of Color | Links must not rely solely on color to distinguish from surrounding text | Underline or other non-color indicator required for inline links at rest |
| 1.4.3 Contrast (Minimum) | Text contrast ≥ 4.5:1 | Verify `$action08` against background surface |
| 2.1.1 Keyboard | All functionality available via keyboard | ✓ Native `<a>` is keyboard accessible |
| 2.4.4 Link Purpose (In Context) | Link purpose clear from label or context | ✓ Enforced by content guidelines |
| 2.4.7 Focus Visible | Focus indicator must be visible | ✓ Focus state documented |
| 4.1.2 Name, Role, Value | Interactive elements have accessible name | ✓ Via `children` text or `aria-label` |

## Chat surface note

When `isChat` is true, the link color changes to `$action07`. Ensure this token meets 4.5:1 contrast against the chat bubble surface (`$ui13`/`$ui14`).
