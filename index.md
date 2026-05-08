# OX Design System — Documentation Index

> All 37 Oxygen components, organized by category. Each file link opens the doc directly in Obsidian.
> **Map:** [[component-map]]  ·  **Status:** [[pipeline-status]]  ·  **Progress:** [[components-to-extract]]

**Stage:** ✅ spec complete · 🟢 spec ready · 🔴 blocked · 🟡 extracted · ⬜ not started

**Files:** 📐 props · 💡 examples · 🎨 tokens · ♿ accessibility · 🖼 figma · 🔧 pui · 📖 usage · 🔍 audit · 📋 spec

---

## Form Inputs

### 🟢 [[component-lib/Checkbox/Checkbox|Checkbox]]
`@8x8/oxygen-checkbox` `0.68`

**Audit:** 🟢 YES — Zero CONFLICTs. Token SOURCE_GAPs from prior audit resolved. doc-rewrite can proceed.

**Files:** 📐 [[Checkbox/props|props]] · 💡 [[Checkbox/examples|examples]] · 🎨 [[Checkbox/tokens|tokens]] · ♿ [[Checkbox/accessibility|accessibility]] · 🖼 [[Checkbox/checkbox-figma|figma]] · 🔧 [[Checkbox/checkbox-pui|pui]] · 🔍 [[Checkbox/checkbox-audit|audit]]
**Missing:** `checkbox-usage.md`

### 🔴 [[component-lib/Input/Input|Input]]
`@8x8/oxygen-input` `0.70`

**Audit:** 🔴 NO — 1 CONFLICT — Search input isReadOnly discrepancy between Figma and MCP

**Files:** 📐 [[Input/props|props]] · 💡 [[Input/examples|examples]] · 🎨 [[Input/tokens|tokens]] · ♿ [[Input/accessibility|accessibility]] · 🖼 [[Input/Input-figma|figma]] · 🔧 [[Input/Input-pui|pui]] · 🔍 [[Input/Input-audit|audit]]
**Missing:** `Input-usage.md`

### 🟡 [[component-lib/Radio/Radio|Radio]]
`@8x8/oxygen-radio`

**Files:** 📐 [[Radio/props|props]] · 💡 [[Radio/examples|examples]] · 🎨 [[Radio/tokens|tokens]] · ♿ [[Radio/accessibility|accessibility]]
**Missing:** `radio-figma.md`, `radio-usage.md`, `radio-pui.md`, `radio-audit.md`

### 🔴 [[component-lib/Select/Select|Select]]
`@8x8/oxygen-select` `0.53`

**Audit:** 🔴 NO — 2 CONFLICTs — isAsync type mismatch between MCP endpoints; forwardedRef vs ref pattern unclear. Also: select-figma.md missing (blocker SOURCE_GAP).

**Files:** 📐 [[Select/props|props]] · 💡 [[Select/examples|examples]] · 🎨 [[Select/tokens|tokens]] · ♿ [[Select/accessibility|accessibility]] · 🔧 [[Select/select-pui|pui]] · 🔍 [[Select/Select-audit|audit]]
**Missing:** `select-figma.md`, `select-usage.md`

### 🟢 [[component-lib/Slider/Slider|Slider]]
`@8x8/oxygen-slider`

**Audit:** 🟡 PARTIAL — One blocker SOURCE_GAP (slider-figma.md absent). No CONFLICTs. Rewrite can proceed on props, examples, tokens, accessibility, pui dimensions.

**Files:** 📐 [[Slider/props|props]] · 💡 [[Slider/examples|examples]] · 🎨 [[Slider/tokens|tokens]] · ♿ [[Slider/accessibility|accessibility]] · 🔧 [[Slider/slider-pui|pui]] · 🔍 [[Slider/slider-audit|audit]]
**Missing:** `slider-figma.md`, `slider-usage.md`

### 🔴 [[component-lib/TextArea/TextArea|TextArea]]
`@8x8/oxygen-textarea`

**Audit:** 🔴 NO — 3 CONFLICTs — Size/Mode/Filled Figma axes have no direct prop counterparts

**Files:** 📐 [[TextArea/props|props]] · 💡 [[TextArea/examples|examples]] · 🎨 [[TextArea/tokens|tokens]] · ♿ [[TextArea/accessibility|accessibility]] · 🖼 [[TextArea/textarea-figma|figma]] · 🔧 [[TextArea/textarea-pui|pui]] · 🔍 [[TextArea/textarea-audit|audit]]
**Missing:** `textarea-usage.md`

### 🟢 [[component-lib/TextField/TextField|TextField]]
`@8x8/oxygen-textField` `0.68`

**Audit:** 🟢 YES — No CONFLICTs. No blockers. figma.md uses non-standard name (naming violation only).

**Files:** 📐 [[TextField/props|props]] · 💡 [[TextField/examples|examples]] · 🎨 [[TextField/tokens|tokens]] · ♿ [[TextField/accessibility|accessibility]] · 🖼 [[TextField/figma|figma]] · 🔧 [[TextField/TextField-pui|pui]] · 🔍 [[TextField/TextField-audit|audit]]
**Missing:** `TextField-usage.md`

### 🔴 [[component-lib/ToggleButton/ToggleButton|ToggleButton]]
`@8x8/oxygen-toggleButton` `0.73`

**Audit:** 🔴 NO — 2 CONFLICTs — Figma isOn? vs OX isChecked prop name; Figma ToggleGroup isError variant has no OX API counterpart.

**Files:** 📐 [[ToggleButton/props|props]] · 💡 [[ToggleButton/examples|examples]] · 🎨 [[ToggleButton/tokens|tokens]] · ♿ [[ToggleButton/accessibility|accessibility]] · 🖼 [[ToggleButton/ToggleButton-figma|figma]] · 🔧 [[ToggleButton/ToggleButton-pui|pui]] · 🔍 [[ToggleButton/ToggleButton-audit|audit]]
**Missing:** `ToggleButton-usage.md`

---

## Interaction

### 🔴 [[component-lib/Button/Button|Button]]
`@8x8/oxygen-button`

**Audit:** 🔴 NO — 3 CONFLICTs — Secondary rest bg token ($action01 vs action02); Text button active bg ($active17 scope); Primary bg token naming (action09 vs action01) between Figma and tokens.md.

**Files:** 📐 [[Button/props|props]] · 💡 [[Button/examples|examples]] · 🎨 [[Button/tokens|tokens]] · ♿ [[Button/accessibility|accessibility]] · 🖼 [[Button/Button-figma|figma]] · 🔍 [[Button/Button-audit|audit]]
**Missing:** `Button-usage.md`, `Button-pui.md`

---

## Layout & Overlay

### 🟢 [[component-lib/Accordion/Accordion|Accordion]]
`@8x8/oxygen-accordion` `0.73`

**Audit:** 🟢 YES — All core files present. No CONFLICTs. Usage and PUI SOURCE_GAPs are non-blocking.

**Files:** 📐 [[Accordion/props|props]] · 💡 [[Accordion/examples|examples]] · 🎨 [[Accordion/tokens|tokens]] · ♿ [[Accordion/accessibility|accessibility]] · 🖼 [[Accordion/accordion-figma|figma]] · 🔍 [[Accordion/accordion-audit|audit]]
**Missing:** `accordion-usage.md`, `accordion-pui.md`

### 🟢 [[component-lib/Card/Card|Card]] ~~deprecated~~
`@8x8/oxygen-card`

**Audit:** 🟢 YES — Deprecated package. Zero CONFLICTs. Deprecation banner documented. Rewrite can proceed.

**Files:** 📐 [[Card/props|props]] · 💡 [[Card/examples|examples]] · 🎨 [[Card/tokens|tokens]] · ♿ [[Card/accessibility|accessibility]] · 🖼 [[Card/Card-figma|figma]] · 🔍 [[Card/Card-audit|audit]]
**Missing:** `Card-usage.md`, `Card-pui.md`

### 🟢 [[component-lib/Modal/Modal|Modal]]
`@8x8/oxygen-modal` `0.72`

**Audit:** 🟢 YES — All core files present, including PUI (confirmed no relevant context). Zero CONFLICTs. Usage SOURCE_GAP is non-blocking.

**Files:** 📐 [[Modal/props|props]] · 💡 [[Modal/examples|examples]] · 🎨 [[Modal/tokens|tokens]] · ♿ [[Modal/accessibility|accessibility]] · 🖼 [[Modal/Modal-figma|figma]] · 🔧 [[Modal/Modal-pui|pui]] · 🔍 [[Modal/Modal-audit|audit]]
**Missing:** `Modal-usage.md`

### 🟢 [[component-lib/SlideOut/SlideOut|SlideOut]]
`@8x8/oxygen-slide-out`

**Audit:** 🟡 PARTIAL — Figma design confirmed non-existent (SOURCE_GAP blocker). No CONFLICTs. Rewrite can proceed on available dimensions.

**Files:** 📐 [[SlideOut/props|props]] · 💡 [[SlideOut/examples|examples]] · 🎨 [[SlideOut/tokens|tokens]] · ♿ [[SlideOut/accessibility|accessibility]] · 🔍 [[SlideOut/SlideOut-audit|audit]]
**Missing:** `SlideOut-figma.md`, `SlideOut-usage.md`, `SlideOut-pui.md`

### ✅ [[component-lib/Tabs/Tabs|Tabs]]
`@8x8/oxygen-tabs` `0.68`

**Audit:** 🟢 YES — Zero CONFLICTs. Token dimension substantially improved on re-audit 2026-05-05. Spec written.

**Files:** 📐 [[Tabs/props|props]] · 💡 [[Tabs/examples|examples]] · 🎨 [[Tabs/tokens|tokens]] · ♿ [[Tabs/accessibility|accessibility]] · 🖼 [[Tabs/Tabs-figma|figma]] · 🔧 [[Tabs/Tabs-pui|pui]] · 🔍 [[Tabs/Tabs-audit|audit]] · 📋 [[Tabs/Tabs-spec|spec]]
**Missing:** `Tabs-usage.md`

---

## Navigation

### 🟢 [[component-lib/Breadcrumbs/Breadcrumbs|Breadcrumbs]]
`@8x8/oxygen-breadcrumbs` `0.62`

**Audit:** 🟢 YES — Zero CONFLICTs. Token dimension re-scored 0.25→0.55 after re-audit. Zero blockers.

**Files:** 📐 [[Breadcrumbs/props|props]] · 💡 [[Breadcrumbs/examples|examples]] · 🎨 [[Breadcrumbs/tokens|tokens]] · ♿ [[Breadcrumbs/accessibility|accessibility]] · 🖼 [[Breadcrumbs/Breadcrumbs-figma|figma]] · 🔧 [[Breadcrumbs/Breadcrumbs-pui|pui]] · 🔍 [[Breadcrumbs/Breadcrumbs-audit|audit]]
**Missing:** `Breadcrumbs-usage.md`

### 🔴 [[component-lib/Link/Link|Link]]
`@8x8/oxygen-link` `0.67`

**Audit:** 🔴 NO — 2 CONFLICTs — standalone/size type mismatch (MCP vs Figma); hover token identity conflict (MCP search vs Figma design context).

**Files:** 📐 [[Link/props|props]] · 💡 [[Link/examples|examples]] · 🎨 [[Link/tokens|tokens]] · ♿ [[Link/accessibility|accessibility]] · 🖼 [[Link/Link-figma|figma]] · 📖 [[Link/Link-usage|usage]] · 🔍 [[Link/Link-audit|audit]]
**Missing:** `Link-pui.md`

### 🟢 [[component-lib/Pagination/Pagination|Pagination]]
`@8x8/oxygen-pagination` `0.77`

**Audit:** 🟢 YES — Zero CONFLICTs. Token hex values confirmed 2026-05-05. doc-rewrite can proceed.

**Files:** 📐 [[Pagination/props|props]] · 💡 [[Pagination/examples|examples]] · 🎨 [[Pagination/tokens|tokens]] · ♿ [[Pagination/accessibility|accessibility]] · 🖼 [[Pagination/Pagination-figma|figma]] · 📖 [[Pagination/Pagination-usage|usage]] · 🔍 [[Pagination/Pagination-audit|audit]]
**Missing:** `Pagination-pui.md`

### ⬜ sidebarMenu
`@8x8/oxygen-sidebarMenu`

---

## Data Display

### 🔴 [[component-lib/Avatar/Avatar|Avatar]]
`@8x8/oxygen-avatar`

**Audit:** 🔴 NO — 2 CONFLICTs — require human verification before doc-rewrite can proceed.

**Files:** 📐 [[Avatar/props|props]] · 💡 [[Avatar/examples|examples]] · 🎨 [[Avatar/tokens|tokens]] · ♿ [[Avatar/accessibility|accessibility]] · 🖼 [[Avatar/Avatar-figma|figma]] · 🔍 [[Avatar/Avatar-audit|audit]]
**Missing:** `Avatar-usage.md`, `Avatar-pui.md`

### 🟡 [[component-lib/Badge/Badge|Badge]]
`@8x8/oxygen-badge`

**Files:** 📐 [[Badge/props|props]] · 💡 [[Badge/examples|examples]] · 🎨 [[Badge/tokens|tokens]] · ♿ [[Badge/accessibility|accessibility]] · 🔧 [[Badge/badge-pui|pui]]
**Missing:** `badge-figma.md`, `badge-usage.md`, `badge-audit.md`

### 🔴 [[component-lib/DataTable/DataTable|DataTable]]
`@8x8/oxygen-dataTable`

**Audit:** 🔴 NO — 2 CONFLICTs — Pagination props interface: (limit/offset/totalResults) vs (pageNumber/rowsPerPage/canGoBack/canGoNext); must confirm which is canonical.

**Files:** 📐 [[DataTable/props|props]] · 💡 [[DataTable/examples|examples]] · 🎨 [[DataTable/tokens|tokens]] · ♿ [[DataTable/accessibility|accessibility]] · 🖼 [[DataTable/DataTable-figma|figma]] · 🔍 [[DataTable/DataTable-audit|audit]]
**Missing:** `DataTable-usage.md`, `DataTable-pui.md`

### 🔴 [[component-lib/Label/Label|Label]]
`@8x8/oxygen-label`

**Audit:** 🔴 NO — 2 CONFLICTs — token names/sizes diverge (MCP label01 12px vs Figma body01 14px); Figma information boolean mapping to infoBox props unverified.

**Files:** 📐 [[Label/props|props]] · 💡 [[Label/examples|examples]] · 🎨 [[Label/tokens|tokens]] · ♿ [[Label/accessibility|accessibility]] · 🖼 [[Label/Label-figma|figma]] · 🔧 [[Label/label-pui|pui]] · 🔍 [[Label/label-audit|audit]]
**Missing:** `label-usage.md`

### ⬜ list
`@8x8/oxygen-list`

### 🟢 [[component-lib/Tag/Tag|Tag]]
`@8x8/oxygen-tag` `0.70`

**Audit:** 🟢 YES — Zero CONFLICTs. All required files present. doc-rewrite can proceed.

**Files:** 📐 [[Tag/props|props]] · 💡 [[Tag/examples|examples]] · 🎨 [[Tag/tokens|tokens]] · ♿ [[Tag/accessibility|accessibility]] · 🖼 [[Tag/Tag-figma|figma]] · 🔍 [[Tag/Tag-audit|audit]]
**Missing:** `Tag-usage.md`, `Tag-pui.md`

---

## Feedback & Status

### 🔴 [[component-lib/AlertBanner/AlertBanner|AlertBanner]]
`@8x8/oxygen-alertBanner` `0.51`

**Audit:** 🔴 NO — 2 CONFLICTs — Figma exposes mode and breakpoint variant axes not present in OX API.

**Files:** 📐 [[AlertBanner/props|props]] · 💡 [[AlertBanner/examples|examples]] · 🎨 [[AlertBanner/tokens|tokens]] · ♿ [[AlertBanner/accessibility|accessibility]] · 🖼 [[AlertBanner/alert-banner-figma|figma]] · 🔍 [[AlertBanner/alert-banner-audit|audit]]
**Missing:** `alert-banner-usage.md`, `alert-banner-pui.md`

### 🟢 [[component-lib/ProgressBar/ProgressBar|ProgressBar]]
`@8x8/oxygen-loaders` `0.66`

**Audit:** 🟢 YES — Zero CONFLICTs. Pre-labelled conflicts in figma.md reclassified as DOC_GAPs with clear resolution paths.

**Files:** 📐 [[ProgressBar/props|props]] · 💡 [[ProgressBar/examples|examples]] · 🎨 [[ProgressBar/tokens|tokens]] · ♿ [[ProgressBar/accessibility|accessibility]] · 🖼 [[ProgressBar/ProgressBar-figma|figma]] · 🔍 [[ProgressBar/ProgressBar-audit|audit]]
**Missing:** `ProgressBar-usage.md`, `ProgressBar-pui.md`

### 🔴 [[component-lib/SkeletonBlock/SkeletonBlock|SkeletonBlock]]
`@8x8/oxygen-skeletons` `0.56`

**Audit:** 🔴 NO — 1 CONFLICT — SkeletonCircle size values documented in two incompatible formats across SkeletonBlock and SkeletonCircle folders.

**Files:** 📐 [[SkeletonBlock/props|props]] · 💡 [[SkeletonBlock/examples|examples]] · 🎨 [[SkeletonBlock/tokens|tokens]] · ♿ [[SkeletonBlock/accessibility|accessibility]] · 🖼 [[SkeletonBlock/SkeletonBlock-figma|figma]] · 🔍 [[SkeletonBlock/SkeletonBlock-audit|audit]]
**Missing:** `SkeletonBlock-usage.md`, `SkeletonBlock-pui.md`

### 🔴 [[component-lib/SkeletonCircle/SkeletonCircle|SkeletonCircle]]
`@8x8/oxygen-skeletons` `0.56`

**Audit:** 🔴 NO — 1 CONFLICT — size values documented in incompatible formats vs SkeletonBlock docs. Must align before rewrite.

**Files:** 📐 [[SkeletonCircle/props|props]] · 💡 [[SkeletonCircle/examples|examples]] · 🎨 [[SkeletonCircle/tokens|tokens]] · ♿ [[SkeletonCircle/accessibility|accessibility]] · 🖼 [[SkeletonCircle/SkeletonCircle-figma|figma]] · 🔍 [[SkeletonCircle/SkeletonCircle-audit|audit]]
**Missing:** `SkeletonCircle-usage.md`, `SkeletonCircle-pui.md`

### 🔴 [[component-lib/Spinner/Spinner|Spinner]]
`@8x8/oxygen-loaders` `0.61`

**Audit:** 🔴 NO — 2 CONFLICTs — Figma isInverted axis has no React prop (design-only vs API prop decision needed); React spinnerSize includes large2x but Figma only has default/small.

**Files:** 📐 [[Spinner/props|props]] · 💡 [[Spinner/examples|examples]] · 🎨 [[Spinner/tokens|tokens]] · ♿ [[Spinner/accessibility|accessibility]] · 🖼 [[Spinner/Spinner-figma|figma]] · 🔍 [[Spinner/Spinner-audit|audit]]
**Missing:** `Spinner-usage.md`, `Spinner-pui.md`

### 🟢 [[component-lib/Toast/Toast|Toast]]
`@8x8/oxygen-toast`

**Audit:** 🟢 YES — All core files present. Token coverage strong. PUI confirmed no relevant context. doc-rewrite can proceed.

**Files:** 📐 [[Toast/props|props]] · 💡 [[Toast/examples|examples]] · 🎨 [[Toast/tokens|tokens]] · ♿ [[Toast/accessibility|accessibility]] · 🖼 [[Toast/Toast-figma|figma]] · 🔧 [[Toast/Toast-pui|pui]] · 🔍 [[Toast/Toast-audit|audit]]
**Missing:** `Toast-usage.md`

### 🟡 [[component-lib/Toaster/Toaster|Toaster]]
`@8x8/oxygen-toaster`

**Files:** 📝 [[Toaster/toaster-note|note]]

---

## Overlays & Contextual

### ⬜ popover
`@8x8/oxygen-popover`

### 🔴 [[component-lib/Tooltip/Tooltip|Tooltip]]
`@8x8/oxygen-tooltip`

**Audit:** 🔴 NO — 2 CONFLICTs — character limit 140 (MCP) vs 136 (Figma); orientation default 'top' (MCP) vs 'Bottom' (Figma).

**Files:** 📐 [[Tooltip/props|props]] · 💡 [[Tooltip/examples|examples]] · 🎨 [[Tooltip/tokens|tokens]] · ♿ [[Tooltip/accessibility|accessibility]] · 🖼 [[Tooltip/Tooltip-figma|figma]] · 🔧 [[Tooltip/Tooltip-pui|pui]] · 📖 [[Tooltip/Tooltip-usage|usage]] · 🔍 [[Tooltip/Tooltip-audit|audit]]

---

## Date & Time

### ⬜ calendar
`@8x8/oxygen-calendar`

### ⬜ dateTimeRangeSelector
`@8x8/oxygen-dateTimeRangeSelector`

### ⬜ dateTimeSelector
`@8x8/oxygen-dateTimeSelector`

### ⬜ timeSelector
`@8x8/oxygen-timeSelector`

---
