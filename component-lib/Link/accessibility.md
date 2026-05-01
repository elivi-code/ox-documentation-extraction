# Link — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md)

> **Data gap:** The Oxygen MCP returned no explicit accessibility documentation for this component. The guidance below is inferred from the component's interactive nature (wraps `<a>`), standard HTML semantics, and WCAG 2.1 AA requirements.

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

- The link renders a native `<a>` element, which is natively focusable when `href` is provided.
- Focus ring is visible on the focus state (see States in [props.md](props.md)).
- Do not suppress the focus outline via CSS — it must remain visible for keyboard users.

## Screen reader guidance

- Use descriptive link text. Avoid "click here", "read more", or "learn more" without context — screen readers may list links out of context.
- When the link opens a new tab/window (`target="_blank"`), add `aria-label` or visually hidden text to announce this: e.g. `"Getting started guide (opens in new tab)"`.
- If the link contains only an icon and no visible text, provide `aria-label` on the `<Link>` element.
- Visited links must remain identifiable — `$textColor08` provides the visited colour distinction.

## Color and contrast

| State | Token | Light contrast* | Dark contrast* |
|-------|-------|----------------|----------------|
| Default | `$action08` (`#0056E0` on white) | ≥ 4.5:1 | — |
| Hover | `$hover07` (`#246FE5`) | Check against surface | — |
| Visited | `$textColor08` (`#73348C`) | Check against surface | — |

*Exact contrast ratios depend on surface background. Verify with a contrast checker against `$ui01`/`$ui02`.

## WCAG 2.1 AA checklist

| Criterion | Requirement | Status |
|-----------|-------------|--------|
| 1.4.1 Use of Color | Links must not rely solely on color to distinguish from surrounding text | Underline or other non-color indicator required for inline links |
| 1.4.3 Contrast (Minimum) | Text contrast ≥ 4.5:1 | Verify `$action08` against background |
| 2.1.1 Keyboard | All functionality available via keyboard | ✓ Native `<a>` is keyboard accessible |
| 2.4.4 Link Purpose (In Context) | Link purpose clear from label or context | ✓ Enforced by content guidelines |
| 2.4.7 Focus Visible | Focus indicator must be visible | ✓ Focus state documented |
| 4.1.2 Name, Role, Value | Interactive elements have accessible name | ✓ Via `children` text or `aria-label` |

## Chat surface note

When `isChat` is true, the link color changes to `$action07`. Ensure this token also meets 4.5:1 contrast against the chat bubble surface (`$ui13`/`$ui14`).

_Source: Oxygen MCP · Extracted 2026-05-01_
