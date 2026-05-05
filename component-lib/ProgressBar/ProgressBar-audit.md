---
rubric_version: "1.0"
component: ProgressBar
package: "@8x8/oxygen-loaders"
audit_date: "2026-05-05"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - ProgressBar-figma.md
  - figma-screenshot-ProgressBar.png

files_missing:
  - ProgressBar-usage.md
  - ProgressBar-pui.md  # intentionally absent — PUI MCP confirmed no Platform UI relevance

dimension_scores:
  props:        { score: 0.80, coverage: "8/10" }
  examples:     { score: 0.78, coverage: "7/9" }
  tokens:       { score: 0.40, coverage: "2/7 — tokens.md empty; data present in ProgressBar-figma.md" }
  accessibility:{ score: 0.78, coverage: "7/9" }
  figma:        { score: 0.83, coverage: "10/12" }
  usage:        { score: 0.00, coverage: "0/0 — SOURCE_GAP (major) — file missing" }
  pui:          { score: 1.00, coverage: "PASS — PUI MCP search confirmed no Platform UI relevance" }

available_dimensions_avg: 0.77
overall_avg: 0.66

counts:
  doc_gaps: 8
  source_gaps: 5
  conflicts: 0
  warnings: 2

verdict: YES
verdict_reason: >
  Zero CONFLICTs and zero blocker-severity gaps.
  The three items pre-labelled "Conflict" in ProgressBar-figma.md §Gaps & conflicts are
  reclassified here as DOC_GAPs: mode→ThemeProvider, status→value mapping, and
  loadingText/completeText→single text prop are all well-understood design-to-implementation
  mappings with clear resolution paths — no human choice is required between competing options.
  The major SOURCE_GAP (usage.md missing — Desktop Bridge required) blocks only the usage
  dimension of doc-rewrite; all other six dimensions are available.
  doc-rewrite can proceed. Pull token data from ProgressBar-figma.md §Color & token bindings
  to populate tokens.md as part of the rewrite.

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
        manage this themselves.
    fix_action: "Add an example to examples.md showing a controlled component that sets text='Loading...' when value < 100 and text='Complete' when value === 100."
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: "props.md / examples.md / tokens.md / accessibility.md"
      location: "'See also' nav line in each file"
      finding: >
        All four OX MCP-extracted files reference only the three sibling .md files in their
        'See also' nav line. None link to 'ProgressBar-figma.md', which exists in the folder.
        All four cross-links are incomplete.
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
    evidence:
      source_file: ~
      location: "component-lib/ProgressBar/ directory"
      finding: "ProgressBar-usage.md is absent. figma-extract-usage requires the Figma Desktop Bridge plugin (WebSocket on localhost:9228), which was not running during extraction."
    fix_action: "Open Figma Desktop → Plugins → Development → Figma Desktop Bridge, then run figma-extract-usage for ProgressBar."
    blocks: [doc-rewrite/usage-dimension]
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
---

# ProgressBar — Documentation Audit

> **Verdict: YES** — doc-rewrite can proceed on 6 of 7 dimensions.
> Usage dimension blocked pending Desktop Bridge for figma-extract-usage.
>
> Rubric version: 1.0 · Audited: 2026-05-05

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
| `ProgressBar-usage.md` | ❌ **MISSING** | figma-extract-usage |
| `ProgressBar-pui.md` | ✅ N/A — PUI MCP confirmed no relevance | pui-mcp-extract |

---

## Dimension Scores

| Dimension | Score | Coverage | Notes |
|-----------|-------|----------|-------|
| Props | 0.80 | 8/10 | ✅ Available — minor gaps on size pixel dims and Figma mapping docs |
| Examples | 0.78 | 7/9 | ✅ Available — animated example has undefined `step` |
| Tokens | 0.40 | 2/7 | ⚠️ tokens.md empty; token data **present in ProgressBar-figma.md** — auto-fixable |
| Accessibility | 0.78 | 7/9 | ✅ Available — WCAG 1.4.11 missing; contrast ratios need computing |
| Figma | 0.83 | 10/12 | ✅ Available — Desktop Bridge gaps (variables, key, annotations) |
| Usage | 0.00 | — | ❌ SOURCE_GAP (major) — Desktop Bridge required |
| PUI | 1.00 | PASS | ✅ Confirmed — no Platform UI concerns |
| **Available avg** | **0.77** | | 6 of 7 dimensions available |
| **Overall avg** | **0.66** | | Dragged by usage=0 |

---

## Conflict reclassification

Three items in `ProgressBar-figma.md §Gaps & conflicts` were pre-labelled "Conflict".
All three are reclassified as **auto-fixable DOC_GAPs** — they document well-understood
design-to-implementation mappings; no human decision is required between competing options:

| Was labelled | Reclassified as | Reason |
|---|---|---|
| Figma `mode` → no Oxygen prop | **GAP-003** DOC_GAP | ThemeProvider handles theming; document the mapping |
| Figma `status` → `value` | **GAP-004** DOC_GAP | `value === 100` → complete; document the rule |
| Figma `loadingText`/`completeText` → `text` | **GAP-005** DOC_GAP | Single prop; consumer manages text; add example |

---

## Gap Summary

| Count | Category |
|-------|----------|
| 0 | CONFLICTs — **no blocks on doc-rewrite** |
| 5 | SOURCE_GAPs (1 major, 4 minor) |
| 8 | DOC_GAPs (1 major, 7 minor — 5 auto-fixable) |
| 2 | Warnings (heuristic, advisory) |

---

## Gaps

### DOC_GAP — Major (auto-fixable)

**GAP-001** · Tokens
> `tokens.md` is empty — MCP returned no token data. Token names and light/dark values are
> fully documented in `ProgressBar-figma.md §Color & token bindings`.
> **Fix:** doc-rewrite should pull: `--ui/ui01`, `--actions/action04`, `--success/success01`,
> `--text/textcolor01`, `--typography/body01`.

### SOURCE_GAP — Major

**GAP-009** · Usage
> `ProgressBar-usage.md` absent — Figma Desktop Bridge was not running.
> **Fix:** Open Figma Desktop → Plugins → Development → Figma Desktop Bridge, then run `figma-extract-usage`.

### DOC_GAP — Minor (auto-fixable)

**GAP-003** · Props
> No documentation of `mode` → ThemeProvider mapping.
> **Fix:** Add theming note to `props.md`.

**GAP-004** · Props
> `value` description does not state that `value === 100` triggers the complete visual state.
> **Fix:** Extend `value` description in `props.md`.

**GAP-005** · Examples
> No example showing text swap pattern (`Loading...` → `Complete`) as value progresses.
> **Fix:** Add controlled example to `examples.md`.

**GAP-006** · All OX files
> `See also` nav missing `ProgressBar-figma.md` link in all four OX files.
> **Fix:** Add `· [ProgressBar-figma.md](ProgressBar-figma.md)` to each file's nav line.

**GAP-007** · Accessibility
> WCAG 1.4.11 (Non-text Contrast) missing from checklist.
> **Fix:** Add row; compute contrast for `--ui/ui01`, `--actions/action04`, `--success/success01`.

**GAP-008** · Examples
> Animated example references undefined `step` variable.
> **Fix:** Add `const step = 5;` to make snippet self-contained.

### DOC_GAP — Minor (requires external verification)

**GAP-002** · Props
> Named size values (`small`, `default`, `large`) have no pixel dimensions documented.
> **Fix:** Check `@8x8/oxygen-loaders` source or Storybook for actual px values.

### SOURCE_GAP — Minor

**GAP-010** · Figma
> Token names from CSS vars only — not verified against Figma variable collection.
> **Fix:** Run `figma_get_variables` with Desktop Bridge or enterprise token.

**GAP-011** · Figma
> Figma component key not retrieved (`figma_get_component_details` requires Desktop Bridge).
> **Fix:** Retrieve when Desktop Bridge available.

**GAP-012** · Figma
> `8px` bar track height and `8px` bar-to-label gap have no token bindings.
> **Fix:** Design decision needed — flag to designer.

**GAP-013** · Accessibility
> No accessibility annotations in Figma — all a11y docs are inferred from component type.
> **Fix:** Add ARIA role annotation to Bar component in Figma.

---

## Warnings

**WARN-001 (Accessibility):** `role="progressbar"` and `aria-value*` attributes are
inferred from component type, not verified against the rendered DOM of `@8x8/oxygen-loaders`.
Verify before shipping.

**WARN-002 (Props):** `size` default `'240px'` may be the resolved pixel value of the
`'default'` named size rather than a standalone default. Verify and update if needed.

---

## Suggested next actions

```
1. Fix GAP-006 (broken cross-links) → 5-min auto-fix before rewrite
2. Fix GAP-008 (animated example step undefined) → 2-min auto-fix
3. Run doc-rewrite             → produces ProgressBar-spec.md
   (doc-rewrite should auto-fix GAP-001, 003, 004, 005, 007 as part of the rewrite)
2. Run figma-extract-usage     → GAP-009 (requires Desktop Bridge)
3. Verify ARIA roles           → WARN-001
4. Check size px dimensions    → GAP-002
5. Verify size default value   → WARN-002
```

_Source: doc-audit skill v1.0 · Audited from component-lib/ProgressBar/ · 2026-05-05_
