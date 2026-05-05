# Card — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md)

> ⚠️ **DEPRECATED** — `@8x8/oxygen-card` is deprecated. Accessibility documentation preserved for reference.

## ARIA Roles & Semantics

| Sub-component | Role / Semantics |
|---------------|-----------------|
| `Card` | No implicit ARIA role — renders as a generic container. If the card is interactive (clickable), the consuming element should carry `role="button"` or be a `<a>` / `<button>`. |
| `Card.Header` | `role="heading"` with `aria-level` (defaults to `3`). Set `aria-level` to match surrounding document heading hierarchy. |
| `Card.Separator` | Renders as a visual divider. No ARIA role specified in MCP data. |
| `Card.Statistics` | Display component — no interactive ARIA role required. |

## Keyboard Interaction

The Card itself is not an interactive element. Interactivity (click to navigate) must be provided by the consuming application:

| Pattern | Recommendation |
|---------|---------------|
| Clickable card | Wrap in `<a>` (preferred for navigation) or `<button>` for in-page actions. Do not make a `<div>` clickable without `role="button"` and keyboard handling. |
| Focus order | Ensure focusable elements inside the card follow a logical DOM order. |
| CTA button | Cards should default to having a CTA — ensure it is keyboard-reachable and has a descriptive accessible label. |

## Screen Reader Guidance

- **Heading level**: `Card.Header` defaults to `aria-level="3"`. Adjust this to avoid skipping heading levels if cards are nested under `<h1>` / `<h2>` sections.
- **Clickable card context**: If the entire card is a link, use a single `<a>` wrapper rather than nested interactive elements to avoid ambiguous tab stops.
- **Statistics**: Each statistic item should be readable in context. Ensure labels and values are meaningful when read aloud without visual grouping.

## WCAG 2.1 AA Checklist

| Criterion | Guidance |
|-----------|----------|
| 1.3.1 Info and Relationships | Use `Card.Header` with correct `aria-level` to convey heading hierarchy programmatically. |
| 1.4.3 Contrast (Minimum) | `ui01`/`ui02`/`ui03` border tokens meet contrast for decorative borders; ensure card body text meets 4.5:1 ratio against `ui02` background. |
| 2.1.1 Keyboard | If the card is interactive, all actions must be reachable and operable via keyboard alone. |
| 2.4.3 Focus Order | Tab order inside card must be logical and follow visual reading order. |
| 2.4.6 Headings and Labels | `Card.Header` text must be descriptive enough to identify card purpose out of context. |
| 4.1.2 Name, Role, Value | Interactive card wrappers must expose correct ARIA name (via `aria-label` or visible text) and role. |

---

_Source: Oxygen MCP · Extracted 2026-05-05_
