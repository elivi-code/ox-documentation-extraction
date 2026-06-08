---
parent: "[[TextArea]]"
section: tokens
pipeline_stage: draft
audit_verdict: partial
tags:
  - oxygen
  - component/TextArea
  - section/tokens
---

## Color tokens

### Input container background

| State | Token | Light value | Dark value |
|-------|-------|-------------|------------|
| Rest | `--ui/ui05` | `#f4f3ee` | `#2f2e32` |
| Focus | `--ui/ui05` | `#f4f3ee` | `#2f2e32` |
| Error (Rest) | `--ui/ui05` | `#f4f3ee` | `#2f2e32` |
| Disabled | `--interactive/disabled01` | `#c8c8bd` | `#c2c2c2` |

### Input border

| State | Token | Light value | Dark value | Width |
|-------|-------|-------------|------------|-------|
| Rest | _(none — no border)_ | — | — | — |
| Focus | `--interactive/focus01` | `#0056e0` | `#d7e3f9` | 2px solid |
| Error | `--error/error01` | `#cb2233` | `#f24d5f` | 2px solid |
| Disabled | _(none)_ | — | — | — |

### Label text

| State | Token | Light value | Dark value |
|-------|-------|-------------|------------|
| All states | `--text/textcolor01` | `#26252a` | `#ffffff` |

### Required `*` marker

| State | Token | Light value | Dark value |
|-------|-------|-------------|------------|
| All states | `--error/error01` | `#cb2233` | `#f24d5f` |

### Placeholder / input text

| State | Token | Light value | Dark value |
|-------|-------|-------------|------------|
| Rest / Focus | `--text/textcolor02` | `#6c6862` | `#c2c2c2` |
| Disabled | `--interactive/disabled04` | `#8d8b7e` | `#858585` |

> Input value text color when the field is filled (`Filled=True`) is not separately confirmed — see marker below.

### Hint text

| State | Token | Light value | Dark value |
|-------|-------|-------------|------------|
| All states | `--text/textcolor02` | `#6c6862` | `#c2c2c2` |

### Error area

| Element | Token | Light value | Dark value |
|---------|-------|-------------|------------|
| Error message text | `--error/error01` | `#cb2233` | `#f24d5f` |
| Error icon | `--error/error01` (via SVG fill) | `#cb2233` | `#f24d5f` |

> **Note on dark mode values:** tokens.md (extracted 2026-04-29) states dark mode was not resolved. The dark values above are sourced from `textarea-figma.md`, which was updated on 2026-05-05 via `figma_execute` alias chain traversal from the UI-Foundations library. `tokens.md` needs to be re-extracted to reflect this resolution.

<!-- STUB:GAP-004 source="Re-extract tokens.md with Figma Desktop Bridge active to confirm dark mode token aliases match the resolved values in textarea-figma.md — current dark values are sourced from figma.md alias traversal, not from the compiled token registry" -->

<!-- SKIP:GAP-006 manual="Inspect Mode=Light, Size=Large, State=Rest, Filled=True variant (node 21722:35590) in Figma to confirm input value text color token for filled state — only Filled=False baseline was verified at extraction time" -->

---

## Typography tokens

| Element | Token family | Weight | Size | Line height | Letter spacing |
|---------|-------------|--------|------|-------------|----------------|
| Label | `typography/body01` | 400 (Regular) | 14px | 20px | −0.06px |
| Required `*` | `typography/bodyBold01` | 600 (SemiBold) | 14px | 20px | −0.06px |
| Input / Placeholder | `typography/body02` | 400 (Regular) | **16px (hardcoded)** | 24px | 0.0121px |
| Hint text | `typography/label01` | 400 (Regular) | 12px | 16px | 0px |
| Error text | `typography/label01` | 400 (Regular) | 12px | 16px | 0px |

> **Hardcoded value:** Input text font-size is set to `16px` directly in the design — not bound to a typography token variable. All other typography values reference tokens.

---

## Structural / spacing values (hardcoded)

| Property | Value | Notes |
|----------|-------|-------|
| Border radius | `6px` | Not tokenised |
| Padding horizontal | `16px` | Not tokenised |
| Padding vertical | `12px` | Not tokenised |
| Gap (label → input → hint) | `4px` | Not tokenised |
| Resize grip offset (Rest/Focus) | `8px` from edges | Not tokenised |
| Resize grip offset (Error) | `6px` from edges | Not tokenised (slight inconsistency) |
| Focus ring width | `2px` | Not tokenised |
| Focus cursor bar width | `1px` | Not tokenised |

---

## Dark mode

Dark mode is controlled at the `OxygenProvider` theme level — there is no `mode` prop on the component. See the CONFLICT marker in [[TextArea.props]] regarding the Figma `Mode` variant axis. Dark value tokens are resolved in the color tables above.

---

_Source: Oxygen MCP + Figma MCP · Extracted 2026-04-29 · Dark mode values from textarea-figma.md update 2026-05-05_
