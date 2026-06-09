---
parent: "[[Select]]"
section: anatomy
component: Select
pipeline_stage: doc_rewrite
audit_verdict: NO
tags:
  - oxygen
  - component/Select
  - role/anatomy
  - stage/doc_rewrite
---

<!-- STUB:GAP-001 source="Run figma-extract Select targeting node 2105:2 in file 5YihJ5WuDvnvrlrRMC4sBp with Figma Desktop Bridge plugin active. The Select-figma.md file is entirely absent — this spoke is derived from variant metadata strings only." -->

## Anatomy

The published Oxygen docs page describes four numbered anatomy parts:

1. **Label** — visible heading rendered above the field (`labelValue` prop)
2. **Select field** — trigger row containing the input, dropdown chevron (`DropdownIndicator`), optional leading icon (`iconLeft`), and clear button (`ClearIndicator` when `isClearable` is true)
3. **Helper text** — rendered below the field by the consuming surface (not a built-in prop); used for error messages and supplemental instructions
4. **Popover** — floating menu containing the option list; opens on click, Enter, or Arrow Down

Additional optional parts exposed by the API:

5. **Info icon button + tooltip** — rendered when `infoBoxText` is set; accessible name via `infoBoxButtonLabel`
6. **Required indicator** — `*` shown when `isRequired={true}`
7. **Action element** — text + onClick rendered alongside the label via `action` / `actionLabel`

> Exact spacing values (label-to-field gap, popover-to-trigger offset, internal field padding) are not yet documented — pending `Select-figma.md`.

## Variants

The Figma component set (node 2105:2, file 5YihJ5WuDvnvrlrRMC4sBp) exposes ~80 variants across five axes derived from node name metadata:

| Property | Values | Notes |
|----------|--------|-------|
| Mode | Light, Dark | Light is default; Dark inverts token values (e.g. `ui01` shifts from `#EBEAE1` to `#666666`) |
| Size | Large (92px), Medium (84px), Small (76px) | Code prop: `size='large' \| 'default' \| 'small'`. `'default'` = Figma "Medium" |
| State | Rest, Hover, Focus, Disabled, Read-only | All states have distinct visual treatment |
| Open | True, False | Controls whether the popover is rendered |
| Error | True, False | Corresponds to `hasError` prop |

## States

| State | Trigger | Visual |
|-------|---------|--------|
| Rest | Default | Standard border |
| Hover | Pointer over field | Border emphasis |
| Focus | Keyboard Tab | Visible focus ring (WCAG 2.4.7) |
| Open | Click / Enter / Arrow Down | Popover visible; `aria-expanded="true"` |
| Selected | Value chosen | Value text (single) or chips (multi) replace placeholder |
| Disabled | `isDisabled={true}` | Reduced opacity; `aria-disabled="true"` |
| Read-only | Figma variant | Muted, non-editable; no direct boolean prop documented |
| Error | `hasError={true}` | Red border + sibling error message; `aria-invalid="true"` |
| Loading | `isLoading={true}` / async fetch | Spinner + `loadingMessage`; `aria-busy="true"` |

> Per-state colour token bindings are not confirmed — see [[Select.tokens]] `STUB:GAP-011`.

<!-- STUB:GAP-013 source="After running figma-extract (GAP-001), check whether the leading visuals frame (node 69857:19373) — which shows icon/status/avatar types for both Light and Dark modes — maps to the iconLeft prop or represents Figma-only design elements not yet implemented in code. If avatar/status types are unimplemented, flag as a design–code gap." -->
