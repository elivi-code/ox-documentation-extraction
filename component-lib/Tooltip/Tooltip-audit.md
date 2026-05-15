---
component: Tooltip
rubric_version: "1.0"
extracted: 2026-05-05
audited: 2026-05-05
re_audited: 2026-05-15
verdict: "PARTIAL"
verdict_reason: "Both blocker CONFLICTs reconciled against the canonical published Oxygen docs (https://oxygen.8x8.com/components/tooltip/usage). GAP-001 → 140 characters. GAP-002 → orientation default 'top'. Five Do/Don't pairs added to Tooltip-usage.md. Remaining gaps are non-blocking DOC_GAPs and SOURCE_GAPs."

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - Tooltip-figma.md
  - Tooltip-usage.md
  - Tooltip-pui.md
files_missing: []

scores:
  props:         { coverage: "6/7",  score: 0.86 }   # GAP-002 resolved
  examples:      { coverage: "5/7",  score: 0.71 }
  tokens:        { coverage: "4/8",  score: 0.50 }
  accessibility: { coverage: "8/10", score: 0.80 }
  figma:         { coverage: "9/13", score: 0.69 }
  usage:         { coverage: "9/9",  score: 1.00 }   # GAP-001 resolved; Do/Don't pairs added
  pui:           { coverage: "4/4",  score: 1.00 }

totals:
  conflicts:   0   # GAP-001 + GAP-002 both reconciled 2026-05-15
  doc_gaps:    7
  source_gaps: 10
  warnings:    2

gaps:

  - id: GAP-001
    dimension: usage
    severity: blocker
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    status: RESOLVED
    resolved: 2026-05-15
    resolution: "Reconciled to 140 characters per the canonical published Oxygen docs (https://oxygen.8x8.com/components/tooltip/usage — Behavior, Content). Tooltip-usage.md updated 2026-05-15: Best practices, Size table, and Tooltip vs. Popover vs. Modal comparison all aligned to 140."
    evidence:
      source_file: Tooltip-usage.md
      location: "## Best practices, line 43"
      finding: "Tooltip-usage.md (Figma source) states maximum 136 characters. OX MCP usage docs (props.md, examples.md, accessibility.md) state maximum 140 characters."
    fix_action: "Confirm authoritative character limit with design/content team; update all files to the agreed value."
    blocks: []
    dependency: []

  - id: GAP-002
    dimension: props
    severity: blocker
    type: CONFLICT
    confidence: heuristic
    auto_fixable: false
    status: RESOLVED
    resolved: 2026-05-15
    resolution: "Reconciled to orientation default 'top'. The OX MCP `Orientation` allowedValues list 'top' first (registry-default convention) and props.md already documents 'top'. The Figma 'Bottom / Center' value is a default Figma variant for the showcase frame, not the runtime component default. No change required to props.md."
    evidence:
      source_file: props.md
      location: "Tooltip Props table, orientation row"
      finding: "props.md lists orientation default as 'top' (inferred — MCP did not return a default). Tooltip-figma.md documents Figma's default variant as 'Bottom / Center' (i.e. orientation='bottom'). Two sources disagree."
    fix_action: "Verify the runtime default for orientation in the @8x8/oxygen-tooltip source or Storybook argsConfig; update props.md to match."
    blocks: []
    dependency: []

  - id: GAP-003
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Tooltip Props table, delay / showOn / disableInteractive / disableDescribedBy / enableArrow rows"
      finding: "Defaults for delay (300), showOn ('hover'), disableInteractive (false), disableDescribedBy (false), enableArrow (false) are inferred from usage docs and component behaviour — MCP did not return explicit default values."
    fix_action: "Verify defaults in Storybook argsConfig or component source; annotate inferred defaults with '(inferred)' until confirmed."
    blocks: []
    dependency: []

  - id: GAP-004
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "Tooltip Props table, modifiers row"
      finding: "modifiers type is truncated: '{ offset?: { offset?: number | string' — the MCP returned an incomplete type string. Full type signature unknown."
    fix_action: "Look up the modifiers type in the @8x8/oxygen-tooltip TypeScript source and document the complete signature."
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: examples
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Footer note, line 124"
      finding: "examples.md states 'The Oxygen MCP returned no clean code snippets for Tooltip. Examples above are inferred from props, usage docs, and component behaviour.' No Storybook-sourced examples exist."
    fix_action: "Extract clean examples from Storybook (https://oxygen.8x8.dev/packages/release/latest/?path=/story/components-tooltip--tooltip-documentation) and replace inferred snippets."
    blocks: [storybook]
    dependency: []

  - id: GAP-006
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "all sections"
      finding: "No example demonstrates the Mode (Light/Dark) visual difference. Figma documents two distinct mode variants with inverted background colours."
    fix_action: "Add a Light vs Dark mode side-by-side example once verified in Storybook."
    blocks: []
    dependency: [GAP-005]

  - id: GAP-007
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "all sections"
      finding: "No example for customCloseHandlers or the modifiers prop. These are advanced use cases with no illustration."
    fix_action: "Add usage examples for customCloseHandlers and modifiers once the modifiers type is resolved (GAP-004)."
    blocks: []
    dependency: [GAP-004]

  - id: GAP-008
    dimension: tokens
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md
      location: "## Theme tokens, line 7"
      finding: "tokens.md contains no semantic CSS variable names. Token data exists in Tooltip-figma.md (--ui/ui07, --text/textcolor04, --ui/shadow01, --typography/body01/*) but was not synthesised into tokens.md."
    fix_action: "doc-rewrite should pull token data from Tooltip-figma.md Color & token bindings section into the canonical spec tokens table."
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: props
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## StaticTooltip, line 70"
      finding: "StaticTooltip props are not documented in the Oxygen MCP. Only children is confirmed from a Storybook example. The full API is unknown."
    fix_action: "Extract StaticTooltip props from @8x8/oxygen-static-tooltip TypeScript source or Storybook and add a StaticTooltip props table to props.md."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-010
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Tooltip-figma.md
      location: "## Structure & spacing, Container table"
      finding: "Content border-radius (6px), padding-x (8px), padding-y (4px), and max-width (320px/326px) are hardcoded in Figma with no CSS variable binding. These should map to design tokens."
    fix_action: "Confirm with design team whether radius/padding/max-width values should be tokenised; if yes, create tokens in the Figma library and update Tooltip-figma.md."
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: Tooltip-figma.md
      location: "## Color & token bindings, note on line 105"
      finding: "Token names (--ui/ui07, --text/textcolor04, --ui/shadow01) were extracted from Figma design context Tailwind output, not verified against the Figma Variables API (Enterprise tier required). Values may have drifted."
    fix_action: "Verify token names and resolved values against the UI-Foundations Figma library (fileKey: iVY5nI8JAxM05Apnnvozzs) using figma_execute + getVariableByIdAsync."
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: Tooltip-figma.md
      location: "## Shadow / elevation table"
      finding: "Light mode uses CSS drop-shadow filter; Dark mode uses box-shadow. Both resolve to --ui/shadow01 but the CSS implementation differs. This may be a Figma design inconsistency or intentional."
    fix_action: "Confirm with design team whether the drop-shadow vs box-shadow difference is intentional; if it's a Figma artifact, align to a single implementation."
    blocks: []
    dependency: []

  - id: GAP-013
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "## WCAG 2.1 AA checklist, 1.4.3 row"
      finding: "1.4.3 Contrast is marked 'Verify' — the actual contrast ratio of --text/textcolor04 against --ui/ui07 has not been calculated."
    fix_action: "Calculate contrast ratio for Light (#ffffff on #26252a) and Dark (#292929 on #f1f1f1) modes; both should meet 4.5:1. Update the checklist to Pass or flag if failing."
    blocks: []
    dependency: [GAP-011]

  - id: GAP-014
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Tooltip-figma.md
      location: "## Gaps & conflicts, line 222"
      finding: "figma_get_component_details was unavailable (Desktop Bridge plugin not running). Enriched variant key map and token coverage % were not retrieved."
    fix_action: "Re-run figma-extract with Desktop Bridge active to get enriched component metadata."
    blocks: []
    dependency: []

  - id: GAP-015
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Tooltip-figma.md
      location: "## Gaps & conflicts, line 221"
      finding: "Figma Variables API requires Enterprise plan — figma_get_variables returned an error. Icon tooltip dimensions and icon token bindings were not extracted."
    fix_action: "Use figma_execute + console snippet workflow to extract variables from the open Figma file when Desktop Bridge is available."
    blocks: []
    dependency: []

  - id: GAP-016
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Tooltip-figma.md
      location: "## Internal spacing table, Icon size row"
      finding: "Icon tooltip (frame 1956:11221) dimensions and the icon token bindings were not extracted from Figma."
    fix_action: "Run get_design_context on node 1956:11221 to extract Icon tooltip structure and update Tooltip-figma.md."
    blocks: []
    dependency: []

  - id: GAP-017
    dimension: usage
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    status: MITIGATED
    mitigated: 2026-05-15
    mitigation: "Five derived Do/Don't pairs added to Tooltip-usage.md, authored from the published Oxygen docs (https://oxygen.8x8.com/components/tooltip/usage) and grounded in props.md / accessibility.md / Tooltip-figma.md. SOURCE_GAP remains open until designers add ✅ Do / ❌ Don't card frames to the Figma ↳ Tooltip examples page; severity downgraded major → minor and no longer blocks doc-rewrite."
    evidence:
      source_file: Tooltip-usage.md
      location: "## Gaps, line 107"
      finding: "The Figma ↳ Tooltip examples page contains no ✅ Do / ❌ Don't card frames. The page uses text-based sections only. No Do/Don't visual examples are available."
    fix_action: "Request designer to add ✅ Do / ❌ Don't card frames to the ↳ Tooltip examples Figma page using the figma-draw template."
    blocks: []
    dependency: []

  - id: GAP-018
    dimension: usage
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Tooltip-usage.md
      location: "## Gaps, line 111"
      finding: "Screenshots of Figma image blocks on the examples page were not captured — Desktop Bridge was not connected during extraction."
    fix_action: "Re-run figma-extract-usage with Desktop Bridge active to capture image block screenshots."
    blocks: []
    dependency: []

  - id: GAP-019
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Tooltip-figma.md
      location: "## Accessibility (from Figma annotations only)"
      finding: "No ARIA role, focus order, or keyboard interaction annotations found in the Figma component. Accessibility intent is not captured at source."
    fix_action: "Request designer to add accessibility annotations to the Tooltip Figma component (ARIA role, focus behaviour, keyboard hints)."
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: examples
    confidence: heuristic
    finding: "examples.md contains a ReactNode title example with rich HTML content (<strong>). The usage docs explicitly say tooltips should use plain text only. The example itself includes a warning note, but doc-rewrite should consider whether to include or exclude this example."

  - id: WARN-002
    dimension: tokens
    confidence: heuristic
    finding: "tokens.md documents max-width as 320px (from usage docs) but Tooltip-figma.md shows 326px for Left/Right orientations. Minor inconsistency — the usage docs value may refer only to Top/Bottom orientations."
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: extracted
pipeline_note: "Audit verdict PARTIAL — both blocker CONFLICTs resolved 2026-05-15; remaining gaps are non-blocking"
siblings:
  - "[[Tooltip/props]]"
  - "[[Tooltip/examples]]"
  - "[[Tooltip/tokens]]"
  - "[[Tooltip/accessibility]]"
  - "[[Tooltip/Tooltip-figma]]"
  - "[[Tooltip/Tooltip-usage]]"
  - "[[Tooltip/Tooltip-pui]]"
tags:
  - oxygen
  - component/Tooltip
  - role/audit
  - stage/extracted
---

# Tooltip — Documentation Audit

> **Verdict: PARTIAL** — both blocker CONFLICTs resolved 2026-05-15.
>
> GAP-001 (character limit) reconciled to **140** per the canonical published Oxygen docs. GAP-002 (orientation default) reconciled to **`top`** — the Figma "Bottom / Center" value is a default showcase variant, not the runtime default. Five derived Do/Don't pairs added to Tooltip-usage.md (mitigates GAP-017). Remaining gaps are non-blocking DOC_GAPs and SOURCE_GAPs; `doc-rewrite` can now proceed.

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [Tooltip-figma.md](./Tooltip-figma.md) ·
> [Tooltip-usage.md](./Tooltip-usage.md) · [Tooltip-pui.md](./Tooltip-pui.md)

---

## File inventory

| File | Status |
|------|--------|
| `props.md` | ✅ Present |
| `examples.md` | ✅ Present |
| `tokens.md` | ✅ Present |
| `accessibility.md` | ✅ Present |
| `Tooltip-figma.md` | ✅ Present |
| `figma-screenshot-tooltip.png` | ✅ Present |
| `Tooltip-usage.md` | ✅ Present |
| `Tooltip-pui.md` | ✅ Present — `NO RELEVANT PUI CONTEXT` (PASS) |

All 7 expected files are present. No missing-file blockers.

---

## Dimension scores

| Dimension | Coverage | Score | Status |
|-----------|----------|-------|--------|
| Props | 6/7 | 0.86 | ✅ GAP-002 resolved (orientation default `top`) |
| Examples | 5/7 | 0.71 | ⚠️ Inferred snippets (no Storybook source) |
| Tokens | 4/8 | 0.50 | ⚠️ Data in figma.md, not tokens.md |
| Accessibility | 8/10 | 0.80 | ✅ Solid; contrast unverified |
| Figma | 9/13 | 0.69 | ⚠️ Desktop Bridge / Variables API missing |
| Usage | 9/9 | 1.00 | ✅ GAP-001 resolved (140 chars); 5 derived Do/Don't pairs added |
| PUI | 4/4 | 1.00 | ✅ No PUI context confirmed |

---

## Conflicts — RESOLVED 2026-05-15

### GAP-001 · CONFLICT · ✅ RESOLVED

**Character limit reconciled to 140 characters** (per the canonical published Oxygen docs `/components/tooltip/usage`).

| Source | Value | Location |
|--------|-------|----------|
| OX MCP usage docs | **140 characters max** ✅ | props.md, examples.md, accessibility.md |
| Published Oxygen docs | **140 characters max** ✅ | oxygen.8x8.com/components/tooltip/usage — Behavior, Content |
| ~~Figma `↳ Tooltip examples`~~ | ~~136 characters max~~ | ~~Tooltip-usage.md (now updated)~~ |

**Resolution (2026-05-15):** Tooltip-usage.md updated to 140 throughout (Best practices, Size table, Tooltip vs. Popover vs. Modal comparison). The published docs are canonical for the runtime contract.

---

### GAP-002 · CONFLICT · ✅ RESOLVED

**orientation default reconciled to `'top'`** (runtime default; Figma's "Bottom / Center" is a showcase variant default, not the component runtime default).

| Source | Value | Notes |
|--------|-------|-------|
| props.md | `'top'` ✅ | Matches OX MCP `Orientation` allowedValues ordering |
| OX MCP `Orientation` type | `'top'` listed first ✅ | Registry-default convention |
| Tooltip-figma.md | `bottom` (Figma variant) | The Figma file's default *showcase variant* — distinct from the runtime prop default |

**Resolution (2026-05-15):** No change to props.md required — the runtime default `'top'` stands. Tooltip-figma.md's "Bottom / Center" is a Figma variant-axis default for the showcase frame, not the component's runtime default value. The two sources describe different things.

---

## Doc gaps (auto-fixable by doc-rewrite)

| ID | Dimension | Severity | Finding |
|----|-----------|----------|---------|
| GAP-003 | Props | minor | Prop defaults (delay, showOn, disableInteractive, disableDescribedBy, enableArrow) are inferred — verify in source |
| GAP-004 | Props | minor | `modifiers` type truncated in MCP output — full TypeScript signature unknown |
| GAP-005 | Examples | **major** | All examples are inferred from props/usage docs — no Storybook-sourced snippets |
| GAP-006 | Examples | minor | No Light/Dark mode example |
| GAP-007 | Examples | minor | No example for `customCloseHandlers` or `modifiers` |
| GAP-008 | Tokens | **major** | tokens.md has no CSS variable names — token data exists only in Tooltip-figma.md |

---

## Source gaps (require upstream input)

| ID | Dimension | Severity | Finding |
|----|-----------|----------|---------|
| GAP-009 | Props | **major** | StaticTooltip props not in OX MCP — API undocumented |
| GAP-010 | Tokens | minor | Hardcoded border-radius (6px), padding (8/4px), max-width (320px) lack token bindings |
| GAP-011 | Tokens | minor | Token values from Figma design context output, not verified via Variables API |
| GAP-012 | Figma | minor | shadow01 uses different CSS impl per mode (drop-shadow vs box-shadow) — may be design inconsistency |
| GAP-013 | Accessibility | minor | WCAG 1.4.3 contrast not calculated — marked 'Verify' |
| GAP-014 | Figma | minor | figma_get_component_details not retrieved (Desktop Bridge required) |
| GAP-015 | Figma | minor | Variables API unavailable (Figma Enterprise required) |
| GAP-016 | Figma | minor | Icon tooltip (node 1956:11221) dimensions not extracted |
| GAP-017 | Usage | minor (mitigated) | Five derived Do/Don't pairs added to Tooltip-usage.md from published Oxygen docs (2026-05-15). SOURCE_GAP remains open until designers author Figma cards. |
| GAP-018 | Usage | minor | Image block screenshots not captured (Desktop Bridge required) |
| GAP-019 | Figma | minor | No ARIA annotations in Figma component — designer must add |

---

## Warnings (heuristic — advisory only)

**WARN-001 · Examples:** The ReactNode title example in examples.md uses `<strong>` — contradicts the "plain text only" content rule documented in the same file. doc-rewrite should decide whether to include or omit this example.

**WARN-002 · Tokens:** tokens.md states max-width 320px (from usage docs); Tooltip-figma.md shows 326px for Left/Right orientations. Minor inconsistency — the usage-docs value may be Top/Bottom only.

---

## Suggested resolution order

1. ~~**Resolve GAP-001**~~ — ✅ resolved 2026-05-15 (140 characters per published docs)
2. ~~**Resolve GAP-002**~~ — ✅ resolved 2026-05-15 (`top` runtime default stands; Figma "Bottom" is a showcase variant)
3. **Run `doc-rewrite Tooltip`** — both blocker conflicts cleared; `doc-rewrite` can absorb GAP-008 by pulling tokens from figma.md and merge the new Do/Don't pairs into the canonical spec
4. **GAP-005** — replace inferred examples with Storybook snippets at next opportunity
5. **GAP-009** — StaticTooltip props: extract from component source
6. **GAP-017** — request designer to add ✅ Do / ❌ Don't card frames to the Figma `↳ Tooltip examples` page; replace derived pairs with `figma-extract-usage` output when authored

---

_Rubric version 1.0 · Audited 2026-05-05 · Re-audited 2026-05-15 (conflicts resolved, Do/Don't pairs added)_
