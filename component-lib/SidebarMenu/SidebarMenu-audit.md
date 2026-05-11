---
component: SidebarMenu
package: "@8x8/oxygen-sidebar-menu"
rubric_version: "1.0"
audit_date: "2026-05-07"
verdict: "NO"
verdict_reason: "One CONFLICT (GAP-009) must be resolved before doc-rewrite can proceed."

dimensions:
  props:
    score: 0.78
    coverage: "7/9"
    notes: "Sidebar and MenuItem fully documented from MCP. SubMenuItem, CollapseItem, SidebarContainer documented from examples only — no MCP prop types. icon prop on MenuItem informally noted."
  examples:
    score: 0.75
    coverage: "6/8"
    notes: "Config-driven and declarative patterns both present. Missing: direct <Sidebar items={...} /> rendering, router integration (linkComponent/linkProp), collapsed state example, dark mode example."
  tokens:
    score: 0.57
    coverage: "4/7"
    notes: "4 OX semantic tokens documented. Figma-discovered primitive tokens (text colors, badge color, border color) not surfaced to tokens.md."
  accessibility:
    score: 0.86
    coverage: "6/7"
    notes: "ARIA roles, keyboard table, screen reader guidance, WCAG checklist all present. Arrow key behavior undefined. All content inferred — no MCP a11y data."
  figma:
    score: 0.78
    coverage: "7/9"
    notes: "Two component sets documented. Variant axes, booleans, spacing, tokens fully resolved. Missing: design intent annotations, _Menu List Items / Expanded atom internals."
  usage:
    score: 0.0
    coverage: "0/1"
    notes: "SidebarMenu-usage.md not present. figma-extract-usage not run. SOURCE_GAP."
  pui:
    score: 1.0
    coverage: "N/A"
    notes: "PUI MCP confirmed no Platform UI package for sidebarMenu. Not applicable — PASS."

gaps:
  - id: GAP-001
    dimension: props
    severity: minor
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: props.md
      location: "SubMenuItem props table"
      finding: "`link` prop present in `SidebarItemProps` interface (props.md line 66) but absent from the SubMenuItem props table (lines 103–110). SubMenuItem receives sub-items from the same interface."
    fix_action: "Add `link` prop (type: `string`, optional) to the SubMenuItem props table in props.md."
    blocks: []
    dependency: []

  - id: GAP-002
    dimension: props
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: props.md
      location: "MenuItem props table, line 83"
      finding: "`icon` prop documented as 'not formally typed in MCP; observed in examples'. MCP returns no type definition for this prop."
    fix_action: "Update @8x8/oxygen-sidebar-menu MCP source to formally type the `icon: ReactNode` prop on MenuItem."
    blocks: []
    dependency: []

  - id: GAP-003
    dimension: tokens
    severity: major
    type: DOC_GAP
    confidence: deterministic
    auto_fixable: true
    evidence:
      source_file: SidebarMenu-figma.md
      location: "Token coverage table, lines 143–149"
      finding: "Figma extraction resolved 3 additional primitive tokens not present in tokens.md: `color/offWhite/offWhite02` (primary text, #26253A), `color/offWhite/offWhite05` (secondary text, #6C6861), `color/turqouise/turqouise05` (badge fill, #04828A). Border uses `color/offWhite/offWhite09` (same as hover12 primitive)."
    fix_action: "Add a 'Typography and badge tokens' section to tokens.md listing the 3 Figma-sourced primitive tokens with their roles and hex values."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-004
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "Pattern 1 section"
      finding: "Pattern 1 shows the state-management hook and item config array, but does not show the actual `<Sidebar items={sidebarItems} />` rendered JSX. A reader cannot tell what component to render."
    fix_action: "Add a minimal `<Sidebar>` render example showing items prop, collapseLabel, expandLabel wired up."
    blocks: []
    dependency: []

  - id: GAP-005
    dimension: examples
    severity: minor
    type: DOC_GAP
    confidence: heuristic
    auto_fixable: true
    evidence:
      source_file: examples.md
      location: "No router integration section"
      finding: "props.md documents `linkComponent` and `linkProp` on both `Sidebar` and `MenuItem` but no example shows router integration (e.g. React Router `<Link to={...}>`)."
    fix_action: "Add a router integration example showing `linkComponent={Link} linkProp='to'` on the Sidebar or MenuItem."
    blocks: []
    dependency: []

  - id: GAP-006
    dimension: accessibility
    severity: minor
    type: SOURCE_GAP
    confidence: heuristic
    auto_fixable: false
    evidence:
      source_file: accessibility.md
      location: "Keyboard interaction table, line 29"
      finding: "Arrow key behavior documented as 'Not documented by MCP; confirm whether sub-menu expansion uses arrow navigation.' No upstream source (MCP or Figma) clarifies this."
    fix_action: "Test keyboard behaviour in @8x8/oxygen-sidebar-menu and update accessibility.md with confirmed arrow key handling."
    blocks: []
    dependency: []

  - id: GAP-007
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: SidebarMenu-figma.md
      location: "Design decisions & annotations section, line 292"
      finding: "No design intent annotations on either component set. `annotations: []` returned by Desktop Bridge plugin for both nodes."
    fix_action: "Add inline Figma annotations to 'Sidebar menu' and 'Sidebar menu - Sublist item' component sets explaining key design decisions."
    blocks: []
    dependency: []

  - id: GAP-008
    dimension: usage
    severity: major
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: "(file absent)"
      location: "component-lib/SidebarMenu/SidebarMenu-usage.md"
      finding: "figma-extract-usage was not run. No Do/Don't editorial guidance file exists."
    fix_action: "Run /figma-extract-usage SidebarMenu to check for a 'Sidebar menu — Examples' page in Figma and extract usage guidance."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-009
    dimension: figma
    severity: major
    type: CONFLICT
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: SidebarMenu-figma.md
      location: "Gaps & conflicts table, line 322; props.md lines 41–55"
      finding: "Figma models collapse as a `collapsed?` boolean variant axis on the component set. The React API splits this across two components: `Sidebar` (manages collapse internally via `initialCollapsedState`/`onCollapseChange`) and `SidebarContainer` (accepts `collapsed` as a controlled prop). The Figma variant maps cleanly to `SidebarContainer.collapsed` but there is no direct equivalent on `<Sidebar>`. Spec must clarify which React API surface the Figma variant should be documented against."
    fix_action: "Human decision required: confirm whether the spec should document `collapsed?` as a `SidebarContainer` prop (controlled) or as `Sidebar.initialCollapsedState` (uncontrolled initial value). Update figma.md API table accordingly before rewrite."
    blocks: [doc-rewrite]
    dependency: []

  - id: GAP-010
    dimension: figma
    severity: minor
    type: SOURCE_GAP
    confidence: deterministic
    auto_fixable: false
    evidence:
      source_file: SidebarMenu-figma.md
      location: "Anatomy section, line 44"
      finding: "`_Menu List Items / Expanded` atom is the core nav item in both Primary and Secondary navigation, but its internal layer tree (icon slot, label, hover/active states) was not drilled. Its component properties are partially documented from the Secondary Navigation instance."
    fix_action: "Run figma_get_component_for_development on the atom's own node ID (componentId: 62897:19254) to extract its internal structure."
    blocks: []
    dependency: []

warnings:
  - id: WARN-001
    dimension: accessibility
    confidence: heuristic
    finding: "All ARIA roles in accessibility.md are inferred from component type, not verified from MCP or Figma annotations. `<nav>` landmark and `aria-current='page'` recommendations are not confirmed from source."
    advisory: "Verify rendered HTML in a browser to confirm actual ARIA output before publishing."

  - id: WARN-002
    dimension: tokens
    confidence: heuristic
    finding: "tokens.md notes that additional tokens may exist under names other than 'sidebar' (e.g. 'menu', 'nav'). The MCP search was not exhaustive."
    advisory: "Re-run get-theme-tokens with queries 'menu' and 'nav' to confirm no additional tokens are missed."

  - id: WARN-003
    dimension: props
    confidence: heuristic
    finding: "SubMenuItem, CollapseItem, and SidebarContainer props are documented from examples only. Actual prop types may differ from observed usage."
    advisory: "These 3 components return errors from get-component-props — flagged upstream as SOURCE_GAP-002. Advisory only."
# --- navigation (added by component-map) ---
role: audit
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
siblings:
  - "[[SidebarMenu/props]]"
  - "[[SidebarMenu/examples]]"
  - "[[SidebarMenu/tokens]]"
  - "[[SidebarMenu/accessibility]]"
  - "[[SidebarMenu/SidebarMenu-figma]]"
tags:
  - oxygen
  - component/SidebarMenu
  - role/audit
  - stage/blocked
  - category/navigation

---

# SidebarMenu — Documentation Audit

> **Verdict: NO** — One CONFLICT (GAP-009) must be resolved before `doc-rewrite` can proceed.
>
> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [SidebarMenu-figma.md](SidebarMenu-figma.md)

---

## File inventory

| File | Status | Notes |
|------|--------|-------|
| `props.md` | ✅ Present | |
| `examples.md` | ✅ Present | |
| `tokens.md` | ✅ Present | |
| `accessibility.md` | ✅ Present | |
| `SidebarMenu-figma.md` | ✅ Present | |
| `figma-screenshot-SidebarMenu.png` | ✅ Present | |
| `SidebarMenu-usage.md` | ❌ Missing | SOURCE_GAP → GAP-008 |
| `SidebarMenu-pui.md` | N/A | No PUI package confirmed via PUI MCP — PASS |

---

## Dimension scores

| Dimension | Score | Coverage | Status |
|-----------|-------|----------|--------|
| Props | 0.78 | 7/9 | Minor gaps |
| Examples | 0.75 | 6/8 | Minor gaps |
| Tokens | 0.57 | 4/7 | Major gap (GAP-003) |
| Accessibility | 0.86 | 6/7 | Minor gap |
| Figma | 0.78 | 7/9 | **CONFLICT** (GAP-009) + minor gaps |
| Usage | 0.00 | 0/1 | Major SOURCE_GAP (GAP-008) |
| PUI | N/A | N/A | PASS — not applicable |

---

## Gaps

### CONFLICT — must resolve before rewrite

#### GAP-009 · figma · major · CONFLICT · deterministic

**Finding:** Figma models `collapsed?` as a boolean variant axis. The React API splits this across two components: `<Sidebar>` (uncontrolled, `initialCollapsedState`) and `<SidebarContainer collapsed={...}>` (controlled). The spec must declare which surface the Figma variant documents.

**Fix:** Human decision — confirm whether the spec documents the controlled (`SidebarContainer.collapsed`) or uncontrolled (`Sidebar.initialCollapsedState`) API, then update `SidebarMenu-figma.md` API table.

---

### Major gaps

#### GAP-003 · tokens · major · DOC_GAP · deterministic · auto-fixable

**Finding:** Figma extraction resolved 3 primitive tokens not in `tokens.md`: primary text color (`color/offWhite/offWhite02`, `#26253A`), secondary text color (`color/offWhite/offWhite05`, `#6C6861`), badge fill (`color/turqouise/turqouise05`, `#04828A`). Border uses `color/offWhite/offWhite09` (same primitive as `hover12`).

**Fix:** Add a typography and badge tokens section to `tokens.md`.

---

#### GAP-008 · usage · major · SOURCE_GAP · deterministic

**Finding:** `SidebarMenu-usage.md` absent. `figma-extract-usage` not run.

**Fix:** Run `/figma-extract-usage SidebarMenu` to check for a Figma Examples page.

---

### Minor gaps

#### GAP-001 · props · minor · DOC_GAP · deterministic · auto-fixable

**Finding:** `link` prop present in `SidebarItemProps` (props.md line 66) but missing from the `SubMenuItem` props table.

**Fix:** Add `link?: string` to `SubMenuItem` props table.

---

#### GAP-002 · props · minor · SOURCE_GAP · deterministic

**Finding:** `icon` prop on `MenuItem` not formally typed in MCP — documented as observed-from-examples.

**Fix:** Update MCP source to formally type `icon: ReactNode` on `MenuItem`.

---

#### GAP-004 · examples · minor · DOC_GAP · heuristic · auto-fixable

**Finding:** Pattern 1 shows the hook and config array but never renders `<Sidebar items={...} />`.

**Fix:** Add a minimal `<Sidebar>` JSX render snippet.

---

#### GAP-005 · examples · minor · DOC_GAP · heuristic · auto-fixable

**Finding:** `linkComponent`/`linkProp` documented in props but no usage example shown.

**Fix:** Add a React Router integration example.

---

#### GAP-006 · accessibility · minor · SOURCE_GAP · heuristic

**Finding:** Arrow key behaviour for sub-menu expansion is undocumented — noted as unconfirmed in accessibility.md.

**Fix:** Test keyboard behaviour in the component and update `accessibility.md`.

---

#### GAP-007 · figma · minor · SOURCE_GAP · deterministic

**Finding:** No design intent annotations on either Figma component set.

**Fix:** Designer adds annotations to Figma; re-run `figma-extract`.

---

#### GAP-010 · figma · minor · SOURCE_GAP · deterministic

**Finding:** `_Menu List Items / Expanded` atom internals not extracted.

**Fix:** Run `figma_get_component_for_development` on node `62897:19254`.

---

## Warnings (heuristic, advisory only)

**WARN-001** — All ARIA roles are inferred, not verified from rendered HTML.

**WARN-002** — Token search may be incomplete; re-run with queries `"menu"` and `"nav"`.

**WARN-003** — SubMenuItem, CollapseItem, SidebarContainer props sourced from examples only; actual types unconfirmed.

---

## Suggested next actions

1. **Resolve GAP-009** (CONFLICT): decide whether `collapsed?` maps to `SidebarContainer.collapsed` or `Sidebar.initialCollapsedState` — update `SidebarMenu-figma.md`
2. **Fix GAP-003** (auto-fixable): add primitive token section to `tokens.md`
3. **Run** `/figma-extract-usage SidebarMenu` → clears GAP-008
4. Once conflict + blockers resolved, run `/doc-rewrite SidebarMenu`

_Audit produced by doc-audit skill · rubric v1.0 · 2026-05-07_
