---
rubric_version: "1.0"
component: ProgressBar
package: "@8x8/oxygen-loaders"
audit_date: "2026-05-14"
auditor: doc-audit skill
re_audit_of: "2026-05-05"
re_audit_reason: "ProgressBar-usage.md was created editorially (no Figma examples page exists). Re-score usage dimension; close GAP-009; partial-fix GAP-006."

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - ProgressBar-figma.md
  - ProgressBar-usage.md     # editorial — see WARN-003
  - figma-screenshot-ProgressBar.png

files_missing:
  - ProgressBar-pui.md  # intentionally absent — PUI MCP confirmed no Platform UI relevance

dimension_scores:
  props:        { score: 0.80, coverage: "8/10" }
  examples:     { score: 0.78, coverage: "7/9" }
  tokens:       { score: 0.40, coverage: "2/7 — tokens.md empty; data present in ProgressBar-figma.md" }
  accessibility:{ score: 0.78, coverage: "7/9" }
  figma:        { score: 0.83, coverage: "10/12" }
  usage:        { score: 0.65, coverage: "6/9 — editorial: 5 grounded Do/Don't pairs, When to use, When not to use; missing screenshots, Figma-source verification, and a failure-state Do/Don't (see GAP-USAGE-002 in ProgressBar-usage.md)" }
  pui:          { score: 1.00, coverage: "PASS — PUI MCP search confirmed no Platform UI relevance" }

available_dimensions_avg: 0.75
overall_avg: 0.75

counts:
  doc_gaps: 8
  source_gaps: 4    # was 5 — GAP-009 closed (resolved editorially)
  conflicts: 0
  warnings: 3       # was 2 — added WARN-003 (editorial usage)

verdict: YES
verdict_reason: >
  Zero CONFLICTs and zero blocker-severity gaps. The usage SOURCE_GAP (GAP-009)
  is closed editorially — ProgressBar-usage.md now exists with grounded Do/Don't
  pairs sourced from the extracted artifacts and the public Oxygen usage page.
  WARN-003 flags that the usage file is not Figma-sourced and should be replaced
  by figma-extract-usage output if a Figma examples page is created.
  doc-rewrite can proceed across all 7 dimensions. Pull token data from
  ProgressBar-figma.md §Color & token bindings to populate tokens.md as part
  of the rewrite.

gaps:
  - id: GAP-001
    dimension: tokens
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md
      location: "## Status"
      finding: >
        tokens.md contains only a SOURCE_GAP note with no token content. The full token set
        is documented in ProgressBar-figma.md §Color & token bindings:
        --ui/ui01 (track bg), --actions/action04 (loading fill), --success/success01
        (complete fill), --text/textcolor01 (label), --typography/body01 (label typography).
    fix_action: "Populate tokens.md with the five tokens documented in ProgressBar-figma.md §Color & token bindings, including light/dark mode values."
    blocks: [storybook-generate]
    dependency: []

  - id: GAP-002
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "### `size` named values table"
      finding: >
        The named size values 'small', 'default', 'large' are listed with only descriptive
        labels (Compact / Standard / Enlarged). The corresponding pixel dimensions (track
        height and/or container width) are not documented. These values are not present in
        either the OX MCP or the Figma component set, which has no size variant axis.
    fix_action: "Check @8x8/oxygen-loaders source or Storybook to determine pixel dimensions for small/default/large named sizes; add to props.md size table."
    blocks: []
    dependency: []

  - id: GAP-003
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "## Props table — mode axis absent"
      finding: >
        Figma exposes a 'mode' variant axis (light/dark) with no corresponding Oxygen prop.
        props.md does not explain this mapping. Consumers inspecting Figma will not know that
        light/dark theming is handled by a design-system ThemeProvider, not a component prop.
    fix_action: "Add a note to props.md (e.g. under a 'Theming' heading) stating that the Figma 'mode' variant corresponds to the ThemeProvider context — no component-level prop exists."
    blocks: []
    dependency: []

  - id: GAP-004
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "## Props table — value row"
      finding: >
        props.md documents 'value' as 0–100 but does not explain that value === 100
        triggers the 'complete' visual state (green fill, full-width). This mapping is
        visible in Figma as the 'status=complete' variant but not bridged in the Oxygen docs.
        Note: ProgressBar-usage.md Pair 5 documents the consumer-side text-swap rule but does
        not satisfy the props.md description gap.
    fix_action: "Extend the 'value' prop description: 'When value reaches 100 the complete state is rendered (green fill, full track coverage)'."
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "## Complete states"
      finding: >
        Figma defines separate 'loadingText' and 'completeText' text properties, while
        Oxygen has a single 'text' prop. No example demonstrates swapping text content
        as value transitions from loading to complete. Consumers may not know they must
        manage this themselves. Note: ProgressBar-usage.md Pair 5 documents the editorial
        rule; examples.md should add a code snippet that models it.
    fix_action: "Add an example to examples.md showing a controlled component that sets text='Loading...' when value < 100 and text='Complete' when value === 100."
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    status: partial
    evidence:
      source_file: "props.md / examples.md / tokens.md / accessibility.md"
      location: "'See also' nav line in each file"
      finding: >
        On 2026-05-14 each file's 'See also' nav was extended to include
        ProgressBar-usage.md — but ProgressBar-figma.md is still missing from the
        See also line in all four OX MCP files. The cross-link is still incomplete.
    fix_action: "Add '· [ProgressBar-figma.md](ProgressBar-figma.md)' to the See also line in props.md, examples.md, tokens.md, and accessibility.md."
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## WCAG 2.1 AA checklist — missing row"
      finding: >
        WCAG 1.4.11 (Non-text Contrast) is absent from the checklist. ProgressBar's track
        background and fill are non-text UI components; they must meet 3:1 contrast against
        adjacent colours. The token values in ProgressBar-figma.md (ui/ui01 #ebeae1,
        actions/action04 #0056e0, success/success01 #127440) should be evaluated against
        the expected page background.
    fix_action: "Add WCAG 1.4.11 row to accessibility.md checklist; compute contrast ratios for --ui/ui01, --actions/action04, --success/success01 against the standard page background token."
    blocks: []
    dependency: []

  - id: GAP-008
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "## Animated (controlled) — code snippet"
      finding: >
        The animated example references 'step' (in setProgress and the useEffect dependency
        array) but 'step' is never defined in the snippet. The example is a fragment from the
        Storybook simulator story and will not compile as shown.
    fix_action: "Add 'const step = 5;' (or a prop/state declaration) to the animated example in examples.md so it is a self-contained, runnable snippet."
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    status: resolved_editorially
    resolution_date: "2026-05-14"
    evidence:
      source_file: ProgressBar-usage.md
      location: "component-lib/ProgressBar/ProgressBar-usage.md"
      finding: >
        ProgressBar-usage.md was missing as of 2026-05-05. On 2026-05-14 an editorial
        usage file was written from the extracted artifacts (props.md, examples.md,
        accessibility.md, ProgressBar-figma.md) and the public Oxygen usage page
        (https://oxygen.8x8.com/components/progressbar/usage). 5 grounded Do/Don't pairs;
        When to use and When not to use sections present. Pairs are NOT Figma-sourced;
        no `↳ ProgressBar examples` page exists in Figma.
    fix_action: "When a Figma '↳ ProgressBar examples' page is created, run figma-extract-usage to replace the editorial pairs with Figma-sourced ones."
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ProgressBar-figma.md
      location: "## Gaps & conflicts — Incomplete data rows"
      finding: >
        figma_get_variables failed (requires Desktop Bridge or Figma enterprise API token).
        Token names were inferred from CSS custom property names in the design context output
        (--ui/ui01, --actions/action04 etc.). These names have not been verified against
        the actual Figma variable collection entries.
    fix_action: "Run figma_get_variables with resolveAliases=true (requires Desktop Bridge or enterprise token) to verify token names against the Figma UI-Foundations library (iVY5nI8JAxM05Apnnvozzs)."
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ProgressBar-figma.md
      location: "## API — Component properties — missing component key"
      finding: "figma_get_component_details failed (Desktop Bridge required). The Figma component key for the Bar component set was not retrieved."
    fix_action: "Run figma_get_component_details with componentName='Progress bar' when Desktop Bridge is available; record the component key in ProgressBar-figma.md for downstream Code Connect use."
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ProgressBar-figma.md
      location: "## Structure & spacing — Gap and track height rows"
      finding: >
        The 8px gap between bar and text label, and the 8px bar track height, both have
        no token binding in Figma (confirmed by design context output). These are hardcoded
        values. Whether they should be tokenised is a design decision not yet made.
    fix_action: "Flag to design: should bar-track height (8px) and bar-to-label gap (8px) be spacing tokens? Confirm intent; update ProgressBar-figma.md once decided."
    blocks: []
    dependency: []

  - id: GAP-013
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ProgressBar-figma.md
      location: "## Accessibility (from Figma annotations only)"
      finding: "No accessibility annotations are present in the Figma component. Desktop Bridge unavailable; ARIA role, focus order, and keyboard interaction fields are all NOT ANNOTATED."
    fix_action: "Add ARIA role annotation to the Bar component in Figma; re-run figma-extract when Desktop Bridge is available."
    blocks: []
    dependency: []

  - id: GAP-USAGE-002
    dimension: usage
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ProgressBar-usage.md
      location: "## Gaps & open questions"
      finding: >
        No editorial guidance currently exists for how to surface a failure state.
        The Figma component set models only `loading` and `complete` — failure is undefined.
    fix_action: "Confirm with design whether failure should be communicated via the existing bar (text-only swap) or by switching to a different component (Toast / AlertBanner). Add a 6th Do/Don't pair to ProgressBar-usage.md once decided."
    blocks: []
    dependency: []

  - id: GAP-USAGE-003
    dimension: usage
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: ProgressBar-usage.md
      location: "## Gaps & open questions"
      finding: >
        Forward-only progress is documented prose-only on oxygen.8x8.com. The Oxygen API
        does not enforce it (value can be decremented). A Do/Don't pair could harden this
        rule editorially.
    fix_action: "Optionally add a Do/Don't pair: ✅ Do — drive `value` forward only; ❌ Don't — decrement or reset the bar mid-flow. Decision: pending designer review of the editorial file."
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: accessibility
    confidence: heuristic
    note: >
      The ARIA role (role="progressbar") and aria-valuenow/min/max attributes in
      accessibility.md are documented as expected behaviour based on component type and
      examples, not verified against the rendered DOM of @8x8/oxygen-loaders. The actual
      implementation may render these differently. Verify against the Storybook / rendered
      output before shipping docs.

  - id: WARN-002
    dimension: props
    confidence: heuristic
    note: >
      The 'size' prop default is documented as '240px' (from get-component-info). The named
      values 'small', 'default', 'large' (from Storybook examples) suggest '240px' is either
      the default for numeric/string usage only, or is the resolved pixel value of 'default'.
      Verify whether size='default' and size='240px' are equivalent; update props.md if
      the default should be 'default' (the named value) rather than '240px' (a raw dimension).

  - id: WARN-003
    dimension: usage
    confidence: heuristic
    note: >
      ProgressBar-usage.md was authored editorially on 2026-05-14 from the extracted
      artifacts and the public Oxygen usage page — NOT from a Figma `↳ ProgressBar examples`
      page. The 5 Do/Don't pairs are explicitly grounded in cited file/line locations but
      should be reviewed by a designer. Replace with `figma-extract-usage` output when a
      Figma examples page is created. The file's frontmatter carries `source_type: editorial`
      and a visible callout to flag this status to downstream consumers.

# --- navigation (added by component-map) ---
role: audit
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES — doc-rewrite can run on all 7 dimensions; usage is editorial (WARN-003)."
siblings:
  - "[[ProgressBar/props]]"
  - "[[ProgressBar/examples]]"
  - "[[ProgressBar/tokens]]"
  - "[[ProgressBar/accessibility]]"
  - "[[ProgressBar/ProgressBar-figma]]"
  - "[[ProgressBar/ProgressBar-usage]]"
tags:
  - oxygen
  - component/ProgressBar
  - role/audit
  - stage/spec_ready
---

# ProgressBar — Documentation Audit

> **Verdict: YES** — doc-rewrite can proceed on **all 7 dimensions**.
> Usage dimension lifted 0.00 → 0.65 by editorial authoring of ProgressBar-usage.md.
> WARN-003 flags the editorial source; replace with figma-extract-usage output when a Figma examples page is created.
>
> Rubric version: 1.0 · Re-audited: 2026-05-14 (prior audit: 2026-05-05)

---

## File Inventory

| File | Status | Produced by |
|------|--------|-------------|
| `props.md` | ✅ Present | oxygen-mcp-extract |
| `examples.md` | ✅ Present | oxygen-mcp-extract |
| `tokens.md` | ✅ Present (empty — SOURCE_GAP content) | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | oxygen-mcp-extract |
| `ProgressBar-figma.md` | ✅ Present | figma-extract |
| `figma-screenshot-ProgressBar.png` | ✅ Present | figma-extract |
| `ProgressBar-usage.md` | ✅ Present (**editorial** — WARN-003) | editorial (not figma-extract-usage) |
| `ProgressBar-pui.md` | ✅ N/A — PUI MCP confirmed no relevance | pui-mcp-extract |

---

## Dimension Scores

| Dimension | Score | Δ | Coverage | Notes |
|-----------|-------|---|----------|-------|
| Props | 0.80 | — | 8/10 | ✅ Available — minor gaps on size pixel dims and Figma mapping docs |
| Examples | 0.78 | — | 7/9 | ✅ Available — animated example has undefined `step` |
| Tokens | 0.40 | — | 2/7 | ⚠️ tokens.md empty; token data **present in ProgressBar-figma.md** — auto-fixable |
| Accessibility | 0.78 | — | 7/9 | ✅ Available — WCAG 1.4.11 missing; contrast ratios need computing |
| Figma | 0.83 | — | 10/12 | ✅ Available — Desktop Bridge gaps (variables, key, annotations) |
| Usage | 0.65 | **+0.65** | 6/9 | ✅ Available — editorial; 5 grounded Do/Don't pairs, When-to-use, When-not-to-use; missing screenshots and Figma-source verification (WARN-003) |
| PUI | 1.00 | — | PASS | ✅ Confirmed — no Platform UI concerns |
| **Available avg** | **0.75** | +0.02 (now all 7) | | All 7 dimensions available |
| **Overall avg** | **0.75** | **+0.09** | | Usage no longer drags overall avg to zero |

---

## Conflict reclassification (unchanged from 2026-05-05)

Three items in `ProgressBar-figma.md §Gaps & conflicts` were pre-labelled "Conflict".
All three remain reclassified as **auto-fixable DOC_GAPs** — they document well-understood
design-to-implementation mappings; no human decision is required between competing options:

| Was labelled | Reclassified as | Reason |
|---|---|---|
| Figma `mode` → no Oxygen prop | **GAP-003** DOC_GAP | ThemeProvider handles theming; document the mapping |
| Figma `status` → `value` | **GAP-004** DOC_GAP | `value === 100` → complete; document the rule |
| Figma `loadingText`/`completeText` → `text` | **GAP-005** DOC_GAP | Single prop; consumer manages text; add example |

---

## Gap Summary

| Count | Category | Δ |
|-------|----------|---|
| 0 | CONFLICTs — **no blocks on doc-rewrite** | — |
| 4 | SOURCE_GAPs (4 minor — usage SOURCE_GAP closed editorially) | **−1** (GAP-009 closed) |
| 8 | DOC_GAPs (1 major, 7 minor — 5 auto-fixable; +GAP-USAGE-003 new minor heuristic) | net same |
| 3 | Warnings (heuristic, advisory) | **+1** (WARN-003) |

---

## Status changes since 2026-05-05

- **GAP-009 (Usage SOURCE_GAP)** → `status: resolved_editorially` on 2026-05-14. Editorial
  ProgressBar-usage.md created with 5 grounded Do/Don't pairs. No Figma examples page
  exists, so the underlying SOURCE_GAP (Figma extraction path) is technically still open —
  but the file gap is closed and the audit reflects that.
- **GAP-006 (Cross-links incomplete)** → `status: partial`. ProgressBar-usage.md is now
  linked from props.md / examples.md / tokens.md / accessibility.md / ProgressBar-figma.md.
  ProgressBar-figma.md is still NOT linked from props/examples/tokens/accessibility — the
  original GAP-006 fix is still pending.
- **New gap: GAP-USAGE-002** — failure-state guidance missing from ProgressBar-usage.md
  (carried over from the file's own Gaps section).
- **New gap: GAP-USAGE-003** — forward-only progress rule could be hardened as a Do/Don't pair.
- **New warning: WARN-003** — usage file is editorial, not Figma-sourced.

---

## Gaps

### DOC_GAP — Major (auto-fixable)

**GAP-001** · Tokens
> `tokens.md` is empty — MCP returned no token data. Token names and light/dark values are
> fully documented in `ProgressBar-figma.md §Color & token bindings`.
> **Fix:** doc-rewrite should pull: `--ui/ui01`, `--actions/action04`, `--success/success01`,
> `--text/textcolor01`, `--typography/body01`.

### DOC_GAP — Minor (auto-fixable)

**GAP-003** · Props · Theme mapping note missing
**GAP-004** · Props · `value === 100` completion rule not in description
**GAP-005** · Examples · No text-swap example modelling Loading→Complete
**GAP-006** · Cross-links — **partial fix 2026-05-14** (usage link added; figma link still missing)
**GAP-007** · Accessibility · WCAG 1.4.11 row missing
**GAP-008** · Examples · Animated example references undefined `step`

### DOC_GAP — Minor (requires external verification)

**GAP-002** · Props · Named size pixel dimensions
**GAP-USAGE-003** · Usage · Optional Do/Don't on forward-only progress

### SOURCE_GAP — Minor

**GAP-010** · Figma · Token names from CSS vars only
**GAP-011** · Figma · Component key not retrieved
**GAP-012** · Figma · 8px gap / 8px track-height untokenised
**GAP-013** · Accessibility · No Figma a11y annotations
**GAP-USAGE-002** · Usage · Failure-state guidance undefined

### SOURCE_GAP — Closed

**GAP-009** · Usage · ✅ Resolved editorially 2026-05-14 (see WARN-003)

---

## Warnings

**WARN-001 (Accessibility):** `role="progressbar"` and `aria-value*` attributes are
inferred from component type, not verified against the rendered DOM of `@8x8/oxygen-loaders`.
Verify before shipping.

**WARN-002 (Props):** `size` default `'240px'` may be the resolved pixel value of the
`'default'` named size rather than a standalone default. Verify and update if needed.

**WARN-003 (Usage):** ProgressBar-usage.md is editorial — authored from extracted artifacts
and the public oxygen.8x8.com page, not from a Figma examples page. 5 Do/Don't pairs are
explicitly grounded with file/line citations. Replace with `figma-extract-usage` output if
and when a `↳ ProgressBar examples` Figma page is created.

---

## Suggested next actions

```
1. Finish GAP-006: add ProgressBar-figma.md to See also in props/examples/tokens/accessibility  → 2-min auto-fix
2. Fix GAP-008 (animated example step undefined)                                                → 2-min auto-fix
3. Run doc-rewrite                                                                              → produces ProgressBar-spec.md
   (doc-rewrite should auto-fix GAP-001, 003, 004, 005, 007 as part of the rewrite)
4. Designer review of editorial Do/Don't pairs in ProgressBar-usage.md (WARN-003, GAP-USAGE-002, GAP-USAGE-003)
5. Verify ARIA roles                                                                            → WARN-001
6. Check size px dimensions                                                                     → GAP-002
7. Verify size default value                                                                    → WARN-002
8. Create Figma `↳ ProgressBar examples` page → run figma-extract-usage to replace editorial Do/Don'ts
```

_Source: doc-audit skill v1.0 · Re-audited from component-lib/ProgressBar/ · 2026-05-14 (prior audit: 2026-05-05)_
