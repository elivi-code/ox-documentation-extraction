---
rubric_version: "1.0"
component: SkeletonCircle
package: "@8x8/oxygen-skeletons"
audit_date: "2026-05-05"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - SkeletonCircle-figma.md
  - figma-screenshot-SkeletonCircle.png

files_missing:
  - SkeletonCircle-usage.md
  - SkeletonCircle-pui.md

dimension_scores:
  props:        { score: 0.45, coverage: "4/9 — SOURCE_GAP (no MCP props); CONFLICT (size format vs SkeletonBlock docs)" }
  examples:     { score: 0.65, coverage: "5/8 — all hand-crafted; format consistent within this folder; good variety" }
  tokens:       { score: 0.50, coverage: "2/4 — --ui/ui02 extracted from CSS fallback; ui01 unresolved" }
  accessibility:{ score: 0.70, coverage: "5/6 — full WCAG checklist present; all guidance inferred (no MCP/Figma source)" }
  figma:        { score: 0.70, coverage: "9/12 — excellent anatomy (18 variants); 1 token; design decisions noted; no component key" }
  usage:        { score: 0.00, coverage: "0/0 — SOURCE_GAP (file missing)" }
  pui:          { score: 0.90, coverage: "PASS (assumed) — display component; no application-layer concerns expected; pui.md not produced" }

available_dimensions_avg: 0.64
overall_avg: 0.56

counts:
  doc_gaps: 1
  source_gaps: 9
  conflicts: 1
  warnings: 2

verdict: NO
verdict_reason: >
  GAP-001 is a CONFLICT that must be resolved before doc-rewrite can proceed.
  SkeletonCircle/props.md and examples.md document size values in Figma axis
  format ("80px - xlarge", "40px - medium"), while SkeletonBlock/props.md and
  examples.md use OX usage-doc short labels ("xlarge", "medium"). The actual
  React `size` prop enum is unknown because get-component-props returned nothing
  for SkeletonCircle. A human must verify the @8x8/oxygen-skeletons source to
  determine the correct format and align both component folders.
  GAP-002 (prop names unconfirmed) also blocks the props dimension rewrite.

gaps:
  - id: GAP-001
    dimension: props / examples
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md / examples.md / SkeletonBlock/props.md / SkeletonBlock/examples.md
      location: "props.md § size values table; examples.md § all snippets; SkeletonBlock/props.md § SkeletonCircle section"
      finding: >
        SkeletonCircle/props.md and SkeletonCircle/examples.md use Figma axis format:
        "80px - xlarge", "48px - large", "40px - medium", "32px - small", "28px - small",
        "24px - xsmall" etc. — sourced from Figma design context.
        SkeletonBlock/props.md (SkeletonCircle section) and SkeletonBlock/examples.md use
        short labels: xlarge, large, medium, small, xsmall — sourced from OX usage docs.
        The actual React prop value format is unknown — get-component-props returned nothing.
        One of these two formats is wrong; they cannot both be correct.
    fix_action: "Check @8x8/oxygen-skeletons source for the SkeletonCircle size prop enum. Align all four files (SkeletonCircle/props.md, SkeletonCircle/examples.md, SkeletonBlock/props.md, SkeletonBlock/examples.md) to the verified format."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-002
    dimension: props
    severity: blocker
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "## Props — SkeletonCircle"
      finding: >
        get-component-props returned no prop definitions for SkeletonCircle.
        All props documented are Figma axis names (mode, size), not confirmed React prop names.
        The existence of a `mode` prop is particularly uncertain — it may be a Figma design
        axis only, with theming handled by the Oxygen theme provider.
        The default for `size` ("80px - xlarge") is the Figma component default, not the
        confirmed React prop default.
    fix_action: "Check @8x8/oxygen-skeletons source for all exported SkeletonCircle props, types, and defaults. Replace Figma-axis props with confirmed React props. Remove `mode` if not a React prop."
    blocks: [doc-rewrite/props-dimension]
    dependency: []

  - id: GAP-003
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ~
      location: "component-lib/SkeletonCircle/ directory"
      finding: "SkeletonCircle-usage.md is absent — figma-extract-usage has not been run."
    fix_action: "Run figma-extract-usage for the Skeleton loader Figma page to produce SkeletonCircle-usage.md with Do/Don't editorial guidance."
    blocks: [doc-rewrite/usage-dimension]
    dependency: []

  - id: GAP-004
    dimension: pui
    severity: major
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: ~
      location: "component-lib/SkeletonCircle/ directory"
      finding: >
        SkeletonCircle-pui.md is absent. SkeletonCircle is a display-only component with no
        known application-layer concerns. PUI concerns are unlikely but unconfirmed via MCP search.
    fix_action: "Run pui-mcp-extract or confirm via mcp__platform-ui-mcp__pui-search that no PUI context exists; create SkeletonCircle-pui.md with a NOT APPLICABLE marker."
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md / SkeletonCircle-figma.md
      location: "tokens.md § Animation tokens; SkeletonCircle-figma.md § Color & token bindings"
      finding: >
        The animation token `ui01` is referenced in OX usage documentation as the animation
        start color but does not appear in the Figma node properties for this component.
        `--ui/ui02` was extracted from CSS fallback values in design context, not from the
        authoritative token library. get-theme-tokens returned 0 results for "skeleton".
    fix_action: "Resolve --ui/ui02 and ui01 from the UI-Foundations token library (file key iVY5nI8JAxM05Apnnvozzs) using figma_execute + getVariableByIdAsync on Circle variant nodes."
    blocks: [doc-rewrite/tokens-dimension]
    dependency: []

  - id: GAP-006
    dimension: tokens / figma
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md / SkeletonCircle-figma.md
      location: "tokens.md § Color tokens; SkeletonCircle-figma.md § Token coverage"
      finding: >
        Figma Variables API unavailable (Enterprise plan). Desktop Bridge offline.
        Token bindings documented from CSS fallback only, not confirmed from source library.
    fix_action: "Enable Variables API or connect Desktop Bridge; re-run figma-extract on node 31984:56124."
    blocks: [doc-rewrite/tokens-dimension]
    dependency: [GAP-005]

  - id: GAP-007
    dimension: props
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "props.md § size values table — multiple rows with same size label"
      finding: >
        Two size values map to the label "small" (32px and 28px) and four map to "xsmall"
        (24px, 22px, 20px, 16px). If the React API uses short labels (xlarge/large/medium/
        small/xsmall), these duplicate labels would be ambiguous and imply a different
        underlying API than the Figma axis format suggests. The actual enum is unknown.
    fix_action: "Resolve via GAP-001 source check. If short labels are used, document how 32px vs 28px are distinguished. If Figma format is used, the px value disambiguates."
    blocks: []
    dependency: [GAP-001]

  - id: GAP-008
    dimension: props / figma
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md / SkeletonCircle-figma.md
      location: "props.md § mode row; SkeletonCircle-figma.md § Variant axes"
      finding: >
        `mode` (Light/Dark) is a Figma variant axis documented as a prop. It likely
        is not a React prop — Oxygen components are themed via a theme provider.
        Unverifiable without MCP prop data or package source access.
    fix_action: "Confirm via @8x8/oxygen-skeletons source. If not a React prop, remove from props.md and add a theming note."
    blocks: []
    dependency: [GAP-002]

  - id: GAP-009
    dimension: tokens / figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md / SkeletonCircle-figma.md
      location: "tokens.md § Hardcoded values; SkeletonCircle-figma.md § Structure & spacing"
      finding: >
        Border radius 100px (fully rounded) is hardcoded in Figma with no token binding.
        While 100px is a conventional full-round value, it may correspond to an Oxygen
        border-radius token and cannot be confirmed without Variables API access.
    fix_action: "Check UI-Foundations token library for a full-rounded border-radius token. Update tokens.md and SkeletonCircle-figma.md if one exists."
    blocks: []
    dependency: [GAP-006]

  - id: GAP-010
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: SkeletonCircle-figma.md
      location: "SkeletonCircle-figma.md § API — Component properties § Token coverage and Boolean toggles"
      finding: >
        Desktop Bridge offline during extraction. Component key not recorded.
        Boolean toggles and instance swap slots unconfirmed. Enriched metadata unavailable.
    fix_action: "Re-run figma_get_component (format=metadata, enrich=true) on node 31984:56124 with Desktop Bridge running."
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "accessibility.md — all sections"
      finding: >
        All accessibility guidance is inferred from component type (passive/display).
        No accessibility data returned by Oxygen MCP. No ARIA annotations in Figma.
        The aria-busy pattern, keyboard behaviour, and prefers-reduced-motion guidance
        are correct by convention but unverified against the actual implementation.
    fix_action: "Verify the rendered DOM of SkeletonCircle in a browser. Confirm prefers-reduced-motion CSS behaviour. Update accessibility.md to reflect actual implementation."
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: examples
    confidence: heuristic
    note: >
      examples.md contains no examples sourced from the actual @8x8/oxygen-skeletons Storybook
      (MCP returned 0 clean examples). All code snippets were hand-crafted using Figma axis
      format ("40px - medium"). If GAP-001 resolves to short-label format, all examples must be rewritten.

  - id: WARN-002
    dimension: tokens
    confidence: heuristic
    note: >
      spacing03 (8px) gap guidance is from OX usage documentation only — unconfirmed as an
      enforced CSS token value within the @8x8/oxygen-skeletons package. May be a spacing
      guideline rather than a hardcoded constraint.
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
siblings:
  - "[[SkeletonCircle/props]]"
  - "[[SkeletonCircle/examples]]"
  - "[[SkeletonCircle/tokens]]"
  - "[[SkeletonCircle/accessibility]]"
  - "[[SkeletonCircle/SkeletonCircle-figma]]"
tags:
  - oxygen
  - component/SkeletonCircle
  - role/audit
  - stage/blocked
---

# SkeletonCircle — Documentation Audit

> **Verdict: NO** — resolve 1 CONFLICT before running doc-rewrite.
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
| `SkeletonCircle-figma.md` | ✅ Present | figma-extract |
| `figma-screenshot-SkeletonCircle.png` | ✅ Present | figma-extract |
| `SkeletonCircle-usage.md` | ❌ **MISSING** | figma-extract-usage |
| `SkeletonCircle-pui.md` | ⚠️ Missing — no PUI concerns expected for display component | pui-mcp-extract |

---

## Dimension Scores

| Dimension | Score | Coverage | Notes |
|-----------|-------|----------|-------|
| Props | 0.45 | 4/9 | SOURCE_GAP: no MCP data; CONFLICT: size format vs SkeletonBlock docs |
| Examples | 0.65 | 5/8 | All hand-crafted; Figma format used consistently within this folder |
| Tokens | 0.50 | 2/4 | `--ui/ui02` from CSS fallback; `ui01` unresolved |
| Accessibility | 0.70 | 5/6 | Full WCAG checklist (incl. 2.3.3); all guidance inferred |
| Figma | 0.70 | 9/12 | 18 variants documented; 1 token; design decisions noted; no component key |
| Usage | 0.00 | — | ❌ SOURCE_GAP (major) — file missing |
| PUI | 0.90 | PASS (assumed) | Display component; no application-layer concerns expected |
| **Available avg** | **0.64** | | (excl. usage) |
| **Overall avg** | **0.56** | | |

---

## Conflicts — must resolve before doc-rewrite

### GAP-001 · CONFLICT · Major — `size` value format inconsistent across component pair

SkeletonCircle's own files use Figma axis format (`"40px - medium"`, `"80px - xlarge"`) while SkeletonBlock's files reference SkeletonCircle using short labels (`"medium"`, `"xlarge"`). The actual React `size` prop enum is unknown. Both cannot be correct.

**Fix:** Check `@8x8/oxygen-skeletons` source; align all four files.

---

## Gap Summary

| Count | Category |
|-------|----------|
| 1 | CONFLICT — **blocking doc-rewrite** |
| 9 | SOURCE_GAPs (4 major, 5 minor) |
| 1 | DOC_GAP (minor) |
| 2 | Warnings (heuristic, advisory) |

---

## Gaps

### SOURCE_GAP — Blocker

**GAP-002** · Props
> `get-component-props` returned nothing. React prop names unconfirmed; all from Figma axes.
> **Fix:** Check `@8x8/oxygen-skeletons` source; update props.md with confirmed API.

### SOURCE_GAP — Major

**GAP-003** · Usage
> `SkeletonCircle-usage.md` absent — `figma-extract-usage` not run.
> **Fix:** Run `figma-extract-usage` for the Skeleton loader page.

**GAP-004** · PUI
> `SkeletonCircle-pui.md` absent — likely no concerns for a display component.
> **Fix:** Run `pui-mcp-extract` or add NOT APPLICABLE marker.

**GAP-005** · Tokens
> `ui01` unresolved; `--ui/ui02` from CSS fallback only; get-theme-tokens returned 0 results.
> **Fix:** Resolve from UI-Foundations library (`iVY5nI8JAxM05Apnnvozzs`) via `figma_execute + getVariableByIdAsync`.

**GAP-006** · Tokens / Figma _(depends on GAP-005)_
> Variables API and Desktop Bridge both unavailable during extraction.
> **Fix:** Enable access; re-run `figma-extract` on node `31984:56124`.

### SOURCE_GAP — Minor

**GAP-007** · Props
> Duplicate size labels: two "small" sizes (32px, 28px) and four "xsmall" sizes (24px–16px). Ambiguous if short labels are the React API.
> **Fix:** Resolve via GAP-001; document disambiguation clearly.

**GAP-008** · Props / Figma
> `mode` prop likely theme-provider-driven, not a direct React prop.
> **Fix:** Confirm via package source; remove from props.md if not a prop.

**GAP-009** · Tokens / Figma
> Border radius `100px` hardcoded; may correspond to a token.
> **Fix:** Check UI-Foundations library; update if a token exists.

**GAP-010** · Figma
> Desktop Bridge offline — no component key, no enrichment, boolean toggles unconfirmed.
> **Fix:** Re-run `figma_get_component` (enrich=true) on node `31984:56124` with Bridge running.

### DOC_GAP — Minor

**GAP-011** · Accessibility
> All guidance inferred — unverified against actual `@8x8/oxygen-skeletons` implementation.
> **Fix:** Verify rendered DOM and CSS; update accessibility.md.

---

## Warnings

**WARN-001 (Examples):** All snippets hand-crafted using Figma format. If GAP-001 resolves to short labels, all examples must be rewritten.

**WARN-002 (Tokens):** `spacing03` guidance sourced from usage docs only — unconfirmed as an enforced CSS value in the package.

---

## Suggested next actions

```
1. Resolve GAP-001 (size format CONFLICT) — check @8x8/oxygen-skeletons source; align all 4 files
2. Resolve GAP-002 (prop names)           — same source check; update props.md, examples.md
3. Fix GAP-007 (duplicate size labels)    — document disambiguation after GAP-001 resolved
4. Fix GAP-008 (mode prop)                — confirm theme-provider behaviour; update props.md
5. Run figma-extract-usage                — closes GAP-003
6. Resolve token bindings (GAP-005/006)   — needs Variables API or figma_execute
7. Run pui-mcp-extract or add N/A marker  — closes GAP-004
8. Run doc-rewrite                        — after conflict resolved
```

_Source: doc-audit skill v1.0 · Audited from component-lib/SkeletonCircle/ · 2026-05-05_
