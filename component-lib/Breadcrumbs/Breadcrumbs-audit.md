---
rubric_version: "1.0"
component: Breadcrumbs
audit_date: "2026-04-30"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - Breadcrumbs-figma.md
  - Breadcrumbs-pui.md

files_missing:
  - Breadcrumbs-usage.md

dimension_scores:
  props:        { score: 0.70, coverage: "7/10" }
  examples:     { score: 0.57, coverage: "4/7"  }
  tokens:       { score: 0.25, coverage: "2/8"  }
  accessibility:{ score: 0.78, coverage: "7/9"  }
  figma:        { score: 0.73, coverage: "8/11" }
  usage:        { score: 0.00, coverage: "0/0 — SOURCE_GAP" }
  pui:          { score: 1.00, coverage: "PASS — NO RELEVANT PUI CONTEXT confirmed by engineer" }

available_dimensions_avg: 0.67
overall_avg: 0.58

counts:
  doc_gaps: 4
  source_gaps: 7
  conflicts: 0
  warnings: 3

verdict: YES
verdict_reason: >
  Zero CONFLICTs and zero blocker-severity gaps — doc-rewrite can proceed.
  The missing Breadcrumbs-usage.md (SOURCE_GAP, major) means the usage dimension
  will be skipped or sparse in the spec. The tokens dimension is weak (0.25) but the
  token data extracted from Figma design context (actions/action08, text/textcolor01,
  typography/body01) is present in Breadcrumbs-figma.md and can be synthesised by
  doc-rewrite. Hover/active/focus state tokens are unresolved (SOURCE_GAP) and will
  remain partial in the spec until the shared Figma library is accessible.

suggested_next_action: >
  1. Fix GAP-007 (broken "See also" cross-links → 4 files, 5-min auto-fix before rewrite)
  2. Run doc-rewrite → produces Breadcrumbs-spec.md
     (tokens dimension will be partially derived from figma.md; usage dimension sparse)
  3. Export screenshot from Figma node 21927:40413 → GAP-005
  4. Run figma-extract-usage for Breadcrumbs → GAP-004
  5. Resolve hover/focus token names via shared Figma library → GAP-003
  6. Verify isActive prop signature in @8x8/oxygen-breadcrumbs source → GAP-008
  7. Verify ARIA role implementation in rendered DOM → WARN-001
  8. Correct Figma typo "curent page" → GAP-011 (Figma-side work)

gaps:
  - id: GAP-001
    dimension: tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Theme tokens"
      finding: >
        get-theme-tokens returned 0 results for "breadcrumb". No Oxygen theme tokens
        are registered against this component in the MCP. tokens.md documents the gap
        explicitly but contains no resolved token names.
    fix_action: "Check @8x8/oxygen-breadcrumbs source stylesheet or raise with the Oxygen team to expose component tokens via the MCP"
    blocks: [doc-rewrite/tokens-dimension, storybook-generate]
    dependency: []

  - id: GAP-002
    dimension: tokens
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: Breadcrumbs-figma.md
      location: "## Color & token bindings and ## Text styles"
      finding: >
        Token data extracted from Figma design context is present in Breadcrumbs-figma.md
        (--actions/action08, --text/textcolor01, --interactive/active07, --ui/ui01,
        --typography/body01/*) but has not been synthesised into tokens.md.
        tokens.md documents only the gap — it does not reference or incorporate the
        Figma-extracted token names. doc-rewrite must merge these.
    fix_action: "Migrate token data from Breadcrumbs-figma.md ## Color & token bindings into tokens.md; add token-name, collection, light/dark value columns"
    blocks: [doc-rewrite/tokens-dimension]
    dependency: []

  - id: GAP-003
    dimension: tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Breadcrumbs-figma.md
      location: "## Interaction states and ## Color & token bindings — strategy note"
      finding: >
        Hover, active, and focus state token bindings for _Text link breadcrumb and
        _Text link elipsis are unresolved. The Figma file has 0 local variables
        (total_variables: 0); all tokens come from a shared library not accessible
        via this file's Variables API. Only rest-state token values were returned.
    fix_action: "Access the shared Oxygen token library for Figma file 5YihJ5WuDvnvrlrRMC4sBp (or ask Oxygen team) to retrieve hover/active/focus token names for the breadcrumb link atom; update tokens.md and Breadcrumbs-figma.md"
    blocks: [doc-rewrite/tokens-dimension]
    dependency: []

  - id: GAP-004
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ~
      location: "component-lib/Breadcrumbs/ directory"
      finding: "Breadcrumbs-usage.md is absent — figma-extract-usage skill has not been run"
    fix_action: "Run figma-extract-usage for Breadcrumbs to produce Do/Don't editorial guidelines from the Figma Examples page"
    blocks: [doc-rewrite/usage-dimension]
    dependency: []

  - id: GAP-005
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Breadcrumbs-figma.md
      location: "## Visual reference"
      finding: >
        The screenshot was captured by the MCP and returned as an embedded image in
        the tool response but was not saved to disk as figma-screenshot-Breadcrumbs.png.
        The file does not exist in component-lib/Breadcrumbs/.
    fix_action: "Export the Breadcrumbs component set from Figma (node 21927:40413, file 5YihJ5WuDvnvrlrRMC4sBp) and save as figma-screenshot-Breadcrumbs.png in component-lib/Breadcrumbs/"
    blocks: [docusaurus-generate]
    dependency: []

  - id: GAP-006
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Breadcrumbs-figma.md
      location: "## Accessibility (from Figma annotations only)"
      finding: >
        No accessibility annotations are present in the Figma component. ARIA role,
        focus order, and keyboard interaction notes are all marked NOT ANNOTATED IN FIGMA.
        The annotations array returned by figma_get_component was empty.
    fix_action: "Request the Figma component owner to add accessibility annotations (ARIA role, focus order, keyboard behaviour) to node 21927:40413"
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "> See also: line 3"
      finding: >
        The "See also" navigation line in props.md, examples.md, tokens.md, and
        accessibility.md does not include a link to Breadcrumbs-figma.md. All four
        files cross-link only among themselves, leaving the Figma spec unreachable
        via internal navigation.
    fix_action: "Add [Breadcrumbs-figma.md](Breadcrumbs-figma.md) to the See also line in props.md, examples.md, tokens.md, and accessibility.md"
    blocks: []
    dependency: []

  - id: GAP-008
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## Breadcrumb Props — isActive row, Note block"
      finding: >
        The isActive prop is documented as "observed in the storybook example code but
        was not returned by get-component-props". Its type (boolean), default (false),
        and behaviour (renders as plain text, not a link) are inferred — not confirmed
        from the Oxygen MCP or the component source.
    fix_action: "Verify isActive prop existence, type, default, and description against @8x8/oxygen-breadcrumbs source or published TypeScript types; update props.md"
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: props
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## Breadcrumbs Props — theme row, Type column"
      finding: >
        The theme prop type is documented only as 'object'. Its internal shape
        (property names, token references, accepted value types) was not returned
        by the Oxygen MCP and is not documented anywhere in the extracted files.
    fix_action: "Inspect @8x8/oxygen-breadcrumbs TypeScript types or source for the BreadcrumbsTheme interface shape; document the theme prop structure in props.md"
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "Note block at bottom of file"
      finding: >
        get-component-examples returned 0 clean snippets. All four code examples were
        constructed from the storybook documentation story and documented behaviour —
        none are MCP-authoritative. No examples exist for: dark mode (mode="dark"),
        ariaLabel override, theme prop usage, or custom separator as a React element.
    fix_action: "Source authoritative code examples from the @8x8/oxygen-breadcrumbs Storybook or source repository; add examples for dark mode, ariaLabel, and a React-node separator"
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Breadcrumbs-figma.md
      location: "## Anatomy — row 7 (Curent page) and ## API — Text properties"
      finding: >
        The Figma text property name contains a typo: "curent page#20679:3" (missing
        one 'r'). This is a Figma-side error — the property name in the design file
        does not match the intended "current page" label. It is documented in
        Breadcrumbs-figma.md with a note, but the typo exists upstream in Figma.
    fix_action: "Ask the Figma component owner to rename the text property from 'curent page' to 'current page' in component node 21927:40413; re-extract after correction"
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: accessibility
    confidence: heuristic
    note: >
      ARIA roles in accessibility.md (nav, ol, a, aria-current, button) are inferred
      from the component's expected behaviour and the WAI-ARIA breadcrumb pattern.
      They are not confirmed from the Oxygen component's rendered DOM. If the
      implementation uses div elements without explicit roles, screen readers will not
      announce the breadcrumb navigation pattern correctly. Verify against the rendered
      output before shipping docs.

  - id: WARN-002
    dimension: accessibility
    confidence: heuristic
    note: >
      WCAG 1.4.3 (Contrast Minimum) and 2.4.7 (Focus Visible) are both marked
      "Unverified" in accessibility.md. The link colour token --actions/action08
      resolves to #0056e0 on a white background — this likely meets AA contrast (4.5:1),
      but has not been formally verified. The focus ring token binding is unresolved
      (GAP-003), so focus contrast cannot be confirmed until tokens are resolved.

  - id: WARN-003
    dimension: figma
    confidence: heuristic
    note: >
      The overflow menu (collapse?=yes, ↪ menu?=yes) shows a generic "Slot" placeholder
      in Figma. It is unclear whether this slot is a designer customisation hook for
      Figma comps only, or whether the Oxygen component ships with a real dropdown
      overlay that consumers populate. The collapsed variant in Figma uses only 6
      predefined combinations — no explicit "items in overflow" slot API is documented
      in props.md. This design intent should be confirmed with the Oxygen team before
      the overflow menu slot is described in the spec.
---

# Breadcrumbs — Documentation Audit

> **Rubric version:** 1.0 · **Audit date:** 2026-04-30 · **Verdict:** YES

---

## File Inventory

| File | Status | Produced by |
|------|--------|-------------|
| `props.md` | ✅ Present | oxygen-mcp-extract |
| `examples.md` | ✅ Present | oxygen-mcp-extract |
| `tokens.md` | ✅ Present | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | oxygen-mcp-extract |
| `Breadcrumbs-figma.md` | ✅ Present | figma-extract |
| `Breadcrumbs-usage.md` | ❌ **MISSING** | figma-extract-usage |
| `Breadcrumbs-pui.md` | ✅ Present — `NO RELEVANT PUI CONTEXT` | pui-mcp-extract |

---

## Dimension Scores

| Dimension | Score | Coverage | Status |
|-----------|-------|----------|--------|
| Props | 0.70 | 7/10 | ✅ Available |
| Examples | 0.57 | 4/7 | ✅ Available — ⚠️ all constructed |
| Tokens | 0.25 | 2/8 | ✅ Available — ⚠️ major gaps |
| Accessibility | 0.78 | 7/9 | ✅ Available |
| Figma | 0.73 | 8/11 | ✅ Available |
| Usage | 0.00 | — | ❌ SOURCE_GAP (major) |
| PUI | 1.00 | PASS | ✅ Resolved — no relevant context |
| **Available avg** | **0.67** | | |
| **Overall avg** | **0.58** | | |

---

## Gap Summary

| Count | Category |
|-------|----------|
| 0 | CONFLICTs — **no blocks on doc-rewrite** |
| 7 | SOURCE_GAPs (3 major, 4 minor) |
| 4 | DOC_GAPs (all minor) |
| 3 | Warnings (heuristic, advisory) |

---

## Gaps

### SOURCE_GAPs

#### GAP-001 · Tokens · MAJOR
**Finding:** `get-theme-tokens` returned 0 results — no Oxygen theme tokens registered for Breadcrumbs in the MCP. `tokens.md` documents this gap but contains no resolved token names.
**Fix:** Check `@8x8/oxygen-breadcrumbs` source stylesheet or raise with the Oxygen team to expose tokens via the MCP.

#### GAP-003 · Tokens · MAJOR
**Finding:** Hover, active, and focus state token bindings for `_Text link breadcrumb` and `_Text link elipsis` are unresolved. Figma file has 0 local variables — all tokens are in a shared library not accessible via this file's Variables API.
**Fix:** Access the shared Oxygen token library (or ask the team) for hover/focus token names; update `tokens.md` and `Breadcrumbs-figma.md`.

#### GAP-004 · Usage · MAJOR
**Finding:** `Breadcrumbs-usage.md` absent — `figma-extract-usage` has not been run.
**Fix:** Run `figma-extract-usage` for Breadcrumbs to produce Do/Don't guidelines.

#### GAP-005 · Figma · MINOR
**Finding:** Screenshot returned as embedded MCP image but not saved as `figma-screenshot-Breadcrumbs.png`. File absent from directory.
**Fix:** Export from Figma node `21927:40413` and save as `figma-screenshot-Breadcrumbs.png`.

#### GAP-006 · Figma · MINOR
**Finding:** No accessibility annotations in Figma — `annotations` array was empty; ARIA role, focus order, and keyboard behaviour all marked `NOT ANNOTATED IN FIGMA`.
**Fix:** Request Figma component owner to add accessibility annotations to node `21927:40413`.

#### GAP-009 · Props · MINOR
**Finding:** `theme` prop documented only as `object` — internal shape (property names, token references) not returned by MCP and not documented anywhere.
**Fix:** Inspect `@8x8/oxygen-breadcrumbs` TypeScript types for `BreadcrumbsTheme` interface; document in `props.md`.

#### GAP-011 · Figma · MINOR (design gap)
**Finding:** Figma text property is named `curent page` (typo — one `r`). Documented in `Breadcrumbs-figma.md` with a note, but the error exists upstream.
**Fix:** Ask Figma component owner to rename the property to `current page` in node `21927:40413`; re-extract after.

---

### DOC_GAPs

#### GAP-002 · Tokens · MAJOR · auto-fixable
Token data extracted from Figma design context (`--actions/action08`, `--text/textcolor01`, `--interactive/active07`, `--ui/ui01`, `--typography/body01/*`) is present in `Breadcrumbs-figma.md` but not synthesised into `tokens.md`. `tokens.md` is sparse and documents only the gap.
→ **Fix:** Migrate token data from `Breadcrumbs-figma.md ## Color & token bindings` into `tokens.md`.

#### GAP-007 · All OX files · MINOR · auto-fixable
"See also" navigation in `props.md`, `examples.md`, `tokens.md`, and `accessibility.md` does not include a link to `Breadcrumbs-figma.md`. All four internal cross-links are incomplete.
→ **Fix:** Add `[Breadcrumbs-figma.md](Breadcrumbs-figma.md)` to the "See also" line in all four files.

#### GAP-008 · Props · MINOR · requires verification
`isActive` prop on `Breadcrumb` documented as "observed in storybook" — not returned by `get-component-props`. Type, default, and behaviour are inferred.
→ **Fix:** Verify `isActive` against `@8x8/oxygen-breadcrumbs` source or TypeScript types; update `props.md`.

#### GAP-010 · Examples · MINOR · not auto-fixable
All four code examples constructed from the storybook documentation story — `get-component-examples` returned 0 clean snippets. No examples for: dark mode, `ariaLabel` override, `theme` prop, or React-node separator.
→ **Fix:** Source authoritative examples from `@8x8/oxygen-breadcrumbs` Storybook or source repo.

---

## Warnings

**WARN-001 (Accessibility):** ARIA roles (`<nav>`, `<ol>`, `aria-current`, `<button>`) are inferred from expected behaviour, not confirmed from the rendered DOM. If the Oxygen implementation uses unsemantic elements, the documented ARIA pattern may not apply. Verify against rendered output before shipping docs.

**WARN-002 (Accessibility):** WCAG 1.4.3 (contrast) and 2.4.7 (focus visible) are marked "Unverified". `--actions/action08` (#0056e0 on white) likely meets AA (4.5:1) but is unconfirmed. Focus ring contrast cannot be checked until GAP-003 (hover/focus tokens) is resolved.

**WARN-003 (Figma):** The overflow menu (`↪ menu?=yes`) shows a generic "Slot" placeholder in Figma. It is unclear whether this is a designer composition hook or a real runtime dropdown. No props API for populating the overflow menu content is documented in `props.md`. Confirm design intent with the Oxygen team before describing this slot in the spec.

---

## Verdict: YES — ready for doc-rewrite

No CONFLICTs, no blocker-severity gaps. `doc-rewrite` can proceed.

Recommended order:

```
1. Fix GAP-007 (broken cross-links → add figma.md to See also in 4 files)
2. Run doc-rewrite          → produces Breadcrumbs-spec.md
                               (tokens will be derived from figma.md; usage sparse)
3. Export screenshot        → GAP-005 → save figma-screenshot-Breadcrumbs.png
4. Run figma-extract-usage  → GAP-004 → re-run doc-audit if needed
5. Resolve hover/focus tokens → GAP-003 (shared Figma library access needed)
6. Verify isActive prop     → GAP-008 (source code or Storybook check)
7. Verify ARIA DOM output   → WARN-001 (rendered DOM inspection)
8. Confirm overflow slot intent → WARN-003 (Oxygen team confirmation)
9. Fix Figma typo "curent page" → GAP-011 (Figma-side work)
```

_Source: doc-audit skill · Rubric v1.0 · 2026-04-30_
