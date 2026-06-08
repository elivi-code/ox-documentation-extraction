---
component: Checkbox
package: "@8x8/oxygen-checkbox"
category: form_inputs
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Checkbox/props]]"
  - "[[Checkbox/examples]]"
  - "[[Checkbox/accessibility]]"
  - "[[Checkbox/checkbox-figma]]"
  - "[[Checkbox/checkbox-pui]]"
  - "[[Checkbox/checkbox-audit]]"
tags:
  - oxygen
  - component/Checkbox
  - role/tokens
  - stage/spec_ready
  - category/form_inputs
---
# Checkbox — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

> **Note:** The Oxygen MCP returned 0 theme token matches for the `checkbox` search term, but
> the component's color/state bindings were subsequently resolved from Figma via `figma_execute`
> alias-chain traversal (2026-05-05) and are recorded below. The spacing references come verbatim
> from usage documentation.

---

## Spacing tokens (from documentation text)

| Usage | Token | Notes |
|-------|-------|-------|
| Between group label and first checkbox | `$spacing04` | Verbatim from anatomy docs |
| Between checkbox labels (vertical list) | `$spacing03` | Verbatim from anatomy docs |

---

## Color and state tokens (confirmed from Figma)

Resolved via `figma_execute` + `getVariableByIdAsync` alias-chain traversal on node `51776:5081`
(UI-components → UI-Foundations library), confirmed 2026-05-05. States as columns, elements as rows.

| Element | Semantic token | Primitive (Light) | Hex (Light) | Primitive (Dark) | Hex (Dark) |
|---------|---------------|-------------------|-------------|------------------|------------|
| Unchecked border | `ui/ui21` | `color/offWhite/offWhite05` | `#6c6862` | `color/gray/gray08` | `#c2c2c2` |
| Checked / indeterminate fill | `ui/ui22` | `color/blue/blue05` | `#0056e0` | `color/blue/blue09` | `#ccddf9` |
| Disabled background | `interactive/disabled02` | `color/offWhite/offWhite08` | `#c8c8bd` | `color/gray/gray05` | `#666666` |
| Focus ring | `interactive/focus01` | `color/blue/blue05` | `#0056e0` | `color/blue/blue10` | `#d7e3f9` |
| Label text | `text/textColor01` | `color/offWhite/offWhite02` | `#26252a` | `color/pure/white` | `#ffffff` |
| Error border / message | `error/error01` | `color/red/red05` | `#cb2233` | `color/red/red07` | `#f24d5f` |

> `text/textColor01` and `error/error01` were resolved from the shared token pattern (not directly
> bound on this component set scan; confirmed from Label, ToggleButton, and Input component
> extractions) — see GAP-003.

### State summary

| State | Input appearance |
|-------|-----------------|
| Unchecked rest | 2px border `ui/ui21` on transparent bg |
| Checked / indeterminate rest | Filled with `ui/ui22` (blue), white check icon |
| Disabled (any) | Bg `interactive/disabled02`, muted appearance |
| Focus ring | 2px outline `interactive/focus01`, inset gap `ui/ui06` (white/dark) |
| Error | Border `error/error01`; error message text `error/error01` |

---

## Figma variant axes (not tokenised — raw values unavailable)

The following variant axes were found in Figma but no bound token values could be retrieved:

| Axis | Values | Notes |
|------|--------|-------|
| Mode | Light, Dark | Theming dimension |
| State | Rest, Hover | Transient — not API props |
| isChecked | False, True | Matches `isChecked` prop |
| isIndeterminate | False, True | Matches `isIndeterminate` prop |
| isDisabled | False, True | Matches `isDisabled` prop |
| isFocused | False, True | Transient — not API prop |

---

## What to investigate

To get actual token bindings for Checkbox:
1. Enable the Figma Desktop Bridge plugin in the UI-components file
2. Re-run extraction with `figma_get_variables(namePattern="checkbox", resolveAliases=true)`
3. Alternatively search the Oxygen design token source for `checkbox` in the semantic layer

_Source: Oxygen MCP + Figma figma-console MCP · Extracted 2026-04-29_
