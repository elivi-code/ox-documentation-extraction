---
rubric_version: 1.0
component: PopoverMenu
package: "@8x8/oxygen-popover"
extracted: 2026-05-08
audited: 2026-05-08
verdict: NO
verdict_reason: "3 CONFLICTs require human resolution before doc-rewrite can proceed"

files:
  present:
    - props.md
    - examples.md
    - tokens.md
    - accessibility.md
    - PopoverMenu-figma.md
    - PopoverMenu-usage.md
  absent:
    - PopoverMenu-pui.md  # confirmed N/A — PUI MCP search returned 0 results for "popover" and "PopoverMenu"; no application-layer concerns

dimensions:
  props:
    score: 0.62
    coverage: "17/26 props fully described across Popover + PopoverMenu; 6 props have empty MCP descriptions; sub-component props absent"
  examples:
    score: 0.40
    coverage: "1/4 examples MCP-sourced; 3 inferred from props API; naming conflict in MCP story unresolved"
  tokens:
    score: 0.35
    coverage: "0 tokens from Oxygen MCP; figma.md has 13 token bindings with light/dark values; no semantic descriptions or collection names"
  accessibility:
    score: 0.50
    coverage: "full structure present but entirely inferred; 0 MCP-sourced or Figma-annotated a11y data; one contrast conflict unverified"
  figma:
    score: 0.72
    coverage: "anatomy, variant axes, token bindings, spacing complete; screenshot file absent; footer padding conflict; component not published"
  usage:
    score: 0.50
    coverage: "prose guidelines present (When to Use / When Not to Use / Best Practices); 0 Do/Don't card pairs"
  pui:
    score: 1.0
    coverage: "N/A confirmed — no PUI context"

summary:
  doc_gaps: 8
  source_gaps: 14
  conflicts: 3
  warnings: 2

gaps:

  # ─── CONFLICTS (human decision required) ───────────────────────────────────

  - id: GAP-001
    dimension: examples
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "lines 9–24, Basic PopoverMenu example note"
      finding: >
        The only MCP-sourced story (Popover.documentation.stories.tsx) renders
        the example using `<Popover items={...}>`, but the `items` prop belongs
        exclusively to `PopoverMenu`. `Popover` uses `floatingContent`/`isOpen`/
        `setIsOpen`. Either the story has a bug (wrong component name) or there
        is an undocumented API alias. doc-rewrite cannot emit a correct import
        and usage snippet until this is resolved.
    fix_action: "Inspect Popover.documentation.stories.tsx source to determine whether <Popover items={...}> is a valid alias or a story authoring error; update examples.md accordingly"
    blocks: [docusaurus, storybook]
    dependency: []

  - id: GAP-002
    dimension: tokens
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: PopoverMenu-figma.md
      location: "Structure & spacing / Internal spacing table, line 212"
      finding: >
        Footer button row padding differs between light mode (`padding: 8px 8px 0 8px`)
        and dark mode (`padding: 8px 12px 0 12px`). These are two variants of the
        same component property rendered from the same Figma frame; the discrepancy
        is in the Figma source. The intended value is unknown — a designer must
        confirm whether this is intentional or a Figma authoring error.
    fix_action: "Ask designer to confirm intended footer button padding for dark mode; fix Figma source if error, or document the intentional difference"
    blocks: [docusaurus]
    dependency: []

  - id: GAP-003
    dimension: accessibility
    severity: major
    type: CONFLICT
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: PopoverMenu-figma.md
      location: "Color & token bindings / Footer table, line 175"
      finding: >
        `--text/textcolor09` resolves to `black` in dark mode on an
        `--actions/action09` (`#4687ed`) Apply button background. Black (#000000)
        on #4687ed yields approximately 3.4:1 contrast — below the WCAG 2.1 AA
        minimum of 4.5:1 for normal text. This may be a token misassignment or
        an intentional design choice with a known workaround. Cannot be auto-fixed.
    fix_action: "Verify contrast ratio of --text/textcolor09 (black) on --actions/action09 (#4687ed) in dark mode; if failing, identify the correct text token or update the Figma source"
    blocks: [docusaurus]
    dependency: []

  # ─── SOURCE GAPS (upstream Figma / MCP work needed) ────────────────────────

  - id: GAP-004
    dimension: props
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "Sub-components section, line 83"
      finding: >
        `Divider`, `SectionHeader`, and `ListItem` (from the popover package) are
        registered in the Oxygen MCP search index but their props are not accessible
        via `get-component-props` (returns 404). `ListItemWrapperProps` — the type
        used in PopoverMenu's `items` prop — is also undocumented.
    fix_action: "Request Oxygen MCP team to register Divider, SectionHeader, and ListItemWrapperProps props for the popover package"
    blocks: [docusaurus, storybook]
    dependency: []

  - id: GAP-005
    dimension: tokens
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: tokens.md
      location: "Theme tokens section, line 7"
      finding: >
        Oxygen MCP `get-theme-tokens` returns 0 matches for "popover".
        All design tokens used by this component (`--ui/*`, `--text/*`,
        `--actions/*`, `--typography/*`) reside in the UI-Foundations library
        (file key `iVY5nI8JAxM05Apnnvozzs`), not in the UI-components file.
        Token names and resolved values are captured in PopoverMenu-figma.md
        but semantic descriptions and collection names are absent.
    fix_action: "Extract token semantic descriptions from UI-Foundations library using figma_execute + getVariableByIdAsync for the token IDs referenced in the Popover window design context"
    blocks: [docusaurus]
    dependency: []

  - id: GAP-006
    dimension: accessibility
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "ARIA roles table, line 13 — note"
      finding: >
        No accessibility data is returned by the Oxygen MCP for Popover or
        PopoverMenu. The Figma file contains no a11y annotations. All ARIA
        roles, keyboard interactions, and focus management guidance in
        accessibility.md is inferred from the ARIA APG Menu Button pattern —
        not verified against the actual implementation.
    fix_action: "Verify ARIA roles, keyboard behavior, and focus management via DOM inspection of the rendered PopoverMenu component in a running application"
    blocks: [docusaurus]
    dependency: []

  - id: GAP-007
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: PopoverMenu-usage.md
      location: "Gaps section, line 64"
      finding: >
        The `↳ Popover examples` Figma page exists and was found, but it contains
        only prose text guidelines — no `✅ Do —` or `❌ Don't —` card frames
        have been authored. The usage.md captures the prose content but 0 Do/Don't
        pairs are available.
    fix_action: "Ask designer to author Do/Don't card frames on the ↳ Popover examples Figma page; re-run figma-extract-usage after cards are added"
    blocks: [docusaurus]
    dependency: []

  - id: GAP-008
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: PopoverMenu-figma.md
      location: "Visual reference section, line 17"
      finding: >
        `figma-screenshot-PopoverMenu.png` was not saved to disk. The screenshot
        was captured visually via `Figma:get_screenshot` during extraction but
        the raw image data could not be written to a file (figma-console Desktop
        Bridge was disconnected at the time). The screenshot is missing from the
        component folder.
    fix_action: "Re-run figma-extract for PopoverMenu with Desktop Bridge connected to save figma-screenshot-PopoverMenu.png"
    blocks: []
    dependency: []

  - id: GAP-009
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: PopoverMenu-figma.md
      location: "Gaps & conflicts section, line 274"
      finding: >
        The Popover canvas is not published as a named library component in Figma.
        `figma_get_component_details` returns "Component not found: PopoverMenu".
        The full variant key map is therefore unavailable.
    fix_action: "No action required unless the Oxygen team publishes the component; note as known limitation"
    blocks: []
    dependency: []

  - id: GAP-010
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: PopoverMenu-figma.md
      location: "Accessibility section, lines 255–257"
      finding: "Figma contains no ARIA role, focus order, or keyboard interaction annotations on the Popover/PopoverMenu frames."
    fix_action: "Ask designer to add a11y annotations to the Popover window Figma frame"
    blocks: []
    dependency: []

  - id: GAP-011
    dimension: tokens
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: PopoverMenu-figma.md
      location: "Token coverage section, lines 119–128"
      finding: >
        Multiple dimension and spacing values are hardcoded in Figma with no
        token binding: border-radius (6px), container width (320px), max-height
        (400px), max-width (1064px), all padding values, and Scrollbar_Mac OS
        colors (#c1c1c1, #fafafa).
    fix_action: "Flag to Oxygen design team to tokenise border-radius, container dimensions, and spacing values; document in tokens.md once tokens exist"
    blocks: []
    dependency: []

  - id: GAP-012
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "ARIA roles table, line 14"
      finding: >
        The ARIA role of the floating panel is listed as `menu` or `dialog`
        (uncertain). PopoverMenu wraps a list structure suggesting `role="menu"`,
        but the low-level `Popover` primitive accepts arbitrary `floatingContent`
        and may use `role="dialog"`. This distinction affects keyboard interaction
        semantics. Unverified.
    fix_action: "Confirm via DOM inspection whether PopoverMenu renders role=menu and Popover renders role=dialog (or another role)"
    blocks: []
    dependency: [GAP-006]

  # ─── DOC GAPS (auto-fixable by doc-rewrite once source gaps / conflicts resolved) ─

  - id: GAP-013
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Popover props table, lines 41–42"
      finding: "`activeProp` and `disabledProp` props have no descriptions in the MCP source. These are present in both Popover and PopoverMenu prop lists but their purpose is undocumented."
    fix_action: "Add inferred descriptions: activeProp — 'Name of the prop on the child element used to set active state'; disabledProp — 'Name of the prop on the child element used to set disabled state'"
    blocks: []
    dependency: []

  - id: GAP-014
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Popover props table, line 45"
      finding: "`placement` prop type is listed as `Placement` with no expansion of valid values."
    fix_action: "Add Placement type values: 'top' | 'top-start' | 'top-end' | 'bottom' | 'bottom-start' | 'bottom-end' | 'left' | 'left-start' | 'left-end' | 'right' | 'right-start' | 'right-end' (standard floating-ui placement values — verify against implementation)"
    blocks: []
    dependency: []

  - id: GAP-015
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "Installation section, lines 7–11"
      finding: "Package version is absent from the installation snippet. The MCP returned null for yarn/npm/package installation fields."
    fix_action: "Add package version to install command (e.g. @8x8/oxygen-popover@<version>) — retrieve from package registry or components-to-extract.md version reference"
    blocks: []
    dependency: []

  - id: GAP-016
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "Lines 29–48, Low-level Popover example"
      finding: "The controlled Popover example (isOpen/setIsOpen/floatingContent) is inferred from the props API, not sourced from an MCP example. It is marked with a data gap note."
    fix_action: "Retain example but remove the inference note once GAP-001 (API naming conflict) is resolved and the Popover vs PopoverMenu boundary is confirmed"
    blocks: []
    dependency: [GAP-001]

  - id: GAP-017
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "Lines 79–98, With header and footer example"
      finding: "Header/footer example is inferred from prop types, not from an MCP story. Marked with a data gap note."
    fix_action: "Retain example; remove inference note once correct prop API is confirmed (dependent on GAP-001 resolution)"
    blocks: []
    dependency: [GAP-001]

  - id: GAP-018
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: examples.md
      location: "All examples"
      finding: >
        No examples demonstrate: placement variants, disabled items via
        activeProp/disabledProp, destructive list items, checkbox/radio list
        items, section headers, sub-menu items, or loading/empty states.
        These require ListItemWrapperProps documentation (GAP-004) first.
    fix_action: "Add examples for list item types once ListItemWrapperProps is documented (GAP-004)"
    blocks: []
    dependency: [GAP-004, GAP-001]

  - id: GAP-019
    dimension: tokens
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: tokens.md
      location: "Entire file"
      finding: >
        tokens.md contains no token table — only a prose explanation of the
        SOURCE_GAP. The token names and resolved values exist in
        PopoverMenu-figma.md (Color & token bindings section) but have not
        been promoted into tokens.md.
    fix_action: "Promote the 13 token bindings from PopoverMenu-figma.md into a structured table in tokens.md"
    blocks: []
    dependency: [GAP-005]

  - id: GAP-020
    dimension: accessibility
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: accessibility.md
      location: "Footer, line 70"
      finding: "All a11y content is explicitly flagged as inferred. The inference note should be retained but linked to the verification gap (GAP-006) so readers know it is advisory."
    fix_action: "Add a prominent advisory banner at the top of accessibility.md linking to GAP-006 verification requirement"
    blocks: []
    dependency: []

# ─── WARNINGS (heuristic — advisory only) ──────────────────────────────────

warnings:

  - id: WARN-001
    dimension: props
    confidence: heuristic
    finding: >
      `PopoverMenu` exposes `onUpdate(arg0: ListItemWrapperProps, arg1: number)`
      but the semantics of `arg1` (likely an index) are not described. If this
      fires on every render it could cause performance issues; if it fires only
      on user-initiated state changes the name is misleading. Worth clarifying.
    advisory: "Clarify onUpdate callback semantics in props.md"

  - id: WARN-002
    dimension: figma
    confidence: heuristic
    finding: >
      The Figma `↳ Popover examples` page has an additional section "Tooltip and
      Popover working together" (frame 88806:12915) showing combined usage patterns.
      This content was not extracted into any documentation file — it may be
      valuable for the usage.md or examples.md.
    advisory: "Consider extracting the 'Tooltip and Popover working together' section from the Figma examples page into examples.md or usage.md"
---

# PopoverMenu — Audit Report

> **Verdict: NO** — 3 conflicts require human resolution before `doc-rewrite` can run.
>
> Resolve GAP-001, GAP-002, and GAP-003 first, then re-run this audit.

**Audited:** 2026-05-08 · **Rubric:** v1.0 · **Package:** `@8x8/oxygen-popover`

---

## File inventory

| File | Status | Notes |
|------|--------|-------|
| `props.md` | ✅ Present | Both Popover (11 props) and PopoverMenu (15 props) |
| `examples.md` | ✅ Present | 1 MCP-sourced + 3 inferred examples |
| `tokens.md` | ✅ Present | No token table — SOURCE_GAP prose only |
| `accessibility.md` | ✅ Present | Full structure, entirely inferred |
| `PopoverMenu-figma.md` | ✅ Present | Anatomy, variants, tokens, spacing complete |
| `PopoverMenu-usage.md` | ✅ Present | Prose guidelines only; 0 Do/Don't cards |
| `PopoverMenu-pui.md` | ⬜ Absent | **Confirmed N/A** — PUI search returned 0 results |

---

## Dimension scores

| Dimension | Score | Coverage summary |
|-----------|-------|-----------------|
| Props | 0.62 | 17/26 props fully described; 6 empty descriptions; sub-component props absent |
| Examples | 0.40 | 1/4 MCP-sourced; naming conflict blocks rewrite |
| Tokens | 0.35 | 0 MCP tokens; 13 bindings in figma.md; no table in tokens.md |
| Accessibility | 0.50 | Full structure inferred; 0 verified data; 1 contrast conflict |
| Figma | 0.72 | Anatomy + tokens + spacing complete; screenshot missing; footer conflict |
| Usage | 0.50 | Prose guidelines present; 0 Do/Don't pairs |
| PUI | N/A | Confirmed no application-layer concerns |

---

## Conflicts — must resolve before rewrite

### GAP-001 · CONFLICT · Examples · major

**Finding:** The sole MCP story (`Popover.documentation.stories.tsx`) renders the example as `<Popover items={...}>`, but `items` is a `PopoverMenu`-only prop. `Popover` uses `floatingContent`/`isOpen`/`setIsOpen`. The component name in the story is either wrong or an undocumented alias exists.

**Fix:** Inspect `Popover.documentation.stories.tsx` to confirm whether `<Popover items={...}>` is valid. Update `examples.md` accordingly.

---

### GAP-002 · CONFLICT · Tokens · major

**Finding:** Footer button row padding differs between light (`8px 8px 0 8px`) and dark (`8px 12px 0 12px`) in Figma. Origin of the discrepancy unknown — may be intentional or a Figma authoring error.

**Fix:** Ask designer to confirm intended dark-mode footer padding; fix Figma source or document the difference as intentional.

---

### GAP-003 · CONFLICT · Accessibility · major

**Finding:** `--text/textcolor09` resolves to `black` in dark mode on `--actions/action09` (`#4687ed`) — estimated contrast ~3.4:1, below WCAG AA (4.5:1). May be a token misassignment.

**Fix:** Calculate exact contrast ratio; if failing, identify the correct text token for dark mode Apply button or update the Figma source.

---

## Source gaps — upstream work needed

| ID | Dimension | Severity | Finding |
|----|-----------|----------|---------|
| GAP-004 | Props | major | `Divider`, `SectionHeader`, `ListItemWrapperProps` props unregistered in Oxygen MCP |
| GAP-005 | Tokens | major | Oxygen MCP returns 0 tokens; all tokens are in UI-Foundations library |
| GAP-006 | Accessibility | major | All a11y content inferred; 0 MCP/Figma-sourced data |
| GAP-007 | Usage | major | 0 Do/Don't cards in Figma examples page |
| GAP-008 | Figma | minor | `figma-screenshot-PopoverMenu.png` not saved to disk |
| GAP-009 | Figma | minor | Component not published; no variant key map |
| GAP-010 | Figma | minor | No a11y annotations in Figma |
| GAP-011 | Tokens | minor | border-radius, dimensions, padding hardcoded — no tokens |
| GAP-012 | Accessibility | minor | ARIA role of floating panel unconfirmed (menu vs dialog) |

---

## Doc gaps — auto-fixable by doc-rewrite

| ID | Dimension | Finding |
|----|-----------|---------|
| GAP-013 | Props | `activeProp`, `disabledProp` have no descriptions |
| GAP-014 | Props | `Placement` type not expanded to valid values |
| GAP-015 | Props | Package version absent from install command |
| GAP-016 | Examples | Controlled Popover example flagged as inferred |
| GAP-017 | Examples | Header/footer example flagged as inferred |
| GAP-018 | Examples | No examples for list item types (blocks on GAP-004) |
| GAP-019 | Tokens | Token bindings in figma.md not promoted to tokens.md table |
| GAP-020 | Accessibility | Inference advisory banner missing from accessibility.md |

---

## Warnings (advisory)

**WARN-001 · Props:** `onUpdate` callback's second argument (`arg1: number`) has no description — semantics (index? count?) unclear.

**WARN-002 · Figma:** "Tooltip and Popover working together" section exists in the Figma examples page (frame 88806:12915) but was not extracted into any documentation file.

---

## Suggested next actions

1. **Resolve GAP-001** — confirm story API naming (is `<Popover items={...}>` valid?)
2. **Resolve GAP-002** — confirm intended footer padding in dark mode with designer
3. **Resolve GAP-003** — verify contrast ratio of Apply button in dark mode
4. **Re-run doc-audit** after all 3 conflicts are resolved
5. Once verdict flips to PARTIAL or YES, run **doc-rewrite** — it can auto-fix GAP-013 through GAP-020

---

_Source: doc-audit skill v1.0 · Audited 2026-05-08_
