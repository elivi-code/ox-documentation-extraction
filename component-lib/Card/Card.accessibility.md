---
parent: "[[Card]]"
section: accessibility
---

# Card — Accessibility

> ⚠️ **DEPRECATED** — `@8x8/oxygen-card` is deprecated. Accessibility documentation preserved for reference.

<!-- STUB:GAP-011 source="Verify ARIA role and keyboard behaviour from @8x8/oxygen-card component source or Storybook a11y addon. Confirm: (1) root element type, (2) aria-level default for Header, (3) whether Focus ring is the Card's own implementation or the consumer's. Replace inferred content with confirmed data." -->
> **SOURCE_GAP (GAP-011)** — All content below is **inferred** from the component's nature as a layout container. No ARIA role, keyboard interaction, or focus-management behaviour is confirmed from the MCP, component TypeScript, or Figma annotations. Specific unknowns: whether Card renders as a native semantic element or a `div`; whether the focus ring is implemented in CSS or via the Focus-ring sub-instance; the confirmed `aria-level` default for Header.

## ARIA roles & semantics

| Sub-component | Role / Semantics |
|---------------|-----------------|
| `Card` | No implicit ARIA role — renders as a generic container. If the card is interactive (clickable), the consuming element should carry `role="button"` or be an `<a>` / `<button>`. |
| `Card.Header` | `role="heading"` with `aria-level` (defaults to `3`). Set `aria-level` to match surrounding document heading hierarchy. |
| `Card.Separator` | Renders as a visual divider. No ARIA role specified in MCP data. |
| `Card.Statistics` | Display component — no interactive ARIA role required. |

## Keyboard interaction

The Card itself is not an interactive element. Interactivity (click to navigate) must be provided by the consuming application:

| Pattern | Recommendation |
|---------|---------------|
| Clickable card | Wrap in `<a>` (preferred for navigation) or `<button>` for in-page actions. Do not make a `<div>` clickable without `role="button"` and keyboard handling. |
| Focus order | Ensure focusable elements inside the card follow a logical DOM order. |
| CTA button | Cards should default to having a CTA — ensure it is keyboard-reachable and has a descriptive accessible label. |

## Screen reader guidance

- **Heading level**: `Card.Header` defaults to `aria-level="3"`. Adjust to avoid skipping heading levels if cards are nested under `<h1>` / `<h2>` sections.
- **Clickable card context**: If the entire card is a link, use a single `<a>` wrapper rather than nested interactive elements to avoid ambiguous tab stops.
- **Statistics**: Each statistic item should be readable in context. Ensure labels and values are meaningful when read aloud without visual grouping.

## WCAG 2.1 AA checklist

| Criterion | Guidance |
|-----------|----------|
| 1.3.1 Info and Relationships | Use `Card.Header` with correct `aria-level` to convey heading hierarchy programmatically. |
| 1.4.3 Contrast (Minimum) | `ui01`/`ui02`/`ui03` border tokens meet contrast for decorative borders; ensure card body text meets 4.5:1 against `ui02` background. |
| 2.1.1 Keyboard | If the card is interactive, all actions must be reachable and operable via keyboard alone. |
| 2.4.3 Focus Order | Tab order inside card must be logical and follow visual reading order. |
| 2.4.6 Headings and Labels | `Card.Header` text must be descriptive enough to identify card purpose out of context. |
| 4.1.2 Name, Role, Value | Interactive card wrappers must expose correct ARIA name (via `aria-label` or visible text) and role. |
