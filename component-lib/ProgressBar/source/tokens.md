---
component: ProgressBar
package: "@8x8/oxygen-loaders"
category: feedback_status
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[ProgressBar/props]]"
  - "[[ProgressBar/examples]]"
  - "[[ProgressBar/accessibility]]"
  - "[[ProgressBar/ProgressBar-figma]]"
  - "[[ProgressBar/ProgressBar-usage]]"
  - "[[ProgressBar/ProgressBar-audit]]"
tags:
  - oxygen
  - component/ProgressBar
  - role/tokens
  - stage/spec_ready
  - category/feedback_status
---
# ProgressBar — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md) · [ProgressBar-usage.md](ProgressBar-usage.md) · [ProgressBar-figma.md](ProgressBar-figma.md)

Token names are extracted from CSS custom property names in the Figma design context output; not verified against the Figma UI-Foundations library (`iVY5nI8JAxM05Apnnvozzs`) — see GAP-010.

## Color tokens

| Element | Token | Role | Light mode | Dark mode |
|---------|-------|------|-----------|-----------|
| Bar track background | `--ui/ui01` | Empty-track fill | `#ebeae1` | `#666666` |
| Loading fill indicator | `--actions/action04` | Active progress fill | `#0056e0` | `#246fe5` |
| Complete fill | `--success/success01` | Completed-progress fill | `#127440` | `#189b55` |
| Text label | `--text/textcolor01` | Label text color | `#26252a` | `#ffffff` |

## Typography tokens

| Element | Token | Family | Size | Weight | Line height | Letter spacing |
|---------|-------|--------|------|--------|-------------|----------------|
| Text label | `--typography/body01` | Inter Regular | 14px | 400 | 20px | −0.06px |

## Spacing (no token bindings)

| Property | Value | Notes |
|----------|-------|-------|
| Bar track height | 8px | Hardcoded in Figma — no token binding found (GAP-012) |
| Gap (bar → text label) | 8px | Hardcoded in Figma — no token binding found (GAP-012) |
| Bar track border-radius | 8px | Hardcoded |

## Hardcoded values (Figma demo artifacts — not token bindings)

| Property | Value | Notes |
|----------|-------|-------|
| Container width | 184px | Figma placeholder only; runtime width controlled by `size` / `fullWidth` props |
| Loading fill right-inset | 41.85% | Demo fill percentage in Figma; runtime value from `value` prop |

_Source: ProgressBar-figma.md §Color & token bindings and §Structure & spacing · Token names from CSS custom properties · 2026-05-05_
