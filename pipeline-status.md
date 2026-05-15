---
title: "OX Pipeline Status"
description: "Quick-reference status table — pipeline stage, audit verdict, and blocker for every component"
role: pipeline_status
workspace: OX Documentation Extraction
last_updated: 2026-05-15
tags:
  - oxygen
  - navigation
  - pipeline
---
# OX Pipeline Status

> **Quick reference for AI and humans.** Load this file for instant orientation; open `component-map.yaml` for full detail.
> Last updated: 2026-05-15

## Summary

| Stage | Count |
|-------|-------|
| ✅ SPEC COMPLETE | 1 |
| 🟢 SPEC READY | 17 |
| 🔴 BLOCKED | 18 |
| 🟡 EXTRACTED | 0 |
| ⬜ N/A — covered elsewhere | 1 |
| **Total** | **37** |

---

## ✅ SPEC COMPLETE
*Canonical spec.md written — pipeline done*

| Component | Category | Verdict | Score | Blocker / Note |
|-----------|----------|---------|-------|----------------|
| [[component-lib/Tabs/Tabs|Tabs]] | layout overlay | 🟢 YES | 0.68 | Zero CONFLICTs. Token dimension improved on re-audit 2026-05-05. Tabs-usage.md added editorially 2026-05-15 (Figma Do/Don't cards still pending). |

---

## 🟢 SPEC READY
*Audit verdict YES/PARTIAL — run doc-rewrite*

| Component | Category | Verdict | Score | Blocker / Note |
|-----------|----------|---------|-------|----------------|
| [[component-lib/Accordion/Accordion|Accordion]] | layout overlay | 🟢 YES | 0.73 | All core files present. No CONFLICTs. Usage and PUI SOURCE_GAPs are non-... |
| [[component-lib/Badge/Badge|Badge]] | data display | 🟡 PARTIAL | — | One blocker SOURCE_GAP (badge-figma.md absent — figma-extract not run). Zero CONFLICTs. Rewrite can proceed on props, examples, accessibility, usage_patterns. |
| [[component-lib/Breadcrumbs/Breadcrumbs|Breadcrumbs]] | navigation | 🟢 YES | 0.62 | Zero CONFLICTs. Token dimension re-scored 0.25→0.55 after re-audit. Zero... |
| [[component-lib/Card/Card|Card]] | layout overlay | 🟢 YES | — | Deprecated package. Zero CONFLICTs. Deprecation banner documented. Rewri... |
| [[component-lib/Checkbox/Checkbox|Checkbox]] | form inputs | 🟢 YES | 0.68 | Zero CONFLICTs. Token SOURCE_GAPs from prior audit resolved. doc-rewrite... |
| [[component-lib/DateTimeRangeSelector/DateTimeRangeSelector|DateTimeRangeSelector]] | date time | 🟢 YES | 0.59 | Zero CONFLICTs and zero blocker-severity gaps. All 6 expected files pres... |
| [[component-lib/DateTimeSelector/DateTimeSelector|DateTimeSelector]] | date time | 🟢 YES | 0.55 | GAP-004 CONFLICT resolved (2026-05-08) — Option B confirmed: shared trig... |
| [[component-lib/Modal/Modal|Modal]] | layout overlay | 🟢 YES | 0.72 | All core files present, including PUI (confirmed no relevant context). Z... |
| [[component-lib/Pagination/Pagination|Pagination]] | navigation | 🟢 YES | 0.77 | Zero CONFLICTs. Token hex values confirmed 2026-05-05. doc-rewrite can p... |
| [[component-lib/ProgressBar/ProgressBar|ProgressBar]] | feedback status | 🟢 YES | 0.75 | Re-audited 2026-05-14. Usage SOURCE_GAP closed editorially (5 grounded Do/Don't pairs, WARN-003); all 7 dimensions available... |
| [[component-lib/Radio/Radio|Radio]] | form inputs | 🟡 PARTIAL | 0.61 | Audited 2026-05-15. One blocker SOURCE_GAP (Radio-figma.md absent — figma-extract not yet run; nodes 51776:2800, 50606:93474 known). Zero CONFLICTs. Editorial Radio-usage.md mirrors public docs page (WARN-001). One `/figma-extract Radio` call promotes to YES. |
| [[component-lib/SlideOut/SlideOut|SlideOut]] | layout overlay | 🟡 PARTIAL | 0.36 | Re-audited 2026-05-15. Figma design confirmed non-existent (GAP-001 blocker). No CONFLICTs. Usage SOURCE_GAP closed editorially (7 grounded Do/Don't pairs via usage-advisor; WARN-002); mirrors PopoverMenu precedent. Verdict remains PARTIAL until upstream Figma exists. |
| [[component-lib/Slider/Slider|Slider]] | form inputs | 🟡 PARTIAL | — | One blocker SOURCE_GAP (slider-figma.md absent). No CONFLICTs. Editorial Slider-usage.md added 2026-05-15 (derivation-only — no Figma examples page; 6 Do/Don't pairs; +HTML render). Rewrite can proceed on extracted dimensions; figma-extract still owed. |
| [[component-lib/Tag/Tag|Tag]] | data display | 🟢 YES | 0.70 | Zero CONFLICTs. All required files present. doc-rewrite can proceed. |
| [[component-lib/TextField/TextField|TextField]] | form inputs | 🟢 YES | 0.78 | Re-audited 2026-05-15. Editorial TextField-usage.md added (6 Do/Don't pairs grounded in oxygen.8x8.com/components/textinput/usage + extracted artifacts; WARN-005). Usage dim 0.00 → 0.70. No CONFLICTs. figma.md naming violation persists (GAP-006). |
| [[component-lib/Toast/Toast|Toast]] | feedback status | 🟢 YES | 0.78 | Re-audited 2026-05-15. All 7 files now present (Toast-usage.md added editorially — no Figma examples page; GAP-003 resolved). InlineNotification Figma data enriched (all 10 variant colors confirmed). Zero CONFLICTs. doc-rewrite can proceed. |
| [[component-lib/Tooltip/Tooltip|Tooltip]] | overlays contextual | 🟡 PARTIAL | — | Re-audited 2026-05-15. Both blocker CONFLICTs reconciled against canonical published Oxygen docs (GAP-001 → 140 chars; GAP-002 → orientation default `top`). Five derived Do/Don't pairs added to Tooltip-usage.md (mitigates GAP-017; +HTML render). Zero CONFLICTs remaining. doc-rewrite can proceed. |

---

## 🔴 BLOCKED
*Audit verdict NO — CONFLICTs must be resolved first*

| Component | Category | Verdict | Score | Blocker / Note |
|-----------|----------|---------|-------|----------------|
| [[component-lib/AlertBanner/AlertBanner|AlertBanner]] | feedback status | 🔴 NO | 0.51 | 2 CONFLICTs — Figma exposes mode and breakpoint variant axes not present... |
| [[component-lib/Avatar/Avatar|Avatar]] | data display | 🔴 NO | — | 2 CONFLICTs — require human verification before doc-rewrite can proceed. |
| [[component-lib/Button/Button|Button]] | interaction | 🔴 NO | — | 3 CONFLICTs — Secondary rest bg token ($action01 vs action02); Text butt... |
| [[component-lib/Calendar/Calendar|Calendar]] | date time | 🔴 NO | 0.63 | One CONFLICT (GAP-011) requires human decision before doc-rewrite can pr... |
| [[component-lib/DataTable/DataTable|DataTable]] | data display | 🔴 NO | — | 2 CONFLICTs (Pagination interface GAP-001, cell type mapping GAP-002) block doc-rewrite. Usage doc added 2026-05-14 (editorial derivation-only — published Oxygen Table docs page is "In progress" placeholder; no Figma Do/Don't cards). |
| [[component-lib/Input/Input|Input]] | form inputs | 🔴 NO | 0.82 | 1 CONFLICT — Search input isReadOnly discrepancy. Editorial Input-usage.md added 2026-05-14 (mirrors published docs page; 8 Do/Don't pairs; +HTML render). |
| [[component-lib/Label/Label|Label]] | data display | 🔴 NO | — | 2 CONFLICTs — token names/sizes diverge (MCP label01 12px vs Figma body01 14px); information→infoBox prop mapping unverified. Editorial label-usage.md added 2026-05-14 (derivation-only — Oxygen docs page 404; 8 Do/Don't pairs; +HTML render). |
| [[component-lib/Link/Link|Link]] | navigation | 🔴 NO | 0.67 | 2 CONFLICTs — standalone/size type mismatch (MCP vs Figma); hover token ... |
| [[component-lib/List/List|List]] | data display | 🔴 NO | — | 1 CONFLICT — token ui01 described as selected state in tokens.md but Fig... |
| [[component-lib/PopoverMenu/PopoverMenu|PopoverMenu]] | overlays contextual | 🔴 NO | — | 3 CONFLICTs require human resolution before doc-rewrite can proceed. |
| [[component-lib/Select/Select|Select]] | form inputs | 🔴 NO | 0.53 | 2 CONFLICTs — isAsync type mismatch between MCP endpoints; forwardedRef ... |
| [[component-lib/SidebarMenu/SidebarMenu|SidebarMenu]] | navigation | 🔴 NO | — | One CONFLICT (GAP-009) must be resolved before doc-rewrite can proceed. |
| [[component-lib/SkeletonBlock/SkeletonBlock|SkeletonBlock]] | feedback status | 🔴 NO | 0.56 | 1 CONFLICT — SkeletonCircle size values documented in two incompatible formats. Editorial SkeletonBlock-usage.md added 2026-05-14 (derivation-only — no Figma examples page; 6 Do/Don't pairs; +HTML render). |
| [[component-lib/SkeletonCircle/SkeletonCircle|SkeletonCircle]] | feedback status | 🔴 NO | 0.56 | 1 CONFLICT — size values documented in incompatible formats vs SkeletonBlock docs. Editorial SkeletonCircle-usage.md added 2026-05-14 (derivation-only — no Figma examples page; 6 Do/Don't pairs; +HTML render). |
| [[component-lib/Spinner/Spinner|Spinner]] | feedback status | 🔴 NO | 0.61 | 2 CONFLICTs — Figma isInverted axis has no React prop (design-only vs AP... |
| [[component-lib/TextArea/TextArea|TextArea]] | form inputs | 🔴 NO | — | 3 CONFLICTs — Size/Mode/Filled Figma axes have no direct prop counterparts |
| [[component-lib/TimeSelector/TimeSelector|TimeSelector]] | date time | 🔴 NO | — | 2 unresolved CONFLICTs — Size=Large variant existence and default size mismatch between Figma and code API. Editorial timeselector-usage.md added 2026-05-15 (docs-mirrored from oxygen.8x8.com — no Figma examples page; 6 Do/Don't pairs). |
| [[component-lib/ToggleButton/ToggleButton|ToggleButton]] | form inputs | 🔴 NO | 0.73 | 2 CONFLICTs — Figma isOn? vs OX isChecked prop name; Figma ToggleGroup i... |

---

## 🟡 EXTRACTED
*Core files present — audit not yet run*

_(empty — all extracted components have been audited as of 2026-05-15)_

---

## ⬜ N/A — covered elsewhere
*No audit applicable — see referenced component for spec*

| Component | Category | Verdict | Score | Blocker / Note |
|-----------|----------|---------|-------|----------------|
| [[component-lib/Toaster/Toaster|Toaster]] | feedback status | ⬜ N/A | — | Imperative API only — no props/examples/tokens to extract. Visual design lives in [[component-lib/Toast/Toast\|Toast]]; spec is covered there. See [[component-lib/Toaster/toaster-note\|toaster-note.md]]. |

---

## Pipeline stages

| Stage | Meaning | Next action |
|-------|---------|-------------|
| ✅ spec_complete | `{component}-spec.md` written | Ship to Docusaurus / Storybook |
| 🟢 spec_ready | Audit verdict YES or PARTIAL | Run `/doc-rewrite {component}` |
| 🔴 blocked | Audit verdict NO — CONFLICTs present | Resolve conflicts in audit file, re-audit |
| 🟡 extracted | Core files present, no audit yet | Run `/doc-audit {component}` |
| ⬜ not_started | Nothing extracted yet | Run extract skills in parallel |

## File roles

| Role | Filename pattern | Description |
|------|-----------------|-------------|
| `props` | `props.md` | API props — types, defaults, descriptions |
| `examples` | `examples.md` | Code examples basic → advanced |
| `tokens` | `tokens.md` | Design token bindings |
| `accessibility` | `accessibility.md` | ARIA, keyboard, WCAG 2.1 AA |
| `figma` | `{component}-figma.md` | Anatomy, variants, spacing from Figma |
| `pui` | `{component}-pui.md` | Platform UI infra hooks (only where relevant) |
| `usage` | `{component}-usage.md` | Do/Don't guidelines from Figma examples page |
| `audit` | `{component}-audit.md` | Gap report — scores, CONFLICTs, verdict |
| `spec` | `{component}-spec.md` | Final canonical spec (doc-rewrite output) |
