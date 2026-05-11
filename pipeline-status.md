---
title: "OX Pipeline Status"
description: "Quick-reference status table — pipeline stage, audit verdict, and blocker for every component"
role: pipeline_status
workspace: OX Documentation Extraction
last_updated: 2026-05-08
tags:
  - oxygen
  - navigation
  - pipeline
---
# OX Pipeline Status

> **Quick reference for AI and humans.** Load this file for instant orientation; open `component-map.yaml` for full detail.
> Last updated: 2026-05-08

## Summary

| Stage | Count |
|-------|-------|
| ✅ SPEC COMPLETE | 1 |
| 🟢 SPEC READY | 14 |
| 🔴 BLOCKED | 19 |
| 🟡 EXTRACTED | 3 |
| **Total** | **37** |

---

## ✅ SPEC COMPLETE
*Canonical spec.md written — pipeline done*

| Component | Category | Verdict | Score | Blocker / Note |
|-----------|----------|---------|-------|----------------|
| [[component-lib/Tabs/Tabs|Tabs]] | layout overlay | 🟢 YES | 0.68 | Zero CONFLICTs. Token dimension substantially improved on re-audit 2026-... |

---

## 🟢 SPEC READY
*Audit verdict YES/PARTIAL — run doc-rewrite*

| Component | Category | Verdict | Score | Blocker / Note |
|-----------|----------|---------|-------|----------------|
| [[component-lib/Accordion/Accordion|Accordion]] | layout overlay | 🟢 YES | 0.73 | All core files present. No CONFLICTs. Usage and PUI SOURCE_GAPs are non-... |
| [[component-lib/Breadcrumbs/Breadcrumbs|Breadcrumbs]] | navigation | 🟢 YES | 0.62 | Zero CONFLICTs. Token dimension re-scored 0.25→0.55 after re-audit. Zero... |
| [[component-lib/Card/Card|Card]] | layout overlay | 🟢 YES | — | Deprecated package. Zero CONFLICTs. Deprecation banner documented. Rewri... |
| [[component-lib/Checkbox/Checkbox|Checkbox]] | form inputs | 🟢 YES | 0.68 | Zero CONFLICTs. Token SOURCE_GAPs from prior audit resolved. doc-rewrite... |
| [[component-lib/DateTimeRangeSelector/DateTimeRangeSelector|DateTimeRangeSelector]] | date time | 🟢 YES | 0.59 | Zero CONFLICTs and zero blocker-severity gaps. All 6 expected files pres... |
| [[component-lib/DateTimeSelector/DateTimeSelector|DateTimeSelector]] | date time | 🟢 YES | 0.55 | GAP-004 CONFLICT resolved (2026-05-08) — Option B confirmed: shared trig... |
| [[component-lib/Modal/Modal|Modal]] | layout overlay | 🟢 YES | 0.72 | All core files present, including PUI (confirmed no relevant context). Z... |
| [[component-lib/Pagination/Pagination|Pagination]] | navigation | 🟢 YES | 0.77 | Zero CONFLICTs. Token hex values confirmed 2026-05-05. doc-rewrite can p... |
| [[component-lib/ProgressBar/ProgressBar|ProgressBar]] | feedback status | 🟢 YES | 0.66 | Zero CONFLICTs. Pre-labelled conflicts in figma.md reclassified as DOC_G... |
| [[component-lib/SlideOut/SlideOut|SlideOut]] | layout overlay | 🟡 PARTIAL | — | Figma design confirmed non-existent (SOURCE_GAP blocker). No CONFLICTs. ... |
| [[component-lib/Slider/Slider|Slider]] | form inputs | 🟡 PARTIAL | — | One blocker SOURCE_GAP (slider-figma.md absent). No CONFLICTs. Rewrite c... |
| [[component-lib/Tag/Tag|Tag]] | data display | 🟢 YES | 0.70 | Zero CONFLICTs. All required files present. doc-rewrite can proceed. |
| [[component-lib/TextField/TextField|TextField]] | form inputs | 🟢 YES | 0.68 | No CONFLICTs. No blockers. figma.md uses non-standard name (naming viola... |
| [[component-lib/Toast/Toast|Toast]] | feedback status | 🟢 YES | — | All core files present. Token coverage strong. PUI confirmed no relevant... |

---

## 🔴 BLOCKED
*Audit verdict NO — CONFLICTs must be resolved first*

| Component | Category | Verdict | Score | Blocker / Note |
|-----------|----------|---------|-------|----------------|
| [[component-lib/AlertBanner/AlertBanner|AlertBanner]] | feedback status | 🔴 NO | 0.51 | 2 CONFLICTs — Figma exposes mode and breakpoint variant axes not present... |
| [[component-lib/Avatar/Avatar|Avatar]] | data display | 🔴 NO | — | 2 CONFLICTs — require human verification before doc-rewrite can proceed. |
| [[component-lib/Button/Button|Button]] | interaction | 🔴 NO | — | 3 CONFLICTs — Secondary rest bg token ($action01 vs action02); Text butt... |
| [[component-lib/Calendar/Calendar|Calendar]] | date time | 🔴 NO | 0.63 | One CONFLICT (GAP-011) requires human decision before doc-rewrite can pr... |
| [[component-lib/DataTable/DataTable|DataTable]] | data display | 🔴 NO | — | 2 CONFLICTs — Pagination props interface: (limit/offset/totalResults) vs... |
| [[component-lib/Input/Input|Input]] | form inputs | 🔴 NO | 0.70 | 1 CONFLICT — Search input isReadOnly discrepancy between Figma and MCP |
| [[component-lib/Label/Label|Label]] | data display | 🔴 NO | — | 2 CONFLICTs — token names/sizes diverge (MCP label01 12px vs Figma body0... |
| [[component-lib/Link/Link|Link]] | navigation | 🔴 NO | 0.67 | 2 CONFLICTs — standalone/size type mismatch (MCP vs Figma); hover token ... |
| [[component-lib/List/List|List]] | data display | 🔴 NO | — | 1 CONFLICT — token ui01 described as selected state in tokens.md but Fig... |
| [[component-lib/PopoverMenu/PopoverMenu|PopoverMenu]] | overlays contextual | 🔴 NO | — | 3 CONFLICTs require human resolution before doc-rewrite can proceed. |
| [[component-lib/Select/Select|Select]] | form inputs | 🔴 NO | 0.53 | 2 CONFLICTs — isAsync type mismatch between MCP endpoints; forwardedRef ... |
| [[component-lib/SidebarMenu/SidebarMenu|SidebarMenu]] | navigation | 🔴 NO | — | One CONFLICT (GAP-009) must be resolved before doc-rewrite can proceed. |
| [[component-lib/SkeletonBlock/SkeletonBlock|SkeletonBlock]] | feedback status | 🔴 NO | 0.56 | 1 CONFLICT — SkeletonCircle size values documented in two incompatible f... |
| [[component-lib/SkeletonCircle/SkeletonCircle|SkeletonCircle]] | feedback status | 🔴 NO | 0.56 | 1 CONFLICT — size values documented in incompatible formats vs SkeletonB... |
| [[component-lib/Spinner/Spinner|Spinner]] | feedback status | 🔴 NO | 0.61 | 2 CONFLICTs — Figma isInverted axis has no React prop (design-only vs AP... |
| [[component-lib/TextArea/TextArea|TextArea]] | form inputs | 🔴 NO | — | 3 CONFLICTs — Size/Mode/Filled Figma axes have no direct prop counterparts |
| [[component-lib/TimeSelector/TimeSelector|TimeSelector]] | date time | 🔴 NO | — | 2 unresolved CONFLICTs — Size=Large variant existence and default size m... |
| [[component-lib/ToggleButton/ToggleButton|ToggleButton]] | form inputs | 🔴 NO | 0.73 | 2 CONFLICTs — Figma isOn? vs OX isChecked prop name; Figma ToggleGroup i... |
| [[component-lib/Tooltip/Tooltip|Tooltip]] | overlays contextual | 🔴 NO | — | 2 CONFLICTs — character limit 140 (MCP) vs 136 (Figma); orientation defa... |

---

## 🟡 EXTRACTED
*Core files present — audit not yet run*

| Component | Category | Verdict | Score | Blocker / Note |
|-----------|----------|---------|-------|----------------|
| [[component-lib/Badge/Badge|Badge]] | data display | — — | — | No audit run yet. PUI file present. No Figma file. |
| [[component-lib/Radio/Radio|Radio]] | form inputs | — — | — | No audit run yet. No Figma or PUI files extracted. |
| [[component-lib/Toaster/Toaster|Toaster]] | feedback status | — — | — | Imperative API only — no props/examples/tokens extraction. Shares Toast'... |

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
