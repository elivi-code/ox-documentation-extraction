---
# ============================================================
# Badge — Documentation Audit
# ============================================================
component: Badge
rubric_version: "1.0"
audited: 2026-05-12
verdict: "PARTIAL"
verdict_reason: "Blocker SOURCE_GAP — badge-figma.md absent (figma-extract not run). Zero CONFLICTs. Rewrite can proceed on props, examples, accessibility, and usage_patterns dimensions."

files_present:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - badge-usage.md
  - badge-pui.md

files_missing:
  - file: badge-figma.md
    produced_by: figma-extract
    severity: blocker

scores:
  anatomy:          { coverage: "3/8",  score: 0.38 }
  api_props:        { coverage: "6/7",  score: 0.86 }
  color_tokens:     { coverage: "5/9",  score: 0.56 }
  structure_spacing: { coverage: "5/9",  score: 0.56 }
  examples:         { coverage: "4/5",  score: 0.80 }
  accessibility:    { coverage: "5/6",  score: 0.83 }
  usage_patterns:   { coverage: "3/5",  score: 0.60 }
  overall:          0.66

counts:
  doc_gaps: 1
  source_gaps: 8
  conflicts: 0
  warnings: 2

gaps:
  - id: GAP-001
    dimension: anatomy
    severity: blocker
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "[file absent]"
      location: "component-lib/Badge/ directory"
      finding: >
        badge-figma.md is absent. figma-extract was never run for Badge.
        The Figma component set structure, variant axes, inner layer tree,
        component-level anatomy labels, and spacing/token bindings from Figma
        are entirely unknown. All anatomy, structure, and Figma-side token checks
        fail by absence.
    fix_action: >
      Run figma-extract for Badge using the Figma UI-components file
      (file key 5YihJ5WuDvnvrlrRMC4sBp; Badge node 2565:14) with Desktop Bridge
      active to produce badge-figma.md and a screenshot PNG.
    blocks: [badge-figma.md, tokens.md, docusaurus]
    dependency: []

  - id: GAP-002
    dimension: accessibility
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "## WCAG 2.1 AA checklist — 1.4.3 Contrast (dark mode) row"
      finding: >
        White text on dark-mode notification01 (#78CDCF) yields a contrast ratio
        of approximately 1.7:1 — well below the 4.5:1 AA threshold for normal text.
        accessibility.md flags this as "check needed" but does not resolve it.
        The dark theme may use a different (darker) text colour on the badge, but
        this is unconfirmed. No Figma source exists to verify (GAP-001).
    fix_action: >
      Confirm the actual dark-mode badge text colour by inspecting component source
      or Figma dark-theme frames. If white is used, escalate as an accessibility
      failure to the design system team. Update accessibility.md contrast row.
    blocks: [accessibility.md, docusaurus]
    dependency: [GAP-001]

  - id: GAP-003
    dimension: color_tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Colour tokens — no entry for type='secondary'"
      finding: >
        props.md documents type='secondary' as a distinct visual variant, but
        tokens.md contains no token binding for the secondary badge background,
        text colour, or border. The visual appearance of the secondary variant
        is entirely undocumented.
    fix_action: >
      After running figma-extract (GAP-001), inspect the secondary variant fills
      in Figma. Identify and document the token bindings. Update tokens.md with
      a secondary colour row.
    blocks: [tokens.md, docusaurus]
    dependency: [GAP-001]

  - id: GAP-004
    dimension: color_tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Token summary — no AIBadge section"
      finding: >
        AIBadge is documented in props.md and examples.md as a distinct component
        with its own visual style (star icon + text). tokens.md contains no token
        bindings for AIBadge background, border, icon colour, or text colour.
    fix_action: >
      After running figma-extract (GAP-001), inspect the AIBadge frame fills.
      Identify token bindings and add an AIBadge section to tokens.md.
    blocks: [tokens.md, docusaurus]
    dependency: [GAP-001]

  - id: GAP-005
    dimension: structure_spacing
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Sizing (from Figma design specs)"
      finding: >
        All sizing values (counter 16px height, 4px h-padding; dot 12×12px;
        32px border-radius) are raw pixel values extracted from Figma specs.
        No Oxygen spacing or radius token names are mapped to these values.
        The Figma Variables API was not available during extraction.
    fix_action: >
      After running figma-extract with Desktop Bridge (GAP-001), use
      getVariableByIdAsync to resolve spacing fills. Map values to Oxygen
      spacing scale tokens and update the tokens.md sizing table.
    blocks: [tokens.md, badge-figma.md]
    dependency: [GAP-001]

  - id: GAP-006
    dimension: usage_patterns
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: badge-usage.md
      location: "## Gaps — Figma Do/Don't examples row"
      finding: >
        No Figma "↳ Badge examples" page with Do/Don't card frames was found.
        figma-extract-usage cannot produce pairs. badge-usage.md acknowledges
        this limitation and provides guidelines derived from MCP docs instead,
        but Figma-sourced editorial pairs are absent.
    fix_action: >
      If a "↳ Badge examples" page is created in the Figma file in the future,
      run figma-extract-usage for Badge and merge its pairs into badge-usage.md.
      No action available until Figma examples page exists.
    blocks: [badge-usage.md, docusaurus]
    dependency: []

  - id: GAP-007
    dimension: api_props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "## Badge / Props table — children row"
      finding: >
        props.md describes children as "Rendered element inside the badge
        (numerical value only)". However, examples.md shows Badge with "99+"
        as children, where "99+" is technically a string, not a number. The
        description is ambiguous — it excludes the conventional overflow format.
    fix_action: >
      Clarify the children description in props.md: "Numerical value or overflow
      string only. Use whole numbers (e.g. 4, 12) or '99+' for counts exceeding
      two digits. Do not pass icons, arbitrary text, or other ReactNode content."
    blocks: [props.md]
    dependency: []

  - id: GAP-008
    dimension: structure_spacing
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Sizing (from Figma design specs) — no AIBadge row"
      finding: >
        The tokens.md sizing table covers counter, mention, and dot Figma types.
        AIBadge dimensions (height, padding, icon gap, font size) are not documented
        anywhere in the extracted files.
    fix_action: >
      After running figma-extract (GAP-001), inspect the AIBadge frame for
      sizing and spacing values. Add an AIBadge row to the tokens.md sizing table.
    blocks: [tokens.md]
    dependency: [GAP-001]

  - id: GAP-009
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "## WCAG 2.1 AA checklist — 1.4.11 Non-text Contrast row"
      finding: >
        WCAG 1.4.11 (Non-text Contrast ≥ 3:1) for the dot badge on white
        backgrounds is listed as "verify per usage context" with no confirmed ratio.
        The dot badge (#048284 on white) should pass (teal on white is well above 3:1)
        but no calculation is recorded.
    fix_action: >
      Calculate the contrast ratio of #048284 on #FFFFFF and #78CDCF on
      the dark-mode background. Record both ratios in the accessibility.md
      WCAG checklist. Update status to ✅ or ❌ as appropriate.
    blocks: [accessibility.md]
    dependency: []

warnings:
  - id: WARN-001
    dimension: color_tokens
    confidence: heuristic
    finding: >
      The dark-mode notification01 value (#78CDCF) is a lighter teal. If white text
      is applied in dark mode (as in light mode), contrast fails AA (≈1.7:1). However,
      the dark theme may pair the badge with a different (darker) text colour or a
      darker badge background. Do not treat this as a confirmed failure until GAP-002
      is investigated — the visual may be correct and only the documentation is incomplete.

  - id: WARN-002
    dimension: usage_patterns
    confidence: deterministic
    finding: >
      badge-pui.md explicitly states "No PUI hooks are relevant to Badge — it is a
      passive display component." This is a positive signal: the pui dimension is
      fully resolved. No further PUI work is needed for this component.
---

# Badge — Documentation Audit

> **Verdict: PARTIAL — run figma-extract to unblock anatomy/tokens, then proceed to doc-rewrite**
>
> 0 conflicts · 1 blocker source gap (badge-figma.md absent) · 7 additional source/doc gaps.
> Props, examples, accessibility, and usage_patterns are rich enough for partial rewrite now.
> Suggested next action: run figma-extract for Badge, then re-audit, then doc-rewrite.

---

## File inventory

| File | Status | Severity if absent |
|------|--------|--------------------|
| `props.md` | ✅ Present | — |
| `examples.md` | ✅ Present | — |
| `tokens.md` | ✅ Present | — |
| `accessibility.md` | ✅ Present | — |
| `badge-usage.md` | ✅ Present (MCP-derived, no Figma pairs) | — |
| `badge-pui.md` | ✅ Present ("No PUI context" — resolved) | — |
| `badge-figma.md` | ❌ **Missing (GAP-001)** | **blocker** |

---

## Dimension scores

| Dimension | Coverage | Score | Key issue |
|-----------|----------|-------|-----------|
| Anatomy | 3/8 | 0.38 | badge-figma.md absent — Figma layer tree unknown (GAP-001) |
| API / Props | 6/7 | 0.86 | `children` description ambiguous re: "99+" overflow string (GAP-007) |
| Color & Tokens | 5/9 | 0.56 | `type="secondary"` and AIBadge tokens missing; dark mode contrast open (GAP-002–004) |
| Structure & Spacing | 5/9 | 0.56 | All sizing values raw px — no token bindings confirmed (GAP-005) |
| Examples | 4/5 | 0.80 | Comprehensive MCP-sourced set; no `type="secondary"` in-context example |
| Accessibility | 5/6 | 0.83 | Dark mode contrast unresolved; 1.4.11 ratio not calculated (GAP-002, GAP-009) |
| Usage patterns | 3/5 | 0.60 | File present and honest; no Figma-sourced pairs or screenshots (GAP-006) |
| **Overall** | | **0.66** | |

---

## Conflicts

None. ✅

---

## Gap summary

| ID | Dimension | Severity | Type | Auto-fixable | Fix action |
|----|-----------|----------|------|-------------|-----------|
| GAP-001 | Anatomy | **blocker** | SOURCE_GAP | No | Run figma-extract for Badge (node 2565:14) with Desktop Bridge |
| GAP-002 | Accessibility | **major** | SOURCE_GAP | No | Confirm dark-mode badge text colour; resolve contrast ratio |
| GAP-003 | Color & Tokens | **major** | SOURCE_GAP | No | Document `type="secondary"` token bindings after figma-extract |
| GAP-004 | Color & Tokens | **major** | SOURCE_GAP | No | Document AIBadge token bindings after figma-extract |
| GAP-005 | Structure / Spacing | **major** | SOURCE_GAP | No | Map raw px values to Oxygen spacing tokens after figma-extract |
| GAP-006 | Usage patterns | **major** | SOURCE_GAP | No | No action until a Figma "↳ Badge examples" page is created |
| GAP-007 | API / Props | minor | DOC_GAP | **Yes** | Clarify `children` description to include "99+" as valid overflow string |
| GAP-008 | Structure / Spacing | minor | SOURCE_GAP | No | Document AIBadge sizing after figma-extract |
| GAP-009 | Accessibility | minor | SOURCE_GAP | No | Calculate and record 1.4.11 contrast ratios for dot badge |

---

## Warnings (advisory)

- **WARN-001 (heuristic):** Dark-mode `#78CDCF` may pair with a darker text colour in the real theme — do not declare GAP-002 a confirmed failure until the component source or Figma dark-theme frames are inspected.
- **WARN-002 (deterministic):** `badge-pui.md` confirms no PUI context — PUI dimension is fully resolved. No further PUI extraction needed.

---

## What rewrite can proceed on now (PARTIAL dimensions)

Even without badge-figma.md, doc-rewrite can produce a partial spec covering:

| Dimension | Can rewrite now? | Source |
|-----------|-----------------|--------|
| API / Props | ✅ Yes | props.md (complete; GAP-007 auto-fixable inline) |
| Examples | ✅ Yes | examples.md (MCP-sourced, comprehensive) |
| Accessibility | ✅ Yes (with open caveats) | accessibility.md (note dark mode contrast open) |
| Usage patterns | ✅ Yes (with SOURCE_GAP noted) | badge-usage.md (MCP-derived guidelines) |
| PUI | ✅ Yes | badge-pui.md ("no PUI context" — resolved) |
| Color & Tokens | ⚠ Partial | tokens.md (primary badge tokens only) |
| Anatomy | ❌ No | badge-figma.md absent |
| Structure / Spacing | ❌ No | No confirmed token bindings |

---

## Suggested next actions (in order)

1. **Run `figma-extract`** for Badge — resolves GAP-001 and unblocks anatomy, color_tokens, structure_spacing
2. **Re-audit** — aim for verdict **YES** once figma.md is present and GAP-007 is auto-fixed
3. **Run `doc-rewrite`** — can run PARTIAL now, or wait for full YES verdict after step 1–2

---

_Audited by doc-audit skill · rubric v1.0 · 2026-05-12_
