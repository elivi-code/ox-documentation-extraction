---
component: Spinner
package: "@8x8/oxygen-loaders"
category: feedback_status
role: accessibility
role_description: "Accessibility — ARIA roles, keyboard interactions, and WCAG 2.1 AA guidance"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Spinner/props]]"
  - "[[Spinner/examples]]"
  - "[[Spinner/tokens]]"
  - "[[Spinner/Spinner-figma]]"
  - "[[Spinner/Spinner-audit]]"
tags:
  - oxygen
  - component/Spinner
  - role/accessibility
  - stage/blocked
  - category/feedback_status
---
# Spinner — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md) · [Spinner-figma.md](Spinner-figma.md) · [Spinner-usage.md](Spinner-usage.md)

## Overview

The Spinner is a passive, display-only component — it conveys processing state without being interactive. Users cannot focus or activate it. Accessibility responsibility lies in providing a meaningful label so screen readers announce the loading state.

## ARIA roles and attributes

| Attribute | Value | Notes |
|-----------|-------|-------|
| `role` | `status` (inferred from usage) | Announces content changes without interrupting the user (live region, polite). |
| `aria-label` | String | Required when no visible `text` prop is provided. Describes what is loading (e.g. `"Loading"`, `"Loading conversation list"`). |
| `text` prop | Visible string | When provided, acts as the accessible label. Prefer `text` over `aria-label` wherever space permits — visible labels are always better than hidden ones. |

## Keyboard interaction

None. The Spinner is not focusable and has no keyboard interactions.

## Screen reader guidance

- Always supply either `text` or `aria-label`. A spinner without any label is invisible to screen reader users.
- Prefer descriptive labels over generic ones: `"Loading contact list"` is more useful than `"Loading"`.
- The supporting text (`text` prop) should set clear expectations for the user. Do not omit it for stylistic reasons (per Oxygen usage guidelines).
- When a spinner overlays interactive content (e.g. a modal), ensure focus is trapped or managed appropriately by the parent — the spinner itself does not manage focus.

## Motion sensitivity

The spinner is a continuous rotation animation. For users with `prefers-reduced-motion` enabled, consider respecting the system preference via the `hasAnimation` prop (set to `false`) or CSS media query in the consuming layout.

## WCAG 2.1 AA checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.1.1 Non-text content | Must provide | Use `aria-label` or visible `text` |
| 1.4.3 Contrast (minimum) | Inherits theme | Verify spinner stroke meets 3:1 against background |
| 2.1.1 Keyboard | Pass | Component is not focusable; no keyboard interaction required |
| 2.3.1 Three flashes | Pass | Rotation animation is below flash threshold |
| 2.3.3 Animation from Interactions | Must provide | Respect prefers-reduced-motion via hasAnimation=false or CSS media query. |
| 4.1.3 Status messages | Must provide | Spinner should be wrapped in or act as a live region (`role="status"`) so screen readers announce loading state |

_Source: Oxygen MCP · Extracted 2026-05-05_
