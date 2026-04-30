---
# ============================================================
# AlertBanner — Documentation Audit
# ============================================================
component: AlertBanner
rubric_version: "1.0"
audited: 2026-04-28
verdict: "NO"
verdict_reason: "2 unresolved CONFLICTs — resolve before doc-rewrite"

files_present:
  - props.md
  - examples.md
  - tokens.md
  - accessibility.md
  - alert-banner-figma.md

files_missing:
  - file: alert-banner-usage.md
    produced_by: figma-extract-usage
    severity: major
  - file: alert-banner-pui.md
    produced_by: pui-mcp-extract
    severity: major

scores:
  anatomy:          { coverage: "4/8",  score: 0.50 }
  api_props:        { coverage: "4/5",  score: 0.80 }
  color_tokens:     { coverage: "2/9",  score: 0.22 }
  structure_spacing:{ coverage: "5/9",  score: 0.56 }
  examples:         { coverage: "4/5",  score: 0.80 }
  accessibility:    { coverage: "4/6",  score: 0.67 }
  usage_patterns:   { coverage: "0/5",  score: 0.00 }
  overall:          0.51

counts:
  doc_gaps: 4
  source_gaps: 12
  conflicts: 2
  warnings: 3

conflicts:
  - id: CONFLICT-001
    dimension: api_props
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: alert-banner-figma.md
      location: "## API — Component properties / Variant axes; ## Gaps & conflicts row 8"
      finding: >
        Figma component set exposes two variant axes — mode (light | dark) and
        breakpoint (> 576 | < 576). The Oxygen MCP returns 5 props; neither axis
        corresponds to a prop. It is unconfirmed whether the component handles
        mode/breakpoint automatically (e.g. via CSS media queries / theming context)
        or requires explicit parent-level wiring.
    fix_action: >
      Confirm with design system team or component source: are mode and breakpoint
      handled internally, or must consumer supply theme/breakpoint context?
      Update props.md and alert-banner-figma.md with the authoritative answer.
    blocks: [props.md, alert-banner-figma.md, storybook, docusaurus]
    dependency: []

  - id: CONFLICT-002
    dimension: color_tokens
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: alert-banner-figma.md
      location: "## Color & token bindings / Banner container background"
      finding: >
        Raw fill value #F8AE1A extracted from all 4 variants matches alertYellow
        dark-mode value exactly (colorPalette.yellow06). However the Oxygen theme
        registry documents alertYellow as a data-visualisation token (graphs, bars,
        quality indicators) — not an AlertBanner component token. This is either a
        naming conflict (different token reusing the same palette value) or a
        scoping error in the registry description.
    fix_action: >
      Confirm with design system token owner: does AlertBanner use alertYellow directly,
      a separate semantic token that aliases yellow06, or a hardcoded value?
      Update tokens.md with the canonical token name and scope.
    blocks: [tokens.md, alert-banner-figma.md, docusaurus]
    dependency: []

gaps:
  - id: GAP-001
    dimension: anatomy
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: alert-banner-figma.md
      location: "## Anatomy — note below table"
      finding: >
        Rows 6–8 (warning icon, message text, action button) are inferred from the
        screenshot and Oxygen props. The Figma REST API did not return inner children
        of the variant nodes (nodeId depth limit). Layer names, IDs, and exact roles
        are unconfirmed.
    fix_action: >
      Run figma-extract with the Figma Desktop Bridge plugin active, or manually
      inspect node 13899:15489 children in the Figma file to confirm inner anatomy.
    blocks: [alert-banner-figma.md]
    dependency: []

  - id: GAP-002
    dimension: anatomy
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: alert-banner-figma.md
      location: "## API — Component properties / Boolean toggles"
      finding: >
        The boolean toggle property name for the action button is listed as
        "Action button visible" — inferred from screenshot behaviour and actionText
        prop. No Figma boolean property name was returned by the API.
    fix_action: >
      Confirm the Figma boolean property name (e.g. "Show action", "hasAction")
      via Desktop Bridge and update alert-banner-figma.md Boolean toggles table.
    blocks: [alert-banner-figma.md]
    dependency: []

  - id: GAP-003
    dimension: api_props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "## Props table — no entry for mode or breakpoint"
      finding: >
        The mode and breakpoint Figma variant axes are mentioned in alert-banner-figma.md
        but props.md does not explicitly confirm they are non-consumer props. A reader
        of props.md alone would not know whether to pass mode or breakpoint to the component.
    fix_action: >
      Add a "Layout behaviour" note to props.md confirming mode and breakpoint are
      internal concerns (after CONFLICT-001 is resolved).
    blocks: [props.md, docusaurus]
    dependency: [CONFLICT-001]

  - id: GAP-004
    dimension: api_props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "## Props table — actionText and actionCallback rows"
      finding: >
        The Oxygen MCP returned empty description strings for actionText and
        actionCallback. props.md supplies editorial context but flags no official
        description.
    fix_action: >
      Escalate to Oxygen team to add official descriptions in the registry, or
      confirm the editorial descriptions in props.md are authoritative.
    blocks: [props.md]
    dependency: []

  - id: GAP-005
    dimension: color_tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: alert-banner-figma.md
      location: "## API — Component properties / Token coverage"
      finding: >
        figma_get_variables failed — REST API token lacks variable-read permission
        and Figma Desktop Bridge was unavailable. Zero confirmed token bindings for
        any property of the component.
    fix_action: >
      Re-run figma-extract with Desktop Bridge active or request elevated Figma
      REST token permissions. All color and spacing token columns in tokens.md
      and alert-banner-figma.md must be re-populated.
    blocks: [tokens.md, alert-banner-figma.md, docusaurus]
    dependency: []

  - id: GAP-006
    dimension: color_tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Missing tokens — Text colour row"
      finding: >
        Inner layer children of variant nodes were not returned. Text colour is
        listed as "unknown" in both tokens.md and accessibility.md.
    fix_action: >
      Inspect inner children of variant 13899:15490 (or any variant) in Figma —
      extract text fill token/hex. Update tokens.md and accessibility.md contrast table.
    blocks: [tokens.md, accessibility.md]
    dependency: [GAP-005]

  - id: GAP-007
    dimension: color_tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Missing tokens — Icon colour row"
      finding: >
        Icon colour is listed as "unknown" — inner layer children not returned by API.
    fix_action: >
      Inspect warning icon fill in Figma inner layer tree.
      Update tokens.md icon colour row.
    blocks: [tokens.md, accessibility.md]
    dependency: [GAP-005]

  - id: GAP-008
    dimension: color_tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Summary"
      finding: >
        Oxygen theme registry contains no AlertBanner-scoped tokens. Either they
        exist under a different search term, or the component uses global semantic
        tokens without a component-specific namespace.
    fix_action: >
      Search the Oxygen token registry with wider terms (e.g. "warning", "notification",
      "feedback") and confirm absence. Note result explicitly in tokens.md.
    blocks: [tokens.md]
    dependency: []

  - id: GAP-009
    dimension: structure_spacing
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "## Spacing / layout values (raw — no tokens confirmed)"
      finding: >
        All 4 spacing values (padding-H 16 px, padding-V 12 px, gap-desktop 16 px,
        gap-mobile 8 px) are raw pixel values with no confirmed token binding.
        Depends on Variables API access (GAP-005).
    fix_action: >
      After resolving GAP-005, map spacing values to Oxygen spacing scale tokens.
      Update tokens.md and alert-banner-figma.md Structure & spacing token column.
    blocks: [tokens.md, alert-banner-figma.md]
    dependency: [GAP-005]

  - id: GAP-010
    dimension: structure_spacing
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: alert-banner-figma.md
      location: "## Structure & spacing / Auto-layout / Alignment"
      finding: >
        Auto-layout alignment (cross-axis, primary-axis) not returned because inner
        children were not resolved in the API response.
    fix_action: >
      Inspect auto-layout settings on variant frames in Figma.
      Update alert-banner-figma.md Auto-layout section.
    blocks: [alert-banner-figma.md]
    dependency: []

  - id: GAP-011
    dimension: examples
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "## Storybook documentation story"
      finding: >
        Oxygen MCP returned 0 clean/standalone examples. All examples in examples.md
        are editorially derived from prop definitions and Figma design — not sourced
        from official Oxygen documentation or tested snippets.
    fix_action: >
      Request official usage examples from the Oxygen team or validate editorial
      examples against the real component in a test environment.
    blocks: [examples.md, storybook, docusaurus]
    dependency: []

  - id: GAP-012
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "## Full example — last code block"
      finding: >
        No edge-case examples documented: actionText without actionCallback, very
        long message text causing line-wrap, ReactNode children (non-string).
    fix_action: >
      Add edge-case examples for: actionText with missing actionCallback, long
      message wrapping, and non-string children.
    blocks: [examples.md]
    dependency: []

  - id: GAP-013
    dimension: accessibility
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "## ARIA role"
      finding: >
        The ARIA role used in the component implementation is unknown. Figma has no
        a11y annotations. The Oxygen API exposes no role prop. accessibility.md
        documents two candidates (role="alert", role="status") but cannot confirm
        which is implemented.
    fix_action: >
      Inspect component source code (@8x8/oxygen-alert-banner) to confirm the
      implemented ARIA role. Update accessibility.md ARIA role section.
    blocks: [accessibility.md, docusaurus]
    dependency: []

  - id: GAP-014
    dimension: accessibility
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "## Colour contrast table"
      finding: >
        Text and icon colours are unknown (GAP-006, GAP-007), making contrast ratio
        calculation impossible. All 6 WCAG checklist criteria are marked ⚠ Unverified.
    fix_action: >
      After resolving GAP-006 and GAP-007, calculate contrast ratios for text-on-amber
      and icon-on-amber. Update WCAG checklist statuses.
    blocks: [accessibility.md]
    dependency: [GAP-006, GAP-007]

  - id: GAP-015
    dimension: usage_patterns
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "[file absent]"
      location: "component-lib/AlertBanner/ directory"
      finding: >
        alert-banner-usage.md is absent. figma-extract-usage skill was not run.
        Do/Don't usage guidelines from Figma are not available.
    fix_action: >
      Run figma-extract-usage for AlertBanner using the same Figma URL to produce
      alert-banner-usage.md with annotated do/don't examples.
    blocks: [alert-banner-usage.md, docusaurus]
    dependency: []

  - id: GAP-016
    dimension: usage_patterns
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "[file absent]"
      location: "component-lib/AlertBanner/ directory"
      finding: >
        alert-banner-pui.md is absent. pui-mcp-extract skill was not run.
        Platform UI component context is unavailable.
    fix_action: >
      Run pui-mcp-extract for AlertBanner to determine whether a PUI equivalent exists
      and produce alert-banner-pui.md (or note "NO RELEVANT PUI CONTEXT").
    blocks: [alert-banner-pui.md]
    dependency: []

warnings:
  - id: WARN-001
    dimension: color_tokens
    confidence: heuristic
    finding: >
      The banner background fill #F8AE1A is identical across all four variants
      (light AND dark) in the Figma reconstruction. If the component is truly
      mode-adaptive, this likely indicates the Variables API failed to resolve
      aliases rather than the component using a fixed colour. Do not treat all
      four as "the same token binding" — they may differ under correct variable
      resolution.

  - id: WARN-002
    dimension: anatomy
    confidence: heuristic
    finding: >
      The off-canvas _Information & support frame (node 48956:2083) is correctly
      excluded from anatomy. However, the "Stable" status badge inside it suggests
      this component is production-ready — which is a positive signal for
      prioritising this documentation.

  - id: WARN-003
    dimension: examples
    confidence: heuristic
    finding: >
      examples.md includes the full Storybook documentation story, which imports
      README and CHANGELOG markdown files. These may contain additional usage
      guidance not surfaced via MCP. Consider inspecting the Storybook source for
      exampleAlertBanner content.
---

# AlertBanner — Documentation Audit

> **Verdict: NO — resolve CONFLICTs before doc-rewrite**
>
> 2 conflicts block accurate documentation. 12 source gaps and 4 doc gaps identified.
> Suggested next action: resolve CONFLICT-001 and CONFLICT-002 with the design/dev team,
> then run pui-mcp-extract and figma-extract-usage, then re-audit.

---

## File inventory

| File | Status | Severity if absent |
|------|--------|--------------------|
| `props.md` | ✅ Present | — |
| `examples.md` | ✅ Present | — |
| `tokens.md` | ✅ Present | — |
| `accessibility.md` | ✅ Present | — |
| `alert-banner-figma.md` | ✅ Present | — |
| `alert-banner-usage.md` | ❌ Missing (GAP-015) | major |
| `alert-banner-pui.md` | ❌ Missing (GAP-016) | major |

---

## Dimension scores

| Dimension | Coverage | Score | Key issue |
|-----------|----------|-------|-----------|
| Anatomy | 4/8 | 0.50 | Inner layer children not returned by API (GAP-001) |
| API / Props | 4/5 | 0.80 | mode/breakpoint axes unresolved (CONFLICT-001) |
| Color & Tokens | 2/9 | 0.22 | Variables API unavailable — zero confirmed bindings (GAP-005) |
| Structure & Spacing | 5/9 | 0.56 | All spacing values raw px, no tokens confirmed (GAP-009) |
| Examples | 4/5 | 0.80 | All examples editorially derived, no MCP-sourced snippets (GAP-011) |
| Accessibility | 4/6 | 0.67 | ARIA role unconfirmed; contrast unverifiable (GAP-013, GAP-014) |
| Usage patterns | 0/5 | 0.00 | File absent — figma-extract-usage not run (GAP-015) |
| **Overall** | | **0.51** | |

---

## Conflicts (must resolve before doc-rewrite)

### CONFLICT-001 — Figma variant axes vs Oxygen API props
- **Dimension:** API / Props
- **Severity:** major
- **Files:** `alert-banner-figma.md`, `props.md`
- **Finding:** Figma exposes `mode` (light | dark) and `breakpoint` (> 576 | < 576) as variant axes. The Oxygen API has 5 props — none correspond to these axes. It is unconfirmed whether the component handles these internally (CSS media queries, theme context) or needs parent wiring.
- **Fix:** Confirm with design system team or component source code. Update props.md.

### CONFLICT-002 — Banner background token identity
- **Dimension:** Color & Tokens
- **Severity:** major
- **Files:** `tokens.md`, `alert-banner-figma.md`
- **Finding:** Raw fill `#F8AE1A` matches `alertYellow` dark value (`colorPalette.yellow06`). But `alertYellow` is documented as a data-visualisation token, not an AlertBanner token. Either the component aliases the same palette entry via a different semantic token, or `alertYellow` is being used out of its documented scope.
- **Fix:** Confirm with token owner whether AlertBanner has a dedicated warning/banner token or intentionally uses `alertYellow`.

---

## Gap summary

| ID | Dimension | Severity | Type | Auto-fixable | Fix action |
|----|-----------|----------|------|-------------|-----------|
| GAP-001 | Anatomy | minor | SOURCE_GAP | No | Run figma-extract with Desktop Bridge to confirm inner layer children |
| GAP-002 | Anatomy | minor | SOURCE_GAP | No | Confirm boolean property name via Desktop Bridge |
| GAP-003 | API / Props | minor | DOC_GAP | Yes | Add layout-behaviour note to props.md (after CONFLICT-001 resolved) |
| GAP-004 | API / Props | minor | DOC_GAP | Yes | Escalate empty `actionText`/`actionCallback` descriptions to Oxygen team |
| GAP-005 | Color & Tokens | **major** | SOURCE_GAP | No | Re-run extraction with Desktop Bridge or elevated REST permissions |
| GAP-006 | Color & Tokens | **major** | SOURCE_GAP | No | Extract text fill from inner layer children in Figma |
| GAP-007 | Color & Tokens | **major** | SOURCE_GAP | No | Extract icon fill from inner layer children in Figma |
| GAP-008 | Color & Tokens | minor | SOURCE_GAP | No | Widen token search (try "warning", "notification", "feedback") |
| GAP-009 | Structure / Spacing | **major** | SOURCE_GAP | No | Map raw px values to Oxygen spacing tokens after GAP-005 resolved |
| GAP-010 | Structure / Spacing | minor | SOURCE_GAP | No | Inspect auto-layout alignment in Figma |
| GAP-011 | Examples | **major** | SOURCE_GAP | No | Request official examples from Oxygen team; validate editorial snippets |
| GAP-012 | Examples | minor | DOC_GAP | Yes | Add edge-case examples (long text, missing actionCallback, ReactNode children) |
| GAP-013 | Accessibility | **major** | SOURCE_GAP | No | Inspect component source to confirm ARIA role implementation |
| GAP-014 | Accessibility | **major** | SOURCE_GAP | No | Calculate contrast once GAP-006/007 resolved |
| GAP-015 | Usage patterns | **major** | SOURCE_GAP | No | Run figma-extract-usage skill |
| GAP-016 | Usage patterns | **major** | SOURCE_GAP | No | Run pui-mcp-extract skill |

---

## Warnings (advisory)

- **WARN-001:** All 4 Figma variants returned identical fill `#F8AE1A` — likely Variables API failure to resolve aliases, not a real same-colour design decision.
- **WARN-002:** "Stable" status badge in the Figma info card confirms this is a production component — prioritise resolving the major source gaps.
- **WARN-003:** Storybook source `exampleAlertBanner` markdown reference may contain additional usage guidance not surfaced via MCP — worth inspecting.

---

## Suggested next actions (in order)

1. **Resolve CONFLICT-001** — confirm mode/breakpoint handling with design system team
2. **Resolve CONFLICT-002** — confirm banner token name with token owner
3. **Run `figma-extract-usage`** to produce `alert-banner-usage.md` (do/don't patterns)
4. **Run `pui-mcp-extract`** to produce `alert-banner-pui.md`
5. **Fix Variables API access** (GAP-005) — then re-run figma-extract to fill token columns
6. **Inspect component source** to confirm ARIA role (GAP-013) and mode/breakpoint handling (CONFLICT-001)
7. **Re-run `doc-audit`** — aim for verdict **PARTIAL** or **YES** before proceeding to doc-rewrite

---

_Audited by doc-audit skill · rubric v1.0 · 2026-04-28_
