---
rubric_version: "1.0"
component: Tabs
audit_date: "2026-04-30"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - Tabs-figma.md
  - Tabs-pui.md

files_missing:
  - Tabs-usage.md

dimension_scores:
  props:        { score: 0.80, coverage: "8/10" }
  examples:     { score: 0.67, coverage: "6/9"  }
  tokens:       { score: 0.50, coverage: "4/8"  }
  accessibility:{ score: 0.78, coverage: "7/9"  }
  figma:        { score: 0.67, coverage: "8/12" }
  usage:        { score: 0.00, coverage: "0/0 — SOURCE_GAP" }
  pui:          { score: 1.00, coverage: "PASS — NO RELEVANT PUI CONTEXT confirmed by engineer" }

available_dimensions_avg: 0.74
overall_avg: 0.63

counts:
  doc_gaps: 9
  source_gaps: 3
  conflicts: 0
  warnings: 3

verdict: YES
verdict_reason: >
  Zero CONFLICTs and zero blocker-severity gaps — doc-rewrite can proceed.
  The missing Tabs-usage.md (SOURCE_GAP, major) means the usage dimension will be
  skipped or left sparse in the spec; all other dimensions have sufficient data.
  Major token gaps (unresolved semantic names, missing typography) will produce
  incomplete token tables but do not block the rewrite.

suggested_next_action: >
  1. Run doc-rewrite → produces Tabs-spec.md (usage dimension will be sparse)
  2. Run figma-extract-usage → produces Tabs-usage.md, then re-run doc-audit
  3. Investigate Figma variable library to resolve token IDs (20136:253 etc.)
     to semantic names (border03, interactive01) — fixes GAP-001
  4. Fix broken "See also" cross-links in all 4 OX files → figma.md → Tabs-figma.md

gaps:
  - id: GAP-001
    dimension: tokens
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Color variables observed in Figma variants — Variable ID column"
      finding: >
        Border color variable IDs (20136:253, 20136:265, 20136:286, 20136:324) were
        captured from Figma but their semantic token names (e.g. border03, interactive01)
        are unresolved. The file documents hex values but not the token names that
        doc-rewrite and Storybook controls need.
    fix_action: "Access the Figma variable library for file 5YihJ5WuDvnvrlrRMC4sBp and resolve each variable ID to its semantic token name; update tokens.md"
    blocks: [doc-rewrite/tokens-dimension, storybook-generate]
    dependency: []

  - id: GAP-002
    dimension: tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "Entire file"
      finding: >
        Typography tokens not captured: no font size, font weight, line height, or
        letter spacing for the tab label text. The Figma screenshot shows the selected
        tab label renders bold compared to unselected, but no text style token is
        documented anywhere in the extracted files.
    fix_action: "Inspect the tab label TEXT node inside the selected variant (85651:78786) for text style name and font properties; add to tokens.md"
    blocks: [doc-rewrite/tokens-dimension]
    dependency: []

  - id: GAP-003
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ~
      location: "component-lib/Tabs/ directory"
      finding: "Tabs-usage.md is absent — figma-extract-usage skill has not been run"
    fix_action: "Run figma-extract-usage for Tabs to produce Tabs-usage.md with Do/Don't guidelines"
    blocks: [doc-rewrite/usage-dimension]
    dependency: []

  - id: GAP-004
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Tabs-figma.md
      location: "## Visual snapshots — all three image references"
      finding: >
        Tabs-figma.md references three screenshot files (figma-tabs-variants.png,
        figma-tabs-disclosure.png, figma-tabs-popover-atom.png) that are not present
        in the component-lib/Tabs/ directory. Screenshots were captured during
        extraction but not saved to disk.
    fix_action: "Re-run figma_take_screenshot for nodes 85651:78740, 85651:78793, 86754:680 and save PNGs to component-lib/Tabs/"
    blocks: [docusaurus-generate]
    dependency: []

  - id: GAP-005
    dimension: figma
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: Tabs-figma.md
      location: "## Components on the Tabs page / tabs — COMPONENT_SET / Variants"
      finding: >
        The Figma screenshot shows the selected tab label renders in bold (heavier font
        weight) compared to unselected tabs. This typographic state change is visible
        but not documented in the variant table or design properties — no text style,
        font-weight token, or typography note exists for the selected state.
    fix_action: "Inspect the text node inside variant 85651:78786 (state=rest, isSelected=true) for font weight / text style; document in Tabs-figma.md variant table"
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: figma
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: Tabs-figma.md
      location: "## Components on the Tabs page / tabs — Design properties / selectIcon row"
      finding: >
        The selectIcon property default is documented as 'chevron icon' but the actual
        Figma default is an INSTANCE_SWAP pointing to node 85016:131. The icon name
        is not identified — downstream tooling cannot reference it by name.
    fix_action: "Query figma_get_component for node 85016:131 to retrieve the icon name; update selectIcon default value in Tabs-figma.md"
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## <Tab> (named export) — isStretched row, Description column"
      finding: >
        The isStretched description 'Stretches tab to fill available space in <Tabs>'
        is inferred. The Oxygen MCP source returned an eslint-disable comment as the
        description instead of a real doc string. The inferred description is plausible
        but unverified.
    fix_action: "Verify isStretched behaviour by checking @8x8/oxygen-tabs source or Storybook; update description if incorrect"
    blocks: []
    dependency: []

  - id: GAP-008
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## <Tabs> and ## <Tab> — color prop, Default column"
      finding: >
        The color prop default value is undocumented for both <Tabs> and <Tab>.
        The MCP did not return a default value. It is unclear whether the component
        defaults to 'light', inherits from context, or requires explicit specification.
    fix_action: "Check @8x8/oxygen-tabs source for the color prop default; document in props.md"
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## Keyboard interactions — table"
      finding: >
        Arrow key (Left/Right) navigation within the tablist is not documented.
        WAI-ARIA Authoring Practices for the tablist pattern require Left/Right arrows
        to move focus between tabs without activating them, and optionally Home/End
        for first/last tab. The Figma spec documented only Tab/Shift+Tab/Enter/Escape.
        If the component implements WAI-ARIA tablist, arrow key behaviour must be
        documented.
    fix_action: "Confirm whether the Oxygen Tabs component implements arrow key navigation; add Left/Right (and optionally Home/End) rows to the keyboard interactions table"
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "## WCAG 2.1 Level AA compliance — Criteria met table"
      finding: >
        WCAG 1.4.1 (Use of Color) is not addressed. The selected tab state is
        communicated via a blue bottom border — if this is the sole differentiator
        from unselected tabs (no shape, icon, or text weight change confirmed), the
        component may rely on color alone to convey state, which fails 1.4.1.
        The selected tab does show bold text in the screenshot, but this is not
        confirmed in the spec as an intentional non-color indicator.
    fix_action: "Confirm whether bold font weight on selected tab is intentional; add WCAG 1.4.1 row to the checklist noting the combined indicator (underline + font weight) or flagging a gap if color is the sole differentiator"
    blocks: []
    dependency: [GAP-005]

  - id: GAP-011
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "> See also: line 3"
      finding: >
        The 'See also' cross-navigation links in props.md, examples.md, tokens.md,
        and accessibility.md all reference 'figma.md' — but the actual file in
        component-lib/Tabs/ is named 'Tabs-figma.md'. All four internal links are broken.
    fix_action: "Update 'See also' links in props.md, examples.md, tokens.md, and accessibility.md to reference Tabs-figma.md instead of figma.md"
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "## Basic usage — note block"
      finding: >
        No MCP-sourced code examples exist for this component (Oxygen MCP returned 0
        clean examples). All code snippets were constructed from prop definitions and
        usage description. There are no examples for the icon, badge, or hasDropdown
        props — only prose guidance is provided.
    fix_action: "Source real usage examples from the @8x8/oxygen-tabs Storybook or source repository; replace constructed snippets with authoritative code"
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: props
    confidence: heuristic
    note: >
      forwardedRef is listed as required by the OX MCP but has a null default value.
      For a ref-forwarding prop this is unusual — required with a null default implies
      the component will accept a null ref gracefully, but the API is ambiguous.
      Downstream type generation may emit a non-optional ref parameter.

  - id: WARN-002
    dimension: accessibility
    confidence: heuristic
    note: >
      ARIA roles in accessibility.md are explicitly labelled 'inferred from component
      nature' and 'recommended'. The actual Oxygen implementation may render as plain
      div/button elements without role="tablist" / role="tab" / aria-selected. If
      semantic HTML is absent, assistive technology will not announce the tablist
      pattern correctly. Verify against the rendered DOM before shipping docs.

  - id: WARN-003
    dimension: figma
    confidence: heuristic
    note: >
      The tabsDisclosure states list includes 'active' (press state) inherited from
      Icon Button, but the tabs COMPONENT_SET only exposes 'rest' and 'hover' as
      named variant axes. The active/press state for an individual tab is handled
      implicitly via click → isSelected=true transition. If a visible press-state
      visual exists it is not captured.
---

# Tabs — Documentation Audit

> **Rubric version:** 1.0 · **Audit date:** 2026-04-30 · **Verdict:** YES

---

## File Inventory

| File | Status | Produced by |
|------|--------|-------------|
| `props.md` | ✅ Present | oxygen-mcp-extract |
| `examples.md` | ✅ Present | oxygen-mcp-extract |
| `tokens.md` | ✅ Present | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | oxygen-mcp-extract |
| `Tabs-figma.md` | ✅ Present | figma-extract |
| `Tabs-usage.md` | ❌ **MISSING** | figma-extract-usage |
| `Tabs-pui.md` | ✅ Present — `NO RELEVANT PUI CONTEXT` | pui-mcp-extract |

---

## Dimension Scores

| Dimension | Score | Coverage | Status |
|-----------|-------|----------|--------|
| Props | 0.80 | 8/10 | ✅ Available |
| Examples | 0.67 | 6/9 | ✅ Available |
| Tokens | 0.50 | 4/8 | ✅ Available — ⚠️ major gaps |
| Accessibility | 0.78 | 7/9 | ✅ Available |
| Figma | 0.67 | 8/12 | ✅ Available |
| Usage | 0.00 | — | ❌ SOURCE_GAP (major) |
| PUI | 1.00 | PASS | ✅ Resolved — no relevant context |
| **Available avg** | **0.74** | | |
| **Overall avg** | **0.63** | | |

---

## Gap Summary

| Count | Category |
|-------|----------|
| 0 | CONFLICTs — **no blocks on doc-rewrite** |
| 3 | SOURCE_GAPs (2 major, 1 minor) |
| 9 | DOC_GAPs (all minor) |
| 3 | Warnings (heuristic, advisory) |

---

## Gaps

### SOURCE_GAPs

#### GAP-003 · Usage · MAJOR
**Finding:** `Tabs-usage.md` absent — `figma-extract-usage` has not been run.
**Fix:** Run `figma-extract-usage` for Tabs to produce Do/Don't guidelines.

#### GAP-002 · Tokens · MAJOR
**Finding:** Typography tokens not captured — font size, weight, line height for tab label are absent. The selected tab renders bold in the Figma screenshot but no text style token is documented.
**Fix:** Inspect TEXT node inside selected variant `85651:78786` for font properties; add to `tokens.md`.

#### GAP-004 · Figma · MINOR
**Finding:** Three screenshot PNGs referenced in `Tabs-figma.md` (`figma-tabs-variants.png`, `figma-tabs-disclosure.png`, `figma-tabs-popover-atom.png`) are not present in the directory.
**Fix:** Re-capture and save PNGs from Figma nodes `85651:78740`, `85651:78793`, `86754:680`.

---

### DOC_GAPs

#### GAP-001 · Tokens · MAJOR · not auto-fixable
Figma variable IDs (`20136:253`, `20136:265`, `20136:286`, `20136:324`) captured but semantic token names unresolved. Hex values documented but token names needed by doc-rewrite and Storybook.
→ **Fix:** Resolve variable IDs via Figma variable library; update `tokens.md`.

#### GAP-005 · Figma · MINOR · not auto-fixable
Selected tab renders bold in screenshot but no font weight / text style token is documented in variant table.
→ **Fix:** Inspect text node in `85651:78786`; add typography note to `Tabs-figma.md`.

#### GAP-006 · Figma · MINOR · auto-fixable
`selectIcon` default icon is node `85016:131` — name not identified. Documented only as "chevron icon".
→ **Fix:** Query `figma_get_component` for `85016:131`; update `Tabs-figma.md`.

#### GAP-007 · Props · MINOR · requires verification
`isStretched` description is inferred (MCP returned an eslint-disable comment instead of a real description).
→ **Fix:** Verify from `@8x8/oxygen-tabs` source or Storybook.

#### GAP-008 · Props · MINOR · not auto-fixable
`color` prop default value undocumented for both `<Tabs>` and `<Tab>`.
→ **Fix:** Check package source for default; add to `props.md`.

#### GAP-009 · Accessibility · MINOR · auto-fixable (pending verification)
Arrow key (Left/Right) navigation not documented. WAI-ARIA tablist pattern requires arrow keys to move focus between tabs.
→ **Fix:** Confirm whether OX Tabs implements arrow key navigation; add rows to keyboard interaction table.

#### GAP-010 · Accessibility · MINOR · auto-fixable (depends GAP-005)
WCAG 1.4.1 (Use of Color) not addressed. If bold font weight on selected tab is confirmed as intentional, the component passes (color + weight = two indicators). If not, it may fail.
→ **Fix:** Confirm bold-text intent (GAP-005); add WCAG 1.4.1 row to checklist.

#### GAP-011 · All OX files · MINOR · auto-fixable
"See also" cross-links in `props.md`, `examples.md`, `tokens.md`, `accessibility.md` reference `figma.md` — actual filename is `Tabs-figma.md`. All four links are broken.
→ **Fix:** Replace `figma.md` → `Tabs-figma.md` in the "See also" line of all four files.

#### GAP-012 · Examples · MINOR · not auto-fixable
No MCP-sourced code examples exist (OX MCP returned 0 clean snippets). All code was constructed from prop definitions. No examples for `icon`, `badge`, or `hasDropdown` props.
→ **Fix:** Source real examples from `@8x8/oxygen-tabs` Storybook or source repo.

---

## Warnings

**WARN-001 (Props):** `forwardedRef` is listed as required with a null default — ambiguous API signal. Type generation may emit a non-optional ref parameter.

**WARN-002 (Accessibility):** ARIA roles are explicitly marked "inferred" in `accessibility.md`. Verify against rendered DOM — if the implementation doesn't use `role="tablist"` / `role="tab"` / `aria-selected`, the recommended enhancements become requirements, not nice-to-haves.

**WARN-003 (Figma):** `tabsDisclosure` inherits an `active` press state from Icon Button, but the individual tab component set exposes only `rest` and `hover` variant axes. Press-state visual (if any) is undocumented.

---

## Verdict: YES — ready for doc-rewrite

No CONFLICTs, no blocker-severity gaps. `doc-rewrite` can proceed.

Recommended order:

```
1. Fix GAP-011 (broken cross-links) → 5-min auto-fix before rewrite
2. Run doc-rewrite          → produces Tabs-spec.md
                               (usage dimension sparse — acceptable)
3. Save screenshots         → GAP-004
4. Run figma-extract-usage  → GAP-003 → re-run doc-audit if needed
5. Resolve token names      → GAP-001 (Figma variable library access needed)
6. Verify ARIA roles        → WARN-002 → update accessibility.md
7. Confirm arrow keys       → GAP-009
8. Confirm bold-text intent → GAP-005 + GAP-010 (unblocks WCAG 1.4.1 check)
```

_Source: doc-audit skill · Rubric v1.0 · 2026-04-30_
