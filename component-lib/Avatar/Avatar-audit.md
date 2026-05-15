---
rubric_version: 1.0
component: Avatar
audited: 2026-05-11
verdict: "NO"
verdict_reason: "Two unresolved CONFLICTs require human verification before doc-rewrite can proceed"
audit_note: "Partial re-audit 2026-05-11 — Avatar-usage.md added editorially (GAP-001 resolved). All other findings unchanged."

files_found:
  - Avatar/props.md
  - Avatar/examples.md
  - Avatar/tokens.md
  - Avatar/accessibility.md
  - Avatar/Avatar-figma.md
  - Avatar/Avatar-usage.md   # editorial — authored from extracted artifacts, no Figma examples page

files_missing:
  - Avatar/Avatar-pui.md     # pui-mcp-extract not run

dimension_scores:
  source_completeness: { score: 0.86, coverage: "6/7" }
  props:               { score: 0.79, coverage: "11/14" }
  tokens:              { score: 0.77, coverage: "10/13" }
  figma_spec:          { score: 0.88, coverage: "14/16" }
  examples:            { score: 0.80, coverage: "8/10", confidence: heuristic }
  accessibility:       { score: 0.89, coverage: "8/9" }
  usage:               { score: 0.75, coverage: "7 pairs (editorial)", confidence: heuristic }
  cross_file:          { score: 0.90, coverage: "9/10" }

totals:
  doc_gaps: 8
  source_gaps: 8
  conflicts: 2
  warnings: 4

gaps:
  - id: GAP-001
    dimension: source_completeness
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    status: RESOLVED
    resolved: "2026-05-11 — Avatar-usage.md authored editorially (7 Do/Don't pairs, grounded in extracted artifacts). No Figma examples page exists; replace with figma-extract-usage output when one is created."
    evidence:
      source_file: ~
      location: "Avatar/ directory"
      finding: "Avatar-usage.md not present — figma-extract-usage skill was not run"
    fix_action: "Run figma-extract-usage for Avatar to produce Do/Don't usage guidelines"
    blocks: [doc-rewrite usage section, docusaurus usage page]
    dependency: []

  - id: GAP-002
    dimension: source_completeness
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: ~
      location: "Avatar/ directory"
      finding: "Avatar-pui.md not present — pui-mcp-extract skill was not run"
    fix_action: "Run pui-mcp-extract for Avatar to capture Platform UI alignment notes"
    blocks: [doc-rewrite PUI section]
    dependency: []

  - id: GAP-003
    dimension: props
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Avatar/props.md"
      location: "AvatarSize values table, lines 61–67"
      finding: "Figma component set shows sizes xsmall/small/medium/large/xlarge only. props.md lists 2xsmall and 2xlarge as unconfirmed. Oxygen constraint docs reference userStatus available 'for sizes 2xsmall–2xlarge' — implying those sizes exist in code but are absent from Figma."
    fix_action: "Verify AvatarSize enum in @8x8/oxygen-avatar source code and confirm whether 2xsmall and 2xlarge are implemented; update AvatarSize table with confirmed values only"
    blocks: [doc-rewrite props, storybook size examples]
    dependency: []

  - id: GAP-004
    dimension: props
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Avatar/Avatar-figma.md"
      location: "Variant axes — Status row, line 97"
      finding: "Figma Status axis includes raw color names (Gray, Green, Purple, Red, Yellow) alongside semantic names (Available, Away, Busy…). props.md AvatarUserStatus section excludes these. It is unclear whether they are public API values or internal Figma atom tokens."
    fix_action: "Verify AvatarUserStatus enum in @8x8/oxygen-avatar source and remove or document the raw-color values (Gray, Green, Purple, Red, Yellow) accordingly"
    blocks: [doc-rewrite props, accessibility status guidance]
    dependency: []

  - id: GAP-005
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: "Avatar/props.md"
      location: "AvatarStack section, line 31"
      finding: "AvatarStack is listed as a package component but has no props documented. MCP returned no prop data for AvatarStack."
    fix_action: "Add note to props.md that AvatarStack props were unavailable from MCP; link to Storybook for current API"
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: tokens
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Avatar/tokens.md"
      location: "Status badge / presence ring tokens, lines 47–57"
      finding: "Tokens for statuses OnCall, DirectCall, DoNotDisturb, WorkingOffline, OnBreak are missing. These statuses appear in Figma variant axes but their specific token names were not returned by the MCP theme tokens endpoint."
    fix_action: "Query the UserStatus component token data or inspect the Figma file directly (Desktop Bridge) to find the missing 5 status tokens and add them to tokens.md"
    blocks: [doc-rewrite tokens, accessibility status guidance]
    dependency: [GAP-004]

  - id: GAP-007
    dimension: figma_spec
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Avatar/Avatar-figma.md"
      location: "Visual reference section, line 17"
      finding: "Screenshot placeholder says 'screenshot' — no actual URL. Figma get_screenshot succeeded and image was captured during extraction but the URL was not persisted to the file."
    fix_action: "Re-run get_screenshot and embed the returned image URL in Avatar-figma.md visual reference section"
    blocks: []
    dependency: []

  - id: GAP-008
    dimension: figma_spec
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Avatar/Avatar-figma.md"
      location: "Interaction states table, line 285"
      finding: "'pressed' state has no data — marker '<!-- NOT FOUND IN FIGMA RESPONSE -->'. No pressed variant exists in the Figma component set."
    fix_action: "Confirm with design team whether a pressed state is intended; if not, document explicitly as 'not designed' in interaction states"
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: figma_spec
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Avatar/Avatar-figma.md"
      location: "Anatomy — Non-user types, lines 70–74"
      finding: "Internal anatomy for non-User types (Room, Auto Attendant, Call Queue, Ring Group, Channel, SMS Group) was not extracted — only noted as simpler structures. No get_design_context was run on these variants."
    fix_action: "Run get_design_context on at least one non-User type variant to capture its internal layer structure"
    blocks: [doc-rewrite anatomy section]
    dependency: []

  - id: GAP-010
    dimension: figma_spec
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Avatar/Avatar-figma.md"
      location: "Gaps & conflicts, line 332"
      finding: "figma-console tools (figma_get_variables, figma_get_styles, figma_get_component_details) all failed due to Desktop Bridge being unavailable. Variable data was obtained from Oxygen MCP theme tokens instead — this may miss Figma-specific variable modes or overrides."
    fix_action: "Re-run extraction with Figma Desktop Bridge plugin open to obtain full figma_get_variables output and cross-check against MCP token data"
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: examples
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Avatar/examples.md"
      location: "Header note, lines 6–9"
      finding: "All examples are reconstructed — MCP get-component-examples returned 0 clean snippets. No verified, runnable examples sourced from the actual component library."
    fix_action: "Flag all examples in examples.md as 'unverified reconstruction'; verify each example against Storybook or live package before doc-rewrite"
    blocks: [doc-rewrite examples, storybook-generate]
    dependency: []

  - id: GAP-012
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: "Avatar/examples.md"
      location: "No imageProps example present"
      finding: "imageProps prop is documented in props.md but no example shows how to use it (e.g. adding loading='lazy' or a custom className to the img element)"
    fix_action: "Add an imageProps usage example to examples.md"
    blocks: []
    dependency: []

  - id: GAP-013
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Avatar/Avatar-figma.md"
      location: "Accessibility section, lines 309–311"
      finding: "No accessibility annotations found in Figma (ARIA role, screen-reader label, focus order). accessibility.md is inferred, not sourced from design."
    fix_action: "Request designer to add ARIA role and screen-reader label annotations to the Avatar Figma component"
    blocks: []
    dependency: []

  - id: GAP-014
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: "Avatar/accessibility.md"
      location: "WCAG checklist, line 99"
      finding: "1.1.1 check flags that src prop has no alt — but does not confirm whether the component internally renders an empty alt='' for decorative treatment or relies on imageProps. Needs code verification."
    fix_action: "Verify how @8x8/oxygen-avatar handles alt text for the img element internally; update WCAG 1.1.1 check accordingly"
    blocks: [doc-rewrite accessibility]
    dependency: []

  - id: GAP-015
    dimension: cross_file
    severity: minor
    type: CONFLICT
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: "Avatar/props.md"
      location: "showEditOverlay constraint, line 51 and prop constraints table line 101"
      finding: "props.md states showEditOverlay is available for sizes 'l–3xl'. Figma component set only defines sizes up to xlarge. There is no '3xl' size in Figma — this constraint text may reference an extended API not reflected in the design."
    fix_action: "Verify showEditOverlay size constraint in @8x8/oxygen-avatar source code; reconcile with Figma size set"
    blocks: []
    dependency: [GAP-003]

warnings:
  - id: WARN-001
    dimension: examples
    confidence: heuristic
    finding: "AvatarStack example uses children API (<Avatar> as children) but AvatarStack props are completely undocumented — the example may be wrong if AvatarStack uses a different data-driven API (e.g. items prop)"

  - id: WARN-002
    dimension: tokens
    confidence: heuristic
    finding: "avatarHover token value is identical in Light and Dark (#29292926). This may be intentional, but is unusual — worth confirming with design that the dark mode hover overlay is the same alpha gray."

  - id: WARN-003
    dimension: figma_spec
    confidence: heuristic
    finding: "Figma user-internal atom uses 'heading01' typography for initials on large size. It is not confirmed that the same typography token is used for smaller sizes (medium, small, xsmall) — different sizes may use different type styles."

  - id: WARN-004
    dimension: props
    confidence: heuristic
    finding: "The 'children' prop is listed as default: null in get-component-info but default: null with required: true — this is a contradiction in the MCP data. Required props should not have null defaults."
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
siblings:
  - "[[Avatar/props]]"
  - "[[Avatar/examples]]"
  - "[[Avatar/tokens]]"
  - "[[Avatar/accessibility]]"
  - "[[Avatar/Avatar-figma]]"
tags:
  - oxygen
  - component/Avatar
  - role/audit
  - stage/blocked
---

# Avatar — Documentation Audit

> **Rubric version:** 1.0 · **Audited:** 2026-05-11 (partial re-audit) · **Verdict:** NO

---

## Verdict

**NO — resolve 2 CONFLICTs before doc-rewrite**

Two confirmed data conflicts must be resolved by a human before automated doc generation:
1. `AvatarSize` enum boundaries (`2xsmall`, `2xlarge`) — present in Oxygen code constraints but absent from Figma
2. `AvatarUserStatus` raw color values (`Gray`, `Green`, `Purple`, `Red`, `Yellow`) — present in Figma but not confirmed as public API

Once those are resolved, the remaining blockers are source gaps solvable by running the missing extract skills.

---

## File inventory

| File | Status | Produced by |
|------|--------|-------------|
| `Avatar/props.md` | ✅ Present | oxygen-mcp-extract |
| `Avatar/examples.md` | ✅ Present | oxygen-mcp-extract |
| `Avatar/tokens.md` | ✅ Present | oxygen-mcp-extract |
| `Avatar/accessibility.md` | ✅ Present | oxygen-mcp-extract |
| `Avatar/Avatar-figma.md` | ✅ Present | figma-extract |
| `Avatar/Avatar-usage.md` | ✅ Present (editorial) | usage-advisor → promoted 2026-05-11; replace with figma-extract-usage when Figma examples page exists |
| `Avatar/Avatar-pui.md` | ❌ Missing | pui-mcp-extract |

---

## Dimension scores

| Dimension | Score | Coverage | Confidence |
|-----------|-------|----------|------------|
| Source completeness | 0.86 | 6/7 | deterministic |
| Props | 0.79 | 11/14 | deterministic |
| Tokens | 0.77 | 10/13 | deterministic |
| Figma spec | 0.88 | 14/16 | deterministic |
| Examples | 0.80 | 8/10 | **heuristic** |
| Accessibility | 0.89 | 8/9 | mixed |
| Usage | 0.75 | 7 pairs (editorial) | **heuristic** |
| Cross-file consistency | 0.90 | 9/10 | mixed |

---

## Gap summary

| Count | Category |
|-------|----------|
| 2 | CONFLICTs (blocking) |
| 1 | SOURCE_GAPSs — major (missing extract run: Avatar-pui.md) |
| 7 | SOURCE_GAPSs — minor |
| 4 | DOC_GAPSs (auto-fixable or minor) |
| 4 | WARNINGs (heuristic) |
| 1 | RESOLVED — GAP-001 (Avatar-usage.md authored editorially 2026-05-11) |

---

## CONFLICTs — must resolve manually

### GAP-003 · AvatarSize enum mismatch · major · CONFLICT

Figma defines sizes `xsmall / small / medium / large / xlarge`. The Oxygen API docs reference sizes `2xsmall` and `2xlarge` in constraint text (userStatus constraint, showEditOverlay constraint) but these are absent from Figma.

**Evidence:** `Avatar/props.md` lines 61–67 (AvatarSize table); `Avatar/Avatar-figma.md` line 85 (Variant axes)

**Fix:** Check `AvatarSize` TypeScript enum in `@8x8/oxygen-avatar` source and confirm the full value set. Update both `props.md` and `Avatar-figma.md`.

---

### GAP-004 · AvatarUserStatus raw color values · major · CONFLICT

Figma `Status` axis includes `Gray, Green, Purple, Red, Yellow` alongside semantic values. These are absent from the documented `AvatarUserStatus` enum. It is unknown whether they are public API values or internal Figma design tokens.

**Evidence:** `Avatar/Avatar-figma.md` line 97 (Status axis); `Avatar/props.md` lines 76–81 (AvatarUserStatus)

**Fix:** Check `AvatarUserStatus` TypeScript type in `@8x8/oxygen-avatar` source. Remove or document the raw-color values.

---

## Major gaps

### ~~GAP-001 · Avatar-usage.md missing · SOURCE_GAP~~ — RESOLVED 2026-05-11

`Avatar-usage.md` authored editorially using `usage-advisor` — 7 Do/Don't pairs grounded in
`props.md`, `examples.md`, `accessibility.md`, and `Avatar-figma.md`. Source type: editorial.
Replace with `figma-extract-usage` output when a Figma `↳ Avatar examples` page is created.

---

### GAP-002 · Avatar-pui.md missing · SOURCE_GAP

`pui-mcp-extract` was not run. Platform UI alignment notes are absent.

**Fix:** Run `pui-mcp-extract` for Avatar.

---

### GAP-006 · 5 status tokens missing · DOC_GAP

Tokens for `OnCall`, `DirectCall`, `DoNotDisturb`, `WorkingOffline`, `OnBreak` were not returned by the Oxygen MCP theme tokens endpoint. These statuses appear in Figma.

**Fix:** Extract token data from UserStatus component or Figma Desktop Bridge. Add to `tokens.md`.

---

### GAP-011 · All examples are reconstructed · SOURCE_GAP

MCP returned 0 clean code snippets. Every example in `examples.md` was hand-written from prop definitions. None are verified against the live component.

**Fix:** Verify each example in `examples.md` against Storybook before doc-rewrite.

---

## Minor gaps

| ID | Dimension | Type | Finding |
|----|-----------|------|---------|
| GAP-005 | Props | DOC_GAP | AvatarStack has no documented props |
| GAP-007 | Figma spec | SOURCE_GAP | Screenshot URL not persisted to Avatar-figma.md |
| GAP-008 | Figma spec | SOURCE_GAP | Pressed state not in Figma — needs design confirmation |
| GAP-009 | Figma spec | SOURCE_GAP | Non-User type anatomy not extracted (Room, Auto Attendant, etc.) |
| GAP-010 | Figma spec | DOC_GAP | figma-console unavailable during extraction — variable data from MCP only |
| GAP-012 | Examples | DOC_GAP | No `imageProps` usage example |
| GAP-013 | Accessibility | SOURCE_GAP | No ARIA annotations in Figma — a11y.md is inferred |
| GAP-014 | Accessibility | DOC_GAP | alt text handling not verified in component source |
| GAP-015 | Cross-file | CONFLICT (minor) | `showEditOverlay` references size `3xl` — not a Figma size |

---

## Warnings (heuristic — advisory only)

| ID | Finding |
|----|---------|
| WARN-001 | AvatarStack example may use wrong API (children vs data prop) — unverifiable without source |
| WARN-002 | `avatarHover` token is identical in Light and Dark — confirm intentional with design |
| WARN-003 | Initials typography (`heading01`) confirmed only for `large` size — may differ on smaller sizes |
| WARN-004 | `children` prop in MCP data has `required: true` with `default: null` — contradiction in source data |

---

## Suggested next actions

1. **Resolve GAP-003** — check `AvatarSize` enum in `@8x8/oxygen-avatar` TypeScript source
2. **Resolve GAP-004** — check `AvatarUserStatus` enum in `@8x8/oxygen-avatar` TypeScript source
3. ~~**Run `figma-extract-usage`**~~ — GAP-001 resolved; `Avatar-usage.md` authored editorially (7 pairs). Replace with `figma-extract-usage` when a Figma examples page is created.
4. **Run `pui-mcp-extract`** — produces `Avatar-pui.md` (GAP-002)
5. **Verify examples** against Storybook (GAP-011)
6. After conflicts resolved and source gaps closed → run `doc-rewrite`

---

_Audit produced by doc-audit skill · Rubric version 1.0 · 2026-04-28_
