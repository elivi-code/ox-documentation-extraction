---
component: TextField
package: "@8x8/oxygen-textField"
category: form_inputs
role: figma
role_description: "Figma design spec — anatomy, variant axes, token bindings, and spacing extracted from Figma"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[TextField/props]]"
  - "[[TextField/examples]]"
  - "[[TextField/tokens]]"
  - "[[TextField/accessibility]]"
  - "[[TextField/TextField-pui]]"
  - "[[TextField/TextField-audit]]"
tags:
  - oxygen
  - component/TextField
  - role/figma
  - stage/spec_ready
  - category/form_inputs
---
# TextField — Figma Design Specs

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)
>
> **Figma file:** [UI-components — Input canvas](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=2072-14)

## Canvas structure

The "Input" canvas (node `2072:14`) contains three component families:

| Frame name | Node ID | Description |
|------------|---------|-------------|
| Text input | `22155:36793` | Single-line text field |
| Text area | `21562:34985` | Multi-line textarea |
| Search input | `25655:40530` | Text input with leading search icon |

There is also an **Atoms** section (`21562:35640`) containing two shared sub-components:
- `_base_form_label` — label + optional required asterisk + info icon button
- `_base_form_hint` — hint / error helper text beneath the input

---

## Variant dimensions

### Text input variants

Axes: **Mode** × **Size** × **State** × **Error** × **Read Only** × **Filled**

| Axis | Values |
|------|--------|
| Mode | Light, Dark |
| Size | Large, Medium, Small |
| State | Rest, Focus, Disabled |
| Error | True, False |
| Read Only | True, False |
| Filled | True, False |

### Text area variants

Same axes as Text input.

### Search input variants

| Axis | Values |
|------|--------|
| Mode | Light, Dark |
| Size | Large, Medium, Small |
| State | Rest, Focus, Disabled |
| Error | True, False |
| Filled | True, False |

No Read Only variant on Search input.

---

## Size reference

### Text input heights (fixed)

| Figma Size label | OX `size` prop | Height |
|-----------------|----------------|--------|
| Large | `large` | 92px |
| Medium | `default` | 84px |
| Small | `small` | 76px |

### Text area heights (fixed)

| Figma Size label | OX `size` prop | Height |
|-----------------|----------------|--------|
| Large | `large` | 156px |
| Medium | `default` | 124px |
| Small | `small` | 90px |

---

## Visual states

### Rest state (Light, Medium)

```
[_base_form_label]
  Label text (body01, 14px, --text/textColor01)
  Required asterisk * (bodyBold01, 14px, --error/error01)
  Info icon button (2px padding, rounded-6px)

[Input container]
  background: --ui/ui05 (#F4F3EE light / #2F2E32 dark)
  border-radius: 6px
  padding: 12px horizontal, 10px vertical
  Placeholder text (body01, 14px, --text/textColor02)

[_base_form_hint]
  Hint text (label01, 12px, --text/textColor02)
```

Screenshot (Medium, Light, Rest):
`node 22155:36806` — Label* ⓘ / [Placeholder] / This is a hint to help users.

### Focus state

Adds an **absolute focus ring overlay** inside the input container:
- `border: 2px solid var(--interactive/focus01, #0056E0)`
- `border-radius: 6px`
- A 1px-wide cursor indicator (height 20px, colour `--text/textColor01`) appears before the placeholder

Screenshot (Medium, Light, Focus):
`node 22155:36980` — Blue 2px ring visible around input

### Error state

Input container gains:
- `border: 2px solid var(--error/error01, #CB2233)`

Error area replaces hint text:
- Error icon (16×16px, triangle/exclamation)
- Error message text (label01, 12px, `--error/error01`)
- Layout: horizontal flex, gap 4px

Screenshot (Medium, Light, Error):
`node 22155:37040` — Red 2px border, "⚠ Error message goes here."

### Disabled state

- Same background, reduced opacity applied at container level
- Input is non-interactive (no focus ring)

### Read-only state (Filled=True required in Figma)

- Same appearance as Rest/Filled
- No focus ring on click
- Value text displayed; user cannot type

---

## Text area specifics

- Container has a **fixed height** (not hug) matching the size variants above
- `padding: 12px horizontal, 8px vertical` (vs 10px for text input)
- Optional **resize grip**: 5×5px dot icon in the bottom-right corner (Figma prop `resizeGrip`)
- Placeholder/value text is clipped with `overflow: hidden; text-overflow: ellipsis` (single line in Figma representation)

Screenshot (Medium, Light, Rest):
`node 21562:34998` — Taller container (~80px content area), resize grip visible

---

## Search input specifics

- Leading **search icon** (magnifying glass, 16px) inside the input container
- Padding: `16px horizontal, 12px vertical` (larger than standard text input)
- Placeholder uses `--typography/body02` (16px, 24px line-height) — one size larger than text input
- Code Connect maps to `KeywordSearch` component (`packages/keywordSearch/src/components/KeywordSearch/index.ts`)

Screenshot (Large, Light, Rest):
`node 25649:40529` — 🔍 "Search placeholder" / hint text

---

## Shared atom: `_base_form_label`

Structure (horizontal flex, gap 4px):
```
[H Stack]
  Label text        — body01, --text/textColor01
  * (if required)   — bodyBold01, --error/error01
[Info icon button]  — TypeIcon component, rounded-6px, p-2px
```

Code Connect: `TypeIcon` from `packages/toast/src/components/typeMarkings.tsx`

## Shared atom: `_base_form_hint`

```
Hint / error text   — label01, 12px, --text/textColor02 (hint) or --error/error01 (error)
```

---

## Design token mapping (Figma → CSS variables)

| Figma colour | CSS variable | Light hex | Dark hex |
|-------------|-------------|-----------|----------|
| Input background | `--ui/ui05` | `#F4F3EE` | `#2F2E32` |
| Primary text | `--text/textColor01` | `#26252A` | `#FFFFFF` |
| Placeholder / hint | `--text/textColor02` | `#6C6862` | — |
| Focus ring | `--interactive/focus01` | `#0056E0` | `#D7E3F9` |
| Error | `--error/error01` | `#CB2233` | — |

---

## Component documentation link

All three variants point to:
`https://oxygen.8x8.com/docs/Contribution/intro`

_Source: Figma MCP (file 5YihJ5WuDvnvrlrRMC4sBp, node 2072:14) · Extracted 2026-04-29_
