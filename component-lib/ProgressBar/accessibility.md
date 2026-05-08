---
component: ProgressBar
package: "@8x8/oxygen-loaders"
category: feedback_status
role: accessibility
role_description: "Accessibility — ARIA roles, keyboard interactions, and WCAG 2.1 AA guidance"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[ProgressBar/props]]"
  - "[[ProgressBar/examples]]"
  - "[[ProgressBar/tokens]]"
  - "[[ProgressBar/ProgressBar-figma]]"
  - "[[ProgressBar/ProgressBar-audit]]"
tags:
  - oxygen
  - component/ProgressBar
  - role/accessibility
  - stage/spec_ready
  - category/feedback_status
---
# ProgressBar — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md)

## ARIA role

`ProgressBar` is a passive display component. It renders with `role="progressbar"` and exposes progress state to assistive technologies via:

- `aria-valuenow` — current `value` (0–100)
- `aria-valuemin` — `0`
- `aria-valuemax` — `100`

## Labelling

Because `ProgressBar` has no implicit text label rendered inside the interactive element, an accessible name must always be provided through one of:

| Method | When to use |
|--------|-------------|
| `aria-label` | When no visible label is adjacent (most common) |
| `aria-labelledby` | When a visible heading or label element exists elsewhere in the DOM |
| `text` prop | Provides a visible label below the bar; also satisfies the accessible name requirement |

```tsx
{/* Preferred: visible text label */}
<ProgressBar value={50} text="Uploading files..." />

{/* When no visible text is possible */}
<ProgressBar value={50} aria-label="Loading 50%" />
```

## Keyboard interaction

`ProgressBar` is not keyboard-focusable. It conveys read-only status information; no keyboard interaction is required or expected.

## Screen reader guidance

- The `role="progressbar"` with `aria-valuenow` is announced when the component first renders and on value changes in most screen readers.
- Avoid updating `value` too rapidly (e.g. every render frame) as this can produce excessive announcements. Debounce updates to a perceptible interval (e.g. every 5–10%).
- When progress completes (`value={100}`), update `text` to a completion message (e.g. `"Complete"`) so screen reader users receive confirmation.

## WCAG 2.1 AA checklist

| Criterion | Requirement | Notes |
|-----------|-------------|-------|
| 1.3.1 Info and Relationships | Pass | `role="progressbar"` conveys semantics programmatically |
| 1.4.1 Use of Color | Review | Progress fill must not be the sole indicator of state — pair with `text` or `aria-label` |
| 1.4.3 Contrast (Minimum) | Review | Progress track and fill colors must meet 3:1 contrast against their background |
| 4.1.2 Name, Role, Value | Pass (when labelled) | Requires `text`, `aria-label`, or `aria-labelledby` to satisfy the name requirement |

_Source: Oxygen MCP · Extracted 2026-05-05_
