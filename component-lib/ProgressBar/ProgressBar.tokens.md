---
parent: "[[ProgressBar]]"
section: tokens
component: ProgressBar
pipeline_stage: spec_ready
tags:
  - oxygen
  - component/ProgressBar
  - role/spoke
  - section/tokens
---

Token names are extracted from CSS custom property names in the Figma design context output. Not verified against the Figma UI-Foundations library (`iVY5nI8JAxM05Apnnvozzs`) — see GAP-010.

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
| Bar track height | 8px | Hardcoded in Figma — no token binding (GAP-012) |
| Gap (bar → text label) | 8px | Hardcoded in Figma — no token binding (GAP-012) |
| Bar track border-radius | 8px | Hardcoded |

## Hardcoded values (Figma demo artifacts — not token bindings)

| Property | Value | Notes |
|----------|-------|-------|
| Container width | 184px | Figma placeholder; runtime width controlled by `size` / `fullWidth` props |
| Loading fill right-inset | 41.85% | Demo percentage in Figma; runtime value derived from `value` prop |

<!-- source: figma-only -->
<!-- STUB:GAP-010 source="Run figma_get_variables with resolveAliases=true (requires Desktop Bridge or enterprise token) to verify token names against the Figma UI-Foundations library (iVY5nI8JAxM05Apnnvozzs)" -->
<!-- STUB:GAP-012 source="Flag to design: should bar-track height (8px) and bar-to-label gap (8px) be spacing tokens? Confirm intent and update once decided" -->
