---
rubric_version: "1.0"
component: SkeletonBlock
package: "@8x8/oxygen-skeletons"
audit_date: "2026-05-15"
auditor: doc-audit skill

files_found:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - SkeletonBlock-figma.md
  - figma-screenshot-SkeletonBlock.png
  - SkeletonBlock-usage.md
  - SkeletonBlock-usage.html

files_missing:
  - SkeletonBlock-pui.md

dimension_scores:
  props:        { score: 0.45, coverage: "4/9 — SOURCE_GAP (no MCP props); CONFLICT (SkeletonCircle size format)" }
  examples:     { score: 0.60, coverage: "5/8 — all hand-crafted; SkeletonCircle size strings conflict with figma.md" }
  tokens:       { score: 0.50, coverage: "2/4 — --ui/ui02 extracted from CSS fallback; ui01 unresolved" }
  accessibility: { score: 0.70, coverage: "5/6 — full WCAG checklist present; all guidance inferred (no MCP/Figma source)" }
  figma:        { score: 0.65, coverage: "8/12 — excellent anatomy; 1 token found; no enrichment; no component key" }
  usage:        { score: 0.65, coverage: "6/6 pairs — editorial, no Figma examples page; full When-to-use, Do/Don't pairs with citations; WARN-003" }
  pui:          { score: 0.90, coverage: "PASS (assumed) — display component; no application-layer concerns expected; pui.md not produced" }

available_dimensions_avg: 0.64
overall_avg: 0.64

counts:
  doc_gaps: 1
  source_gaps: 7
  conflicts: 1
  warnings: 3

verdict: "NO"
verdict_reason: >
  GAP-001 is a CONFLICT that must be resolved before doc-rewrite can proceed.
  The `size` prop values for SkeletonCircle are documented in two incompatible
  formats: SkeletonBlock/props.md and examples.md use OX usage-doc short labels
  ("medium", "xlarge"), while SkeletonCircle/props.md and examples.md use
  Figma axis format ("40px - medium", "80px - xlarge"). The actual React prop
  values are unknown — get-component-props returned nothing for either component.
  A human must check the @8x8/oxygen-skeletons package source to determine the
  correct format, then align both component folders.
  Additionally, GAP-002 (prop names unconfirmed) means the props dimension cannot
  be fully rewritten until the React API is verified.
  Usage dimension now present (editorial, 2026-05-15) — GAP-003 closed.

gaps:
  - id: GAP-001
    dimension: props / examples
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md / examples.md / SkeletonCircle/props.md
      location: "props.md § size values (SkeletonCircle); examples.md § Basic usage and Card skeleton"
      finding: >
        props.md (SkeletonCircle section) lists size values as short labels: xlarge, large,
        medium, small, xsmall — sourced from OX usage documentation.
        examples.md uses these short labels: size="medium".
        SkeletonCircle/props.md lists Figma axis values: "80px - xlarge", "48px - large",
        "40px - medium" etc. — sourced from Figma design context.
        SkeletonCircle/examples.md uses Figma format throughout.
        The actual React prop value format is unknown — get-component-props returned nothing.
        One of these two formats is wrong.
    fix_action: "Check @8x8/oxygen-skeletons source (SkeletonCircle component) for the actual size prop enum values. Align all four files (SkeletonBlock/props.md, SkeletonBlock/examples.md, SkeletonCircle/props.md, SkeletonCircle/examples.md) to match the verified format."
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
      location: "## Props — SkeletonBlock and ## Props — SkeletonCircle"
      finding: >
        get-component-props returned no prop definitions for SkeletonBlock or SkeletonCircle.
        All props documented are Figma axis names (mode, size), not confirmed React prop names.
        The existence of a `mode` prop is especially uncertain — it may be purely a Figma
        design axis, with theming handled automatically by the Oxygen theme provider.
    fix_action: "Check @8x8/oxygen-skeletons source for all exported prop names, types, and defaults. Replace Figma-axis props with confirmed React props. If `mode` is not a React prop, remove it and add a note that theming is handled by the theme provider."
    blocks: [doc-rewrite/props-dimension]
    dependency: []

  - id: GAP-003
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    status: CLOSED
    closed_date: "2026-05-14"
    closed_by: "Editorial SkeletonBlock-usage.md authored from extracted artifacts + oxygen.8x8.com/components/skeletonloader/usage. 6 Do/Don't pairs with citations. No Figma examples page exists — see WARN-003."
    evidence:
      source_file: SkeletonBlock-usage.md
      location: "component-lib/SkeletonBlock/SkeletonBlock-usage.md"
      finding: "SkeletonBlock-usage.md now present (editorial). Figma examples page remains absent — figma-extract-usage cannot run until a designer creates the page."
    fix_action: "Create a '↳ Skeleton loader examples' Figma page with Do/Don't cards; then run figma-extract-usage to replace the editorial draft."
    blocks: []
    dependency: []

  - id: GAP-004
    dimension: pui
    severity: major
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: ~
      location: "component-lib/SkeletonBlock/ directory"
      finding: >
        SkeletonBlock-pui.md is absent. SkeletonBlock is a display-only component with no
        known application-layer concerns (no notifications, navigation, session, or event bus
        wiring). PUI concerns are unlikely but unconfirmed via MCP search.
    fix_action: "Run pui-mcp-extract for SkeletonBlock, or confirm via mcp__platform-ui-mcp__pui-search that no PUI context exists, then create SkeletonBlock-pui.md with a NOT APPLICABLE marker."
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md / SkeletonBlock-figma.md
      location: "tokens.md § Animation tokens; SkeletonBlock-figma.md § Color & token bindings"
      finding: >
        The animation token `ui01` is referenced in OX usage documentation as the animation
        start color ("alternates from ui01 to ui02") but does not appear in the Figma node
        properties. Its resolved value (hex) is unknown. The CSS fallback for `--ui/ui02`
        (#f4f3ee light, #3d3d3d dark) was extracted, but the token binding itself is unconfirmed
        from the source library. get-theme-tokens returned 0 results for "skeleton".
    fix_action: "Resolve --ui/ui02 and ui01 from the UI-Foundations token library (file key iVY5nI8JAxM05Apnnvozzs) using figma_execute + getVariableByIdAsync on the Block variant nodes, or request Variables API access."
    blocks: [doc-rewrite/tokens-dimension]
    dependency: []

  - id: GAP-006
    dimension: tokens / figma
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md / SkeletonBlock-figma.md
      location: "tokens.md § Color tokens; SkeletonBlock-figma.md § Token coverage"
      finding: >
        The Figma Variables API returned a permissions error (Enterprise plan required).
        The figma-console Desktop Bridge was offline. Token bindings for --ui/ui02 are
        documented via CSS fallback values from design context, not from the authoritative
        token library. Token names could change or have aliases not captured here.
    fix_action: "Enable Variables API access or connect Desktop Bridge to resolve token bindings from the primary library. Re-run figma-extract once available."
    blocks: [doc-rewrite/tokens-dimension]
    dependency: [GAP-005]

  - id: GAP-007
    dimension: props / figma
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: props.md / SkeletonBlock-figma.md
      location: "props.md § Props — SkeletonBlock, mode row; SkeletonBlock-figma.md § Variant axes"
      finding: >
        `mode` (Light/Dark) is a Figma variant axis documented as a prop. In practice,
        Oxygen components are themed via a theme provider and rarely expose a `mode` prop
        directly. It is likely that `mode` is a Figma design axis only, not a React prop.
        This is unverifiable without MCP prop data or package source access.
    fix_action: "Confirm via @8x8/oxygen-skeletons source whether `mode` is a React prop. If not, remove it from props.md and add a note explaining theme-provider-driven mode switching."
    blocks: []
    dependency: [GAP-002]

  - id: GAP-008
    dimension: tokens / figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md / SkeletonBlock-figma.md
      location: "tokens.md § Hardcoded values; SkeletonBlock-figma.md § Structure & spacing"
      finding: >
        Border radius 6px is hardcoded in Figma with no token binding. This may correspond
        to an Oxygen border-radius token but cannot be confirmed without Variables API access.
    fix_action: "Check UI-Foundations token library for a border-radius token at 6px. If one exists, update both tokens.md and SkeletonBlock-figma.md."
    blocks: []
    dependency: [GAP-006]

  - id: GAP-009
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: SkeletonBlock-figma.md
      location: "SkeletonBlock-figma.md § API — Component properties § Token coverage and Boolean toggles"
      finding: >
        Desktop Bridge was offline during extraction. Component key not recorded.
        Boolean toggles and instance swap slots unconfirmed. Enriched metadata unavailable.
    fix_action: "Open the Skeleton loader Figma page with Desktop Bridge running and re-run figma_get_component (format=metadata, enrich=true) on node 31984:56109."
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "accessibility.md — all sections"
      finding: >
        All accessibility guidance in accessibility.md is inferred from component type
        (passive/display). No accessibility data was returned by the Oxygen MCP and no
        ARIA annotations were found in Figma. The aria-busy pattern, keyboard behaviour,
        and prefers-reduced-motion guidance are correct by convention but unverified
        against the actual @8x8/oxygen-skeletons implementation.
    fix_action: "Verify the rendered DOM of SkeletonBlock in a browser (check for any role, aria-*, or tabIndex attributes). Confirm prefers-reduced-motion CSS behaviour. Update accessibility.md to reflect actual implementation."
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: examples
    confidence: heuristic
    note: >
      examples.md contains no examples sourced from the actual @8x8/oxygen-skeletons Storybook
      (MCP returned 0 clean examples). All code snippets were hand-crafted. The import path,
      prop names, and size values may not match the actual API until GAP-001 and GAP-002 are resolved.

  - id: WARN-002
    dimension: tokens
    confidence: heuristic
    note: >
      spacing03 (8px) is documented in tokens.md as the gap between text skeleton lines,
      sourced from OX usage documentation. This is not confirmed as a CSS token reference
      within the @8x8/oxygen-skeletons package — it may be a spacing guideline rather than
      a hardcoded token value the component enforces.

  - id: WARN-003
    dimension: usage
    confidence: deterministic
    note: >
      SkeletonBlock-usage.md is an editorial draft sourced from extracted artifacts and
      oxygen.8x8.com/components/skeletonloader/usage. No Figma "↳ Skeleton loader examples"
      page exists, so figma-extract-usage cannot run. The 6 Do/Don't pairs are grounded
      and cited but are designer-unreviewed derivations. Replace with figma-extract-usage
      output when a Figma examples page is created.

# --- navigation (added by component-map) ---
role: audit
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
siblings:
  - "[[SkeletonBlock/props]]"
  - "[[SkeletonBlock/examples]]"
  - "[[SkeletonBlock/tokens]]"
  - "[[SkeletonBlock/accessibility]]"
  - "[[SkeletonBlock/SkeletonBlock-figma]]"
  - "[[SkeletonBlock/SkeletonBlock-usage]]"
tags:
  - oxygen
  - component/SkeletonBlock
  - role/audit
  - stage/blocked
---

# SkeletonBlock — Documentation Audit

> **Verdict: NO** — resolve 1 CONFLICT before running doc-rewrite.
>
> Rubric version: 1.0 · Audited: 2026-05-15 (re-audit; prior audit 2026-05-05)

---

## File Inventory

| File | Status | Produced by |
|------|--------|-------------|
| `props.md` | ✅ Present | oxygen-mcp-extract |
| `examples.md` | ✅ Present | oxygen-mcp-extract |
| `tokens.md` | ✅ Present | oxygen-mcp-extract |
| `accessibility.md` | ✅ Present | oxygen-mcp-extract |
| `SkeletonBlock-figma.md` | ✅ Present | figma-extract |
| `figma-screenshot-SkeletonBlock.png` | ✅ Present | figma-extract |
| `SkeletonBlock-usage.md` | ✅ Present (editorial — see WARN-003) | figma-extract-usage / editorial |
| `SkeletonBlock-usage.html` | ✅ Present | figma-extract-usage / editorial |
| `SkeletonBlock-pui.md` | ⚠️ Missing — no PUI concerns expected for display component | pui-mcp-extract |

---

## Dimension Scores

| Dimension | Score | Coverage | Notes |
|-----------|-------|----------|-------|
| Props | 0.45 | 4/9 | SOURCE_GAP: no MCP data; CONFLICT: SkeletonCircle size format |
| Examples | 0.60 | 5/8 | All hand-crafted; SkeletonCircle size strings inconsistent with SkeletonCircle/props.md |
| Tokens | 0.50 | 2/4 | `--ui/ui02` extracted from CSS fallback; `ui01` unresolved |
| Accessibility | 0.70 | 5/6 | Full WCAG checklist (incl. 2.3.3); all guidance inferred |
| Figma | 0.65 | 8/12 | Excellent anatomy; 1 token; no enrichment; no component key |
| Usage | 0.65 | 6/6 pairs | Editorial (no Figma examples page) — see WARN-003 |
| PUI | 0.90 | PASS (assumed) | Display component; no application-layer concerns expected |
| **Overall avg** | **0.64** | | ↑ from 0.56 (usage dimension now scored) |

---

## Conflicts — must resolve before doc-rewrite

### GAP-001 · CONFLICT · Major — SkeletonCircle `size` value format

Two formats are documented across the pair of component folders:

- **Short labels** (from OX usage docs): `medium`, `xlarge`, `small` — used in `SkeletonBlock/props.md` and `SkeletonBlock/examples.md`
- **Figma axis format** (from design context): `"40px - medium"`, `"80px - xlarge"` — used in `SkeletonCircle/props.md` and `SkeletonCircle/examples.md`

The React API is unknown — `get-component-props` returned nothing. One format is wrong.

**Fix:** Check `@8x8/oxygen-skeletons` source for SkeletonCircle's `size` prop enum. Align all four files to the verified format.

---

## Gap Summary

| Count | Category |
|-------|----------|
| 1 | CONFLICT — **blocking doc-rewrite** |
| 6 | SOURCE_GAPs open (3 major, 3 minor; GAP-003 closed editorially) |
| 1 | DOC_GAP (minor) |
| 3 | Warnings (heuristic/deterministic, advisory) |

---

## Gaps

### CLOSED

**GAP-003** · Usage _(closed 2026-05-14)_
> `SkeletonBlock-usage.md` now present — editorial draft from oxygen.8x8.com/components/skeletonloader/usage. 6 Do/Don't pairs with citations. Figma examples page remains absent — see WARN-003.

---

### SOURCE_GAP — Blocker

**GAP-002** · Props
> `get-component-props` returned nothing. All props are Figma axis names — React prop names unconfirmed.
> **Fix:** Check `@8x8/oxygen-skeletons` source for actual prop names, types, and defaults.

### SOURCE_GAP — Major

**GAP-004** · PUI
> `SkeletonBlock-pui.md` absent — likely no concerns for a display component.
> **Fix:** Run `pui-mcp-extract` or confirm via MCP search; create file with NOT APPLICABLE marker.

**GAP-005** · Tokens
> `ui01` animation token unresolved. `--ui/ui02` extracted from CSS fallback only, not from authoritative token library.
> **Fix:** Resolve from UI-Foundations library (file key `iVY5nI8JAxM05Apnnvozzs`) via `figma_execute + getVariableByIdAsync`.

**GAP-006** · Tokens / Figma _(depends on GAP-005)_
> Variables API (Enterprise plan) and Desktop Bridge both unavailable during extraction.
> **Fix:** Enable Variables API or Desktop Bridge; re-run `figma-extract`.

### SOURCE_GAP — Minor

**GAP-007** · Props / Figma
> `mode` prop may be Figma-only — Oxygen components are typically themed by a provider, not a direct prop.
> **Fix:** Confirm via package source; remove or document accordingly.

**GAP-008** · Tokens / Figma
> Border radius `6px` hardcoded — no token binding found. Possibly a border-radius token.
> **Fix:** Check UI-Foundations library; update if a token exists.

**GAP-009** · Figma
> Desktop Bridge offline — no component key, no enrichment, boolean toggles unconfirmed.
> **Fix:** Re-run `figma_get_component` (enrich=true) on node `31984:56109` with Desktop Bridge running.

### DOC_GAP — Minor

**GAP-010** · Accessibility
> All guidance is inferred — not sourced from MCP or Figma annotations. Unverified against actual implementation.
> **Fix:** Verify rendered DOM in browser; confirm `prefers-reduced-motion` CSS behaviour.

---

## Warnings

**WARN-001 (Examples):** All code snippets hand-crafted — MCP returned 0 clean examples. Prop names and size values unverified until GAP-001 / GAP-002 resolved.

**WARN-002 (Tokens):** `spacing03` (8px) gap guidance is from usage docs only — unconfirmed as an enforced CSS value within the component.

**WARN-003 (Usage):** `SkeletonBlock-usage.md` is an editorial draft (no Figma examples page). 6 pairs are grounded in sibling files + oxygen.8x8.com but designer-unreviewed. Replace with `figma-extract-usage` output when a Figma examples page is created.

---

## Suggested next actions

```
1. Resolve GAP-001 (size format CONFLICT) — check @8x8/oxygen-skeletons source, align all 4 files
2. Resolve GAP-002 (prop names)           — same source check; update props.md and examples
3. Fix GAP-007 (mode prop)                — confirm theme-provider behaviour; update props.md
4. Resolve token bindings (GAP-005/006)   — needs Variables API or figma_execute
5. Run pui-mcp-extract or add N/A marker  — closes GAP-004
6. Run doc-rewrite                        — after conflict resolved
```

_Source: doc-audit skill v1.0 · Re-audited 2026-05-15 (prior: 2026-05-05) · component-lib/SkeletonBlock/_
