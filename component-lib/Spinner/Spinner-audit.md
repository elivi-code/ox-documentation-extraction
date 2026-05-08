---
rubric_version: "1.0"
component: Spinner
package: "@8x8/oxygen-loaders"
audit_date: "2026-05-05"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - Spinner-figma.md
  - figma-screenshot-Spinner.png

files_missing:
  - Spinner-usage.md
  - Spinner-pui.md

dimension_scores:
  props:        { score: 0.78, coverage: "7/9" }
  examples:     { score: 0.75, coverage: "6/8" }
  tokens:       { score: 0.25, coverage: "1/4 — SOURCE_GAP (no token bindings available)" }
  accessibility:{ score: 0.83, coverage: "10/12" }
  figma:        { score: 0.67, coverage: "8/12" }
  usage:        { score: 0.00, coverage: "0/0 — SOURCE_GAP (file missing)" }
  pui:          { score: 1.00, coverage: "PASS — no results from Platform UI MCP search; no application-layer concerns" }

available_dimensions_avg: 0.71
overall_avg: 0.61

counts:
  doc_gaps: 4
  source_gaps: 5
  conflicts: 2
  warnings: 2

verdict: NO
verdict_reason: >
  Two CONFLICTs must be resolved before doc-rewrite can proceed.
  GAP-010: the Figma `isInverted` variant axis has no corresponding React prop — needs
  human decision on whether a prop should be added or whether this is design-only intent
  handled by theme context.
  GAP-011: React `spinnerSize` includes `"large2x"` but the Figma component set only
  defines `default` and `small` — one of the two sources is incomplete and needs alignment.
  Additionally, GAP-006 (major SOURCE_GAP: no token bindings available) limits the
  rewrite of the tokens dimension.

gaps:
  - id: GAP-001
    dimension: props / examples / tokens / accessibility
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md, examples.md, tokens.md, accessibility.md
      location: "'See also' nav line in each file"
      finding: >
        All four OX files link only to each other; none include a link to
        Spinner-figma.md. The Figma spec file exists in the folder but is not
        cross-referenced.
    fix_action: "Append ' · [Spinner-figma.md](Spinner-figma.md)' to the See also line in props.md, examples.md, tokens.md, and accessibility.md."
    blocks: []
    dependency: []

  - id: GAP-002
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## Props — strokeWidth and hasAnimation rows"
      finding: >
        Both `strokeWidth` and `hasAnimation` have empty description strings (the OX MCP
        returned no doc string for either). Their purpose is undocumented beyond the type.
    fix_action: "Verify strokeWidth and hasAnimation behaviour from @8x8/oxygen-loaders source or Storybook; write descriptions in props.md."
    blocks: []
    dependency: []

  - id: GAP-003
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## Props — Default column, all rows"
      finding: >
        All five props show '—' in the Default column. The OX MCP did not return default
        values. Actual defaults (e.g. `hasAnimation` likely defaults to `true`,
        `size` likely defaults to `"default"`) are unconfirmed.
    fix_action: "Check @8x8/oxygen-loaders source for default prop values; populate the Default column in props.md."
    blocks: []
    dependency: []

  - id: GAP-004
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## WCAG 2.1 AA checklist"
      finding: >
        WCAG 2.3.3 (Animation from Interactions) is not included in the checklist.
        The Spinner features a continuous rotation animation relevant to this criterion,
        and the motion sensitivity section already recommends `hasAnimation=false` for
        `prefers-reduced-motion` users — the matching WCAG row is missing.
    fix_action: "Add WCAG 2.3.3 row to accessibility.md checklist: 'Must provide — respect prefers-reduced-motion via hasAnimation=false or CSS media query.'"
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ~
      location: "component-lib/Spinner/ directory"
      finding: "Spinner-usage.md is absent — figma-extract-usage has not been run."
    fix_action: "Run figma-extract-usage for Spinner to produce Spinner-usage.md with Do/Don't guidelines."
    blocks: [doc-rewrite/usage-dimension]
    dependency: []

  - id: GAP-006
    dimension: tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Theme tokens"
      finding: >
        No token bindings extracted for the Spinner component. The Figma Variables API
        requires an Enterprise plan and returned a permissions error; the figma-console
        Desktop Bridge was offline. Token names for spinner stroke colour, track colour,
        text colour, and animation timing are unknown.
    fix_action: "Resolve token bindings from UI-Foundations library (file key iVY5nI8JAxM05Apnnvozzs) using figma_execute + getVariableByIdAsync on the Spinner variant nodes, or enable Variables API access."
    blocks: [doc-rewrite/tokens-dimension, storybook-generate]
    dependency: []

  - id: GAP-007
    dimension: figma
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Spinner-figma.md
      location: "## Color & token bindings"
      finding: >
        The '## Color & token bindings' section contains only the NOT FOUND marker.
        Both stroke/arc colour and supporting-text typography token bindings are absent
        due to the same Variables API / Desktop Bridge unavailability as GAP-006.
    fix_action: "Re-run figma-extract for Spinner once Variables API access or Desktop Bridge is available; populate Color & token bindings section."
    blocks: [doc-rewrite/tokens-dimension]
    dependency: [GAP-006]

  - id: GAP-008
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Spinner-figma.md
      location: "## Structure & spacing — Internal spacing / Auto-layout"
      finding: >
        Inner padding, gap between spinner arc and supporting text, arc icon dimensions,
        and auto-layout direction are all NOT FOUND. get_design_context required selection
        in Figma Desktop and was unavailable during extraction.
    fix_action: "Open Spinner node in Figma Desktop, select it, and re-run figma-extract (or call get_design_context directly) to populate inner spacing data."
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: figma / tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Spinner-figma.md
      location: "## Color & token bindings — Text styles"
      finding: >
        Text style (typography token) for the supporting text label is not extracted.
        The Styles API returned 0 styles for this file; Desktop Bridge was offline.
    fix_action: "Resolve text style token (likely a body/caption token from the UI-Foundations library) alongside GAP-007 resolution."
    blocks: []
    dependency: [GAP-006]

  - id: GAP-010
    dimension: figma / props
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Spinner-figma.md / props.md
      location: "Spinner-figma.md § API Variant axes — isInverted row; props.md — no isInverted prop"
      finding: >
        The Figma component set exposes `isInverted` as a first-class variant axis
        (values: no / yes), meaning designers can deliberately set a spinner to its
        inverted colour variant for use on dark or brand-coloured backgrounds.
        The Oxygen React component (`@8x8/oxygen-loaders`) has no `isInverted` prop.
        It is unclear whether: (a) the component handles inversion automatically via
        theme/surface context; (b) an `isInverted` prop should be added; or (c) the
        Figma variant is design-only and consuming teams must apply their own CSS.
    fix_action: "Human decision required: confirm whether isInverted is (a) auto-handled by theme context, (b) a missing prop to be added to the React component, or (c) design-only. Document the resolution in props.md and Spinner-figma.md."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-011
    dimension: figma / props
    severity: minor
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md / Spinner-figma.md
      location: "props.md § spinnerSize key values — large2x row; Spinner-figma.md § API Variant axes — size values"
      finding: >
        props.md documents `"large2x"` as a valid `spinnerSize` key (sourced from
        Storybook examples). The Figma component set only defines `size=default` and
        `size=small` — `large2x` is absent from the component set. One of the two
        sources is incomplete.
    fix_action: "Verify whether a large2x Figma variant exists (possibly in a different file or unpublished). If it exists: locate and document. If it was intentionally removed from Figma: note it as code-only. If the size key was renamed: align both sources."
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: accessibility
    confidence: heuristic
    note: >
      `role="status"` in accessibility.md is labelled "(inferred from usage)". The actual
      Oxygen Spinner implementation may render the live region differently or not at all.
      Verify the rendered DOM (`role`, `aria-live`, `aria-busy`) before shipping docs.

  - id: WARN-002
    dimension: accessibility / props
    confidence: heuristic
    note: >
      accessibility.md recommends `hasAnimation=false` for `prefers-reduced-motion` users
      but does not confirm that the component actually reads the OS preference automatically.
      If `hasAnimation` defaults to `true` and requires manual intervention, consuming teams
      must wire it themselves — this should be documented explicitly.
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
siblings:
  - "[[Spinner/props]]"
  - "[[Spinner/examples]]"
  - "[[Spinner/tokens]]"
  - "[[Spinner/accessibility]]"
  - "[[Spinner/Spinner-figma]]"
tags:
  - oxygen
  - component/Spinner
  - role/audit
  - stage/blocked
---

# Spinner — Documentation Audit

> **Verdict: NO** — resolve 2 CONFLICTs before running doc-rewrite.
>
> Rubric version: 1.0 · Audited: 2026-05-05

---

## File Inventory

| File | Status | Produced by |
|------|--------|-------------|
| `props.md` | ✅ Present | oxygen-mcp-extract |
| `examples.md` | ✅ Present | oxygen-mcp-extract |
| `tokens.md` | ✅ Present | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | oxygen-mcp-extract |
| `Spinner-figma.md` | ✅ Present | figma-extract |
| `figma-screenshot-Spinner.png` | ✅ Present | figma-extract |
| `Spinner-usage.md` | ❌ **MISSING** | figma-extract-usage |
| `Spinner-pui.md` | ⚠️ Missing — confirmed no PUI context via MCP search | pui-mcp-extract |

---

## Dimension Scores

| Dimension | Score | Coverage | Notes |
|-----------|-------|----------|-------|
| Props | 0.78 | 7/9 | 2 props have empty descriptions; all defaults undocumented |
| Examples | 0.75 | 6/8 | Clean snippets for all sizes; missing `hasAnimation` example |
| Tokens | 0.25 | 1/4 | **Major SOURCE_GAP** — Variables API unavailable; no token bindings |
| Accessibility | 0.83 | 10/12 | WCAG 2.3.3 missing; `role="status"` inferred |
| Figma | 0.67 | 8/12 | Good anatomy + variant coverage; no color/token/spacing data |
| Usage | 0.00 | — | ❌ SOURCE_GAP (major) — file missing |
| PUI | 1.00 | PASS | Confirmed no application-layer concerns |
| **Available avg** | **0.71** | | (excl. usage) |
| **Overall avg** | **0.61** | | |

---

## Conflicts — must resolve before doc-rewrite

### GAP-010 · CONFLICT · Major — `isInverted` Figma variant vs. no React prop

The Figma component set has `isInverted` as a first-class variant (no / yes). The React component has no such prop. Three possible resolutions:
- **(a)** Theme/surface context handles it automatically → document in props.md as "no prop needed"
- **(b)** A React prop is missing → add `isInverted: boolean` to the package
- **(c)** Design-only intent → note in docs that consuming teams manage this via CSS/theming

**Fix:** Human decision required.

### GAP-011 · CONFLICT · Minor — `large2x` in code, absent from Figma

React `spinnerSize` enum includes `"large2x"` (evidenced in Storybook). Figma component set only defines `default` and `small`. One source is stale.

**Fix:** Locate `large2x` in Figma or confirm it is code-only; align both sources.

---

## Gap Summary

| Count | Category |
|-------|----------|
| 2 | CONFLICTs — **blocking doc-rewrite** |
| 5 | SOURCE_GAPs (2 major, 3 minor) |
| 4 | DOC_GAPs (all minor) |
| 2 | Warnings (heuristic, advisory) |

---

## Gaps

### SOURCE_GAP — Major

**GAP-005** · Usage
> `Spinner-usage.md` absent — `figma-extract-usage` not run.
> **Fix:** Run `figma-extract-usage` for Spinner.

**GAP-006** · Tokens
> No theme token bindings extracted. Variables API requires Enterprise plan; Desktop Bridge offline.
> **Fix:** Resolve via `figma_execute + getVariableByIdAsync` on spinner nodes, or enable Variables API on the UI-Foundations file (`iVY5nI8JAxM05Apnnvozzs`).

**GAP-007** · Figma _(depends on GAP-006)_
> `Spinner-figma.md §Color & token bindings` is entirely empty — stroke, track, and text colour tokens absent.
> **Fix:** Re-run figma-extract once Variables API / Desktop Bridge is available.

### SOURCE_GAP — Minor

**GAP-008** · Figma
> Inner padding, gap between arc and text, icon dimensions, and auto-layout direction not extracted.
> **Fix:** Select Spinner node in Figma Desktop and call `get_design_context`.

**GAP-009** · Figma / Tokens _(depends on GAP-006)_
> Typography token for supporting text label not extracted.
> **Fix:** Resolve alongside GAP-007.

### DOC_GAP — Minor (auto-fixable)

**GAP-001** · All OX files
> `props.md`, `examples.md`, `tokens.md`, `accessibility.md` — "See also" lines all missing the `Spinner-figma.md` cross-link.
> **Fix:** Append `· [Spinner-figma.md](Spinner-figma.md)` to the See also line in all four files.

**GAP-004** · Accessibility
> WCAG 2.3.3 (Animation from Interactions) missing from checklist. Spinner has a continuous rotation; `prefers-reduced-motion` guidance is already present.
> **Fix:** Add WCAG 2.3.3 row.

### DOC_GAP — Minor (requires source verification)

**GAP-002** · Props
> `strokeWidth` and `hasAnimation` props have empty descriptions.
> **Fix:** Check `@8x8/oxygen-loaders` source; write descriptions.

**GAP-003** · Props
> All five prop defaults undocumented (show '—').
> **Fix:** Check `@8x8/oxygen-loaders` source for actual defaults.

---

## Warnings

**WARN-001 (Accessibility):** `role="status"` is inferred. Verify the rendered DOM before shipping docs — the actual live region role/attributes may differ.

**WARN-002 (Accessibility / Props):** `hasAnimation` is recommended for `prefers-reduced-motion` but it is unconfirmed whether the component automatically responds to the OS preference or requires manual wiring by the consumer.

---

## Suggested next actions

```
1. Resolve GAP-010 (isInverted conflict)  — human decision, blocks doc-rewrite
2. Resolve GAP-011 (large2x conflict)     — locate in Figma or confirm code-only
3. Fix GAP-001 (cross-links)              — 5-min auto-fix, 4 files
4. Fix GAP-004 (WCAG 2.3.3)              — auto-fixable in accessibility.md
5. Verify GAP-002 / GAP-003               — check @8x8/oxygen-loaders source
6. Run figma-extract-usage                — closes GAP-005
7. Resolve token bindings (GAP-006/007)   — needs Variables API access or figma_execute
8. Run doc-rewrite                        — after conflicts resolved
```

_Source: doc-audit skill v1.0 · Audited from component-lib/Spinner/ · 2026-05-05_
