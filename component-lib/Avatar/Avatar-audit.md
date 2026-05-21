---
rubric_version: 1.0
component: Avatar
audited: 2026-05-21
verdict: "YES"
verdict_reason: "All CONFLICTs resolved 2026-05-21; Avatar-pui.md now present; no blocker gaps remain. doc-rewrite has already produced the hub + 7 spokes."
audit_note: "Re-audit after editorial resolution of GAP-003/004/015 and pui-mcp-extract run for GAP-002. Hub and spokes already exist; this audit confirms the spec is consumable. Two major gaps (GAP-006 missing status tokens, GAP-011 reconstructed examples) remain as documented limitations but do not block rewrite — they have visible markers in the spokes."

files_found:
  - Avatar/source/props.md
  - Avatar/source/examples.md
  - Avatar/source/tokens.md
  - Avatar/source/accessibility.md
  - Avatar/source/Avatar-figma.md
  - Avatar/source/Avatar-usage.md
  - Avatar/source/Avatar-pui.md

files_missing: []

dimension_scores:
  source_completeness: { score: 1.00, coverage: "7/7" }
  props:               { score: 1.00, coverage: "14/14" }
  tokens:              { score: 0.77, coverage: "10/13" }
  figma_spec:          { score: 0.88, coverage: "14/16" }
  examples:            { score: 0.90, coverage: "9/10", confidence: heuristic }
  accessibility:       { score: 0.89, coverage: "8/9" }
  usage:               { score: 0.75, coverage: "7 pairs (editorial)", confidence: heuristic }
  cross_file:          { score: 1.00, coverage: "10/10" }
  platform_ui:         { score: 1.00, coverage: "1 hook, 1 event, 1 MFE" }

totals:
  doc_gaps: 3
  source_gaps: 5
  conflicts: 0
  warnings: 5
  resolved_since_last_audit: 5

resolved:
  - id: GAP-001
    note: "Avatar-usage.md authored editorially 2026-05-11"
  - id: GAP-002
    note: "Avatar-pui.md produced 2026-05-21 via pui-mcp-extract — useUserDetails hook + shell-userDetails event"
  - id: GAP-003
    note: "Editorial resolution 2026-05-21 — AvatarSize fixed to 5 named values (xsmall|small|medium|large|xlarge). Oxygen README stale phrasings flagged for upstream fix."
  - id: GAP-004
    note: "Resolved 2026-05-21 — Gray/Green/Purple/Red/Yellow confirmed as internal Figma atom variants only, not public AvatarUserStatus values."
  - id: GAP-005
    note: "Applied 2026-05-21 — AvatarStack 'see Storybook' note added to props.md."
  - id: GAP-012
    note: "Applied 2026-05-21 — imageProps usage example added to examples.md."
  - id: GAP-015
    note: "Editorial resolution 2026-05-21 — showEditOverlay applies to large and xlarge only. README 'l–3xl' phrasing flagged for upstream fix."

gaps:
  - id: GAP-006
    dimension: tokens
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Avatar/source/tokens.md"
      location: "Status badge / presence ring tokens, lines 65–79"
      finding: "Tokens for statuses OnCall, DirectCall, DoNotDisturb, WorkingOffline, OnBreak are missing. These statuses appear in Figma variant axes but their specific token names were not returned by the MCP theme tokens endpoint."
    fix_action: "Query UserStatus component token data or inspect the Figma file directly (Desktop Bridge) to find the 5 missing status tokens and add them to tokens.md"
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: figma_spec
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Avatar/source/Avatar-figma.md"
      location: "Visual reference, line 39"
      finding: "Local PNG screenshot embedded (figma-screenshot-avatar.png), but Figma cloud URL not persisted. Re-extract should embed the signed Figma URL alongside the local copy."
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
      source_file: "Avatar/source/Avatar-figma.md"
      location: "Interaction states table, line 307"
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
      source_file: "Avatar/source/Avatar-figma.md"
      location: "Anatomy — Non-user types, lines 92–96"
      finding: "Internal anatomy for non-User types (Room, Auto Attendant, Call Queue, Ring Group, Channel, SMS Group) was not extracted — only noted as simpler structures. No get_design_context was run on these variants."
    fix_action: "Run get_design_context on at least one non-User type variant to capture its internal layer structure"
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: figma_spec
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Avatar/source/Avatar-figma.md"
      location: "Gaps & conflicts, line 353"
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
      source_file: "Avatar/source/examples.md"
      location: "Header note, lines 29–31"
      finding: "All examples are reconstructed — MCP get-component-examples returned 0 clean snippets. The file header explicitly flags this; the imageProps example added 2026-05-21 (GAP-012 fix) is also unverified."
    fix_action: "Verify each example in examples.md against Storybook or the live package before consuming this spec for code generation"
    blocks: [storybook-generate]
    dependency: []

  - id: GAP-013
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "Avatar/source/Avatar-figma.md"
      location: "Accessibility section, lines 329–335"
      finding: "No accessibility annotations found in Figma (ARIA role, screen-reader label, focus order). accessibility.md is inferred, not sourced from design."
    fix_action: "Request designer to add ARIA role and screen-reader label annotations to the Avatar Figma component"
    blocks: []
    dependency: []

  - id: GAP-014
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: "Avatar/source/accessibility.md"
      location: "WCAG 2.1 AA checklist, line 121"
      finding: "1.1.1 check flags that src prop has no alt — but does not confirm whether the component internally renders an empty alt='' for decorative treatment or relies on imageProps. Needs code verification."
    fix_action: "Verify how @8x8/oxygen-avatar handles alt text for the img element internally; update WCAG 1.1.1 check accordingly"
    blocks: []
    dependency: []

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
    finding: "The 'children' prop is listed as default: null with required: true in get-component-info — this is a contradiction in the MCP data. Required props should not have null defaults."

  - id: WARN-005
    dimension: props
    confidence: deterministic
    finding: "Oxygen README contains stale boilerplate size-range phrasings on userStatus ('2xsmall–2xlarge') and showEditOverlay ('l–3xl') constraints. These do not match the public Sizes table (5 sizes only) or the Figma component set. Flag for upstream Oxygen README fix."

# --- navigation (added by component-map) ---
role: audit
pipeline_stage: rewritten
pipeline_note: "Audit verdict YES — doc-rewrite already executed 2026-05-21; hub + 7 spokes present at top level"
siblings:
  - "[[Avatar/source/props]]"
  - "[[Avatar/source/examples]]"
  - "[[Avatar/source/tokens]]"
  - "[[Avatar/source/accessibility]]"
  - "[[Avatar/source/Avatar-figma]]"
  - "[[Avatar/source/Avatar-usage]]"
  - "[[Avatar/source/Avatar-pui]]"
  - "[[Avatar/Avatar]]"
tags:
  - oxygen
  - component/Avatar
  - role/audit
  - stage/rewritten
---

# Avatar — Documentation Audit (re-run)

> **Rubric version:** 1.0 · **Audited:** 2026-05-21 · **Verdict:** YES

---

## Verdict

**YES — spec is consumable for downstream generators.**

All previously-blocking issues are resolved:
- The 3 CONFLICTs (`AvatarSize` enum, `AvatarUserStatus` raw colours, `showEditOverlay` size constraint) were resolved 2026-05-21 — `AvatarSize` is the 5 named sizes, the raw colour values are Figma-internal, and the README's `l`–`3xl` phrasing is upstream stale boilerplate.
- The major SOURCE_GAP (missing `Avatar-pui.md`) was closed 2026-05-21 by running `pui-mcp-extract`.

The hub + 7 spokes were written by `doc-rewrite` 2026-05-21 and have already absorbed these fixes.

---

## File inventory

| File | Status | Produced by |
|------|--------|-------------|
| `Avatar/source/props.md` | ✅ Present | oxygen-mcp-extract |
| `Avatar/source/examples.md` | ✅ Present | oxygen-mcp-extract |
| `Avatar/source/tokens.md` | ✅ Present | oxygen-mcp-extract |
| `Avatar/source/accessibility.md` | ✅ Present | oxygen-mcp-extract |
| `Avatar/source/Avatar-figma.md` | ✅ Present | figma-extract |
| `Avatar/source/Avatar-usage.md` | ✅ Present (editorial) | usage-advisor |
| `Avatar/source/Avatar-pui.md` | ✅ Present | pui-mcp-extract |

---

## Dimension scores

| Dimension | Score | Coverage | Δ since 2026-05-11 |
|---|---|---|---|
| Source completeness | 1.00 | 7/7 | +0.14 |
| Props | 1.00 | 14/14 | +0.21 |
| Tokens | 0.77 | 10/13 | 0 |
| Figma spec | 0.88 | 14/16 | 0 |
| Examples | 0.90 | 9/10 | +0.10 |
| Accessibility | 0.89 | 8/9 | 0 |
| Usage | 0.75 | 7 pairs (editorial) | 0 |
| Cross-file consistency | 1.00 | 10/10 | +0.10 |
| Platform UI | 1.00 | 1 hook, 1 event, 1 MFE | new |

---

## Resolved since previous audit

| ID | Resolution |
|---|---|
| GAP-001 | Avatar-usage.md authored editorially 2026-05-11 |
| GAP-002 | pui-mcp-extract run 2026-05-21 — useUserDetails hook + shell-userDetails event |
| GAP-003 | Editorial — AvatarSize = `xsmall \| small \| medium \| large \| xlarge` |
| GAP-004 | Raw colours confirmed as Figma-internal, not public API |
| GAP-005 | AvatarStack "see Storybook" note added to props.md |
| GAP-012 | imageProps usage example added to examples.md |
| GAP-015 | Editorial — showEditOverlay applies to `large` + `xlarge` only |

---

## Open items (non-blocking)

| ID | Severity | Type | Dimension | Summary |
|---|---|---|---|---|
| GAP-006 | major | DOC_GAP | tokens | 5 status tokens missing (OnCall, DirectCall, DoNotDisturb, WorkingOffline, OnBreak) |
| GAP-011 | major | SOURCE_GAP | examples | All examples reconstructed — flagged in file header |
| GAP-007 | minor | SOURCE_GAP | figma | Figma cloud URL not persisted (local PNG present) |
| GAP-008 | minor | SOURCE_GAP | figma | Pressed state not designed in Figma |
| GAP-009 | minor | SOURCE_GAP | figma | Non-User type anatomy not extracted |
| GAP-010 | minor | DOC_GAP | figma | Desktop Bridge unavailable during extraction |
| GAP-013 | minor | SOURCE_GAP | accessibility | No ARIA annotations in Figma |
| GAP-014 | minor | DOC_GAP | accessibility | alt handling not verified in component source |

---

## Warnings (heuristic — advisory only)

| ID | Finding |
|----|---------|
| WARN-001 | AvatarStack example may use wrong API (children vs data prop) — unverifiable without source |
| WARN-002 | `avatarHover` token identical in Light and Dark — confirm with design |
| WARN-003 | Initials typography (`heading01`) confirmed only for `large` size — may differ on smaller sizes |
| WARN-004 | `children` prop in MCP data has `required: true` with `default: null` — contradiction in source data |
| WARN-005 | Oxygen README has stale boilerplate size constraint text on `userStatus` and `showEditOverlay` — flag for upstream Oxygen team fix |

---

## Suggested next actions

1. ✅ doc-rewrite — already done 2026-05-21
2. Strike through Avatar in `components-to-extract.md` and bump the `Progress: N / 34` counter
3. (Optional) Resolve GAP-006 next time the Figma Desktop Bridge is open — closes the only remaining major DOC_GAP
4. (Optional) Verify the 9 reconstructed examples against Storybook to close GAP-011

---

_Audit produced by doc-audit skill · Rubric version 1.0 · 2026-05-21_
