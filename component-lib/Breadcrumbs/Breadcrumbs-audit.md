---
rubric_version: "1.0"
component: Breadcrumbs
package: "@8x8/oxygen-breadcrumbs"
audit_date: "2026-05-05"
auditor: doc-audit skill
prior_audit: "2026-04-30"

file_inventory:
  present:
    - props.md
    - examples.md
    - tokens.md
    - accessibility.md
    - Breadcrumbs-figma.md
    - Breadcrumbs-pui.md
  missing:
    - Breadcrumbs-usage.md
    - figma-screenshot-Breadcrumbs.png

dimension_scores:
  props:        { score: 0.70, coverage: "7/10" }
  examples:     { score: 0.57, coverage: "4/7" }
  tokens:       { score: 0.55, coverage: "5/9" }
  accessibility:{ score: 0.78, coverage: "7/9" }
  figma:        { score: 0.73, coverage: "8/11" }
  usage:        { score: 0.00, coverage: "0/0 — SOURCE_GAP (file missing)" }
  pui:          { score: 1.00, coverage: "PASS — no relevant PUI context (engineer-confirmed)" }

overall_score: 0.62

counts:
  doc_gaps: 4
  source_gaps: 7
  conflicts: 0
  warnings: 3

verdict: YES
verdict_reason: >
  Zero CONFLICTs and zero blocker-severity gaps — doc-rewrite can proceed.
  Token dimension re-scored from 0.25 → 0.55: rest-state token names for all
  three interactive element types (link, ellipsis, separator/current page) and
  typography style are fully documented in Breadcrumbs-figma.md and are available
  for doc-rewrite to synthesise. tokens.md itself remains a stub that only
  documents the gap (DOC_GAP, auto-fixable). Hover / active / focus state token
  bindings remain unresolved (SOURCE_GAP, major) — these atoms exist in a shared
  Figma library not accessible via this file's Variables API.
  Breadcrumbs-usage.md is absent (SOURCE_GAP, major) — usage dimension will
  be sparse or skipped in the spec. No CONFLICTs block rewrite.

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
        explicitly but contains no resolved token names. The MCP is the authoritative
        source for officially registered tokens; the Figma-extracted names are design
        intent, not confirmed MCP registry entries.
    fix_action: >
      Check @8x8/oxygen-breadcrumbs source stylesheet or raise with the Oxygen team
      to expose component tokens via the MCP theme-tokens endpoint.
    blocks:
      - doc-rewrite/tokens-dimension (partial — Figma data can substitute at lower confidence)
      - storybook-generate

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
        Token data extracted from Figma design context is present in Breadcrumbs-figma.md:
          - --actions/action08 (link text, ellipsis rest): light #0056e0, dark #99bbf3
          - --interactive/active07 (ellipsis menu-open/active): light #0045b3, dark #0056e0
          - --text/textcolor01 (separator, current-page label): light #26252a, dark white
          - --ui/ui01 (overflow menu border, light mode only): #ebeae1
          - --typography/body01/* (font-size 14px, weight 400, line-height 20px,
            letter-spacing -0.06px) — all text elements
        None of this data has been migrated into tokens.md. tokens.md remains a stub
        that only records the absence of MCP token data, without referencing the
        Figma-extracted names that are available for doc-rewrite.
    fix_action: >
      Migrate token data from Breadcrumbs-figma.md ## Color & token bindings and
      ## Text styles into tokens.md. Add columns: token-name, collection, light value,
      dark value, element(s). Note that these come from Figma CSS variable references,
      not the MCP registry — mark confidence accordingly.
    blocks:
      - doc-rewrite/tokens-dimension

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
        (total_variables: 0); all tokens come from a shared library inaccessible via
        this file's Variables API. Only rest-state token values were returned by the
        design context extraction. The atoms for these states exist in the file at
        nodes 20648:30062 and 22076:37746 but their fill bindings were not returned.
    fix_action: >
      Access the shared Oxygen token library for Figma file 5YihJ5WuDvnvrlrRMC4sBp
      (file key iVY5nI8JAxM05Apnnvozzs per reference_figma_foundations_library.md —
      use figma_execute + getVariableByIdAsync to resolve). Retrieve hover / active /
      focus token names for the breadcrumb link atom; update tokens.md and
      Breadcrumbs-figma.md Interaction states table.
    blocks:
      - doc-rewrite/tokens-dimension (hover/focus remain partial in spec)

  - id: GAP-004
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ~
      location: "component-lib/Breadcrumbs/ directory"
      finding: >
        Breadcrumbs-usage.md is absent — figma-extract-usage skill has not been run.
        No Do/Don't editorial guidance is available.
    fix_action: >
      Run figma-extract-usage for Breadcrumbs to produce Do/Don't editorial guidelines
      from the Figma Examples page. If no Examples page exists for this component,
      mark the gap as permanently missing SOURCE_GAP.
    blocks:
      - doc-rewrite/usage-dimension

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
    fix_action: >
      Export the Breadcrumbs component set from Figma (node 21927:40413,
      file 5YihJ5WuDvnvrlrRMC4sBp) and save as figma-screenshot-Breadcrumbs.png
      in component-lib/Breadcrumbs/.
    blocks:
      - docusaurus-generate

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
    fix_action: >
      Request the Figma component owner to add accessibility annotations (ARIA role,
      focus order, keyboard behaviour) to node 21927:40413.
    blocks: []

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
    fix_action: >
      Add [Breadcrumbs-figma.md](Breadcrumbs-figma.md) to the See also line in
      props.md, examples.md, tokens.md, and accessibility.md.
    blocks: []

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
    fix_action: >
      Verify isActive prop existence, type, default, and description against
      @8x8/oxygen-breadcrumbs source or published TypeScript types; update props.md.
    blocks: []

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
    fix_action: >
      Inspect @8x8/oxygen-breadcrumbs TypeScript types or source for the
      BreadcrumbsTheme interface shape; document the theme prop structure in props.md.
    blocks: []

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
    fix_action: >
      Source authoritative code examples from the @8x8/oxygen-breadcrumbs Storybook
      or source repository; add examples for dark mode, ariaLabel, and a React-node
      separator.
    blocks: []

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
    fix_action: >
      Ask the Figma component owner to rename the text property from 'curent page'
      to 'current page' in component node 21927:40413; re-extract after correction.
    blocks: []

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
      resolves to #0056e0 on a white background — this likely meets AA contrast (4.5:1)
      but has not been formally verified. The focus ring token binding is unresolved
      (GAP-003), so focus contrast cannot be confirmed until hover/focus tokens are
      resolved.

  - id: WARN-003
    dimension: figma
    confidence: heuristic
    note: >
      The overflow menu (collapse?=yes, menu?=yes) shows a generic "Slot" placeholder
      in Figma. It is unclear whether this slot is a designer customisation hook for
      Figma comps only, or whether the Oxygen component ships with a real dropdown
      overlay that consumers populate. The collapsed variant in Figma uses only 6
      predefined combinations — no explicit "items in overflow" slot API is documented
      in props.md. This design intent should be confirmed with the Oxygen team before
      the overflow menu slot is described in the spec.
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
siblings:
  - "[[Breadcrumbs/props]]"
  - "[[Breadcrumbs/examples]]"
  - "[[Breadcrumbs/tokens]]"
  - "[[Breadcrumbs/accessibility]]"
  - "[[Breadcrumbs/Breadcrumbs-figma]]"
  - "[[Breadcrumbs/Breadcrumbs-pui]]"
tags:
  - oxygen
  - component/Breadcrumbs
  - role/audit
  - stage/spec_ready
---

# Breadcrumbs — Audit Report

> **Rubric version:** 1.0 · **Audit date:** 2026-05-05 · **Prior audit:** 2026-04-30 · **Verdict:** YES

---

## Re-audit context

This audit supersedes the 2026-04-30 audit. The primary change is a re-evaluation of the **tokens** dimension, which was scored 0.25 in the prior audit because `tokens.md` is a near-empty stub. That score was overly pessimistic: `Breadcrumbs-figma.md` contains well-structured token data for all rest-state elements that `doc-rewrite` can synthesise. The re-scored token dimension is **0.55**, reflecting:

- Rest-state token names for all interactive element types are documented in `Breadcrumbs-figma.md` (5 of ~9 distinct token slots have resolved names)
- `tokens.md` itself needs updating (DOC_GAP, auto-fixable — GAP-002, unchanged from prior)
- Hover / active / focus state token bindings remain unresolved SOURCE_GAPs (GAP-003, unchanged)
- Hardcoded overflow menu values remain unresolved SOURCE_GAPs (noted in figma.md)

No other dimension scores have changed. All gaps from the prior audit carry forward with the same IDs.

---

## File Inventory

| File | Status | Produced by |
|------|--------|-------------|
| `props.md` | Present | oxygen-mcp-extract |
| `examples.md` | Present | oxygen-mcp-extract |
| `tokens.md` | Present (stub — no resolved token names) | oxygen-mcp-extract |
| `accessibility.md` | Present | oxygen-mcp-extract |
| `Breadcrumbs-figma.md` | Present | figma-extract |
| `Breadcrumbs-usage.md` | **MISSING** | figma-extract-usage |
| `Breadcrumbs-pui.md` | Present — `NO RELEVANT PUI CONTEXT` (engineer-confirmed) | pui-mcp-extract |
| `figma-screenshot-Breadcrumbs.png` | **MISSING** (GAP-005) | figma-extract |

---

## Dimension Scores

| Dimension | Score | Coverage | Delta vs prior | Status |
| --------- | ----- | -------- | -------------- | ------ |
| Props | 0.70 | 7/10 | — | Available |
| Examples | 0.57 | 4/7 | — | Available — all examples are constructed, not MCP-authoritative |
| Tokens | **0.55** | **5/9** | **+0.30** | Available — rest-state tokens in figma.md; tokens.md needs migration |
| Accessibility | 0.78 | 7/9 | — | Available |
| Figma | 0.73 | 8/11 | — | Available |
| Usage | 0.00 | 0/0 | — | SOURCE_GAP — file missing |
| PUI | 1.00 | PASS | — | Resolved — no relevant context |
| **Overall score** | **0.62** | | **+0.04** | |

> **Token dimension re-score rationale:**
> The prior score of 0.25 treated the token dimension as nearly empty because `tokens.md` contained no resolved names. However, `Breadcrumbs-figma.md` documents the following token bindings extracted from Figma design context:
>
> | Element | Token | Light | Dark |
> | ------- | ----- | ----- | ---- |
> | Link text (rest) | `--actions/action08` | `#0056e0` | `#99bbf3` |
> | Ellipsis (rest) | `--actions/action08` | `#0056e0` | `#99bbf3` |
> | Ellipsis (menu open / active) | `--interactive/active07` | `#0045b3` | `#0056e0` |
> | Separator text | `--text/textcolor01` | `#26252a` | `white` |
> | Current page label | `--text/textcolor01` | `#26252a` | `white` |
> | Overflow menu border (light) | `--ui/ui01` | `#ebeae1` | — (hardcoded) |
> | All text | `--typography/body01/*` | 14px / 400 / 20px / -0.06px | same |
>
> This data was extracted from Figma CSS variable references and is available for `doc-rewrite` to synthesise. The coverage is 5/9 because hover/active/focus state tokens and overflow menu dark-mode values remain unresolved.

---

## Gap Summary

| Count | Category |
|-------|----------|
| 0 | CONFLICTs — **no blocks on doc-rewrite** |
| 7 | SOURCE_GAPs (3 major: GAP-001 tokens/MCP, GAP-003 hover/focus tokens, GAP-004 usage; 4 minor: GAP-005 screenshot, GAP-006 Figma a11y annotations, GAP-009 theme prop shape, GAP-011 Figma typo) |
| 4 | DOC_GAPs (1 major: GAP-002 tokens.md migration; 3 minor: GAP-007 cross-links, GAP-008 isActive, GAP-010 examples) |
| 3 | Warnings (WARN-001, WARN-002, WARN-003 — unchanged from prior) |

---

## Gaps

### SOURCE_GAPs

#### GAP-001 · Tokens · MAJOR
**Finding:** `get-theme-tokens` returned 0 results — no Oxygen theme tokens registered for Breadcrumbs in the MCP. `tokens.md` documents this gap but contains no resolved token names. The MCP is the authoritative registry; Figma-extracted names are design intent, not confirmed MCP entries.
**Fix:** Check `@8x8/oxygen-breadcrumbs` source stylesheet or raise with the Oxygen team to expose tokens via the MCP theme-tokens endpoint.

#### GAP-003 · Tokens · MAJOR
**Finding:** Hover, active, and focus state token bindings for `_Text link breadcrumb` and `_Text link elipsis` are unresolved. The Figma file has 0 local variables — all tokens are in a shared library not accessible via this file's Variables API. Only rest-state values were returned.
**Fix:** Access the shared Oxygen token library (`iVY5nI8JAxM05Apnnvozzs` per memory reference) using `figma_execute + getVariableByIdAsync`; retrieve hover/active/focus token names for the link atom; update `tokens.md` and `Breadcrumbs-figma.md`.

#### GAP-004 · Usage · MAJOR
**Finding:** `Breadcrumbs-usage.md` absent — `figma-extract-usage` has not been run.
**Fix:** Run `figma-extract-usage` for Breadcrumbs to produce Do/Don't editorial guidelines from the Figma Examples page.

#### GAP-005 · Figma · MINOR
**Finding:** Screenshot returned as embedded MCP image but not saved as `figma-screenshot-Breadcrumbs.png`. File absent from directory.
**Fix:** Export from Figma node `21927:40413` (file `5YihJ5WuDvnvrlrRMC4sBp`) and save as `figma-screenshot-Breadcrumbs.png`.

#### GAP-006 · Figma · MINOR
**Finding:** No accessibility annotations in Figma — `annotations` array was empty; ARIA role, focus order, and keyboard behaviour all marked `NOT ANNOTATED IN FIGMA`.
**Fix:** Request Figma component owner to add accessibility annotations to node `21927:40413`.

#### GAP-009 · Props · MINOR
**Finding:** `theme` prop documented only as `object` — internal shape not returned by MCP and not documented anywhere.
**Fix:** Inspect `@8x8/oxygen-breadcrumbs` TypeScript types for `BreadcrumbsTheme` interface; document in `props.md`.

---

#### GAP-011 · Figma · MINOR (design gap / typo)
**Finding:** Figma text property is named `curent page` (typo — missing one 'r'). Documented in `Breadcrumbs-figma.md` with a note, but the error exists upstream.
**Fix:** Ask Figma component owner to rename the property to `current page` in node `21927:40413`; re-extract after correction.

---

### DOC_GAPs

#### GAP-002 · Tokens · MAJOR · auto-fixable
Token data present in `Breadcrumbs-figma.md` (`--actions/action08`, `--text/textcolor01`, `--interactive/active07`, `--ui/ui01`, `--typography/body01/*`) has not been migrated into `tokens.md`. `tokens.md` is a stub that only records the MCP gap without referencing available Figma-extracted names.
**Fix:** Migrate token table from `Breadcrumbs-figma.md ## Color & token bindings` and `## Text styles` into `tokens.md`. Mark confidence as "Figma design context (not MCP-registered)".

#### GAP-007 · All OX files · MINOR · auto-fixable
"See also" navigation in `props.md`, `examples.md`, `tokens.md`, and `accessibility.md` does not include a link to `Breadcrumbs-figma.md`.
**Fix:** Add `[Breadcrumbs-figma.md](Breadcrumbs-figma.md)` to the "See also" line in all four files.

#### GAP-008 · Props · MINOR · requires verification
`isActive` prop on `Breadcrumb` documented as "observed in storybook" — not returned by `get-component-props`. Type, default, and behaviour are inferred.
**Fix:** Verify `isActive` against `@8x8/oxygen-breadcrumbs` source or TypeScript types; update `props.md`.

#### GAP-010 · Examples · MINOR · not auto-fixable
`get-component-examples` returned 0 clean snippets. All four code examples constructed from storybook story. No examples for: dark mode, `ariaLabel` override, `theme` prop, or React-node separator.
**Fix:** Source authoritative examples from `@8x8/oxygen-breadcrumbs` Storybook or source repo.

---

## Warnings

**WARN-001 (Accessibility):** ARIA roles (`<nav>`, `<ol>`, `aria-current`, `<button>`) are inferred from expected behaviour, not confirmed from the rendered DOM. Verify against rendered output before shipping docs.

**WARN-002 (Accessibility):** WCAG 1.4.3 (contrast) and 2.4.7 (focus visible) marked "Unverified". `--actions/action08` (#0056e0 on white) likely meets AA but is unconfirmed. Focus ring contrast cannot be checked until GAP-003 is resolved.

**WARN-003 (Figma):** The overflow menu (`menu?=yes`) shows a generic "Slot" placeholder in Figma. It is unclear whether this is a designer composition hook or a real runtime dropdown. No props API for populating overflow menu content is documented in `props.md`. Confirm design intent with the Oxygen team before describing this slot in the spec.

---

## Verdict: YES — ready for doc-rewrite

No CONFLICTs, no blocker-severity gaps. `doc-rewrite` can proceed.

Recommended order:

```
1. Fix GAP-002 (migrate token table from figma.md into tokens.md — 10-min auto-fix)
2. Fix GAP-007 (add Breadcrumbs-figma.md to See also in 4 files — 5-min auto-fix)
3. Run doc-rewrite           → produces Breadcrumbs-spec.md
                                (tokens synthesised from figma.md at "Figma context" confidence;
                                 usage dimension sparse/skipped)
4. Export screenshot         → GAP-005 → save figma-screenshot-Breadcrumbs.png
5. Run figma-extract-usage   → GAP-004 → re-run doc-audit if needed
6. Resolve hover/focus tokens → GAP-003 (use iVY5nI8JAxM05Apnnvozzs shared library)
7. Verify isActive prop      → GAP-008 (source code or Storybook)
8. Verify ARIA DOM output    → WARN-001 (rendered DOM inspection)
9. Confirm overflow slot intent → WARN-003 (Oxygen team)
10. Fix Figma typo "curent page" → GAP-011 (Figma-side work)
```

Source: doc-audit skill · Rubric v1.0 · Re-audit 2026-05-05 (supersedes 2026-04-30)
