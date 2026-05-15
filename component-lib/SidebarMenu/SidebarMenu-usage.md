---
component: SidebarMenu
package: "@8x8/oxygen-sidebar-menu"
category: navigation
role: usage
role_description: "Usage guidelines — editorial Do/Don't guidance; produced without a Figma examples page. Update with figma-extract-usage when the '↳ SidebarMenu examples' Figma page exists."
pipeline_stage: editorial
pipeline_note: "Authored editorially from extracted MCP/Figma artifacts — no '↳ SidebarMenu examples' Figma page yet. Run figma-extract-usage to update once that page is created."
source_type: editorial
audit_verdict: null
siblings:
  - "[[SidebarMenu/props]]"
  - "[[SidebarMenu/examples]]"
  - "[[SidebarMenu/tokens]]"
  - "[[SidebarMenu/accessibility]]"
  - "[[SidebarMenu/SidebarMenu-figma]]"
  - "[[SidebarMenu/SidebarMenu-audit]]"
tags:
  - oxygen
  - component/SidebarMenu
  - role/usage
  - stage/editorial
  - category/navigation
---
<!-- SKILL: usage-advisor -->
<!-- COMPONENT: SidebarMenu -->
<!-- DRAFTED: 2026-05-14 -->
<!-- MODE: open -->
<!-- GROUNDING: full -->
<!-- PAIRS: 6 -->
<!-- STATUS: editorial — update with figma-extract-usage when '↳ SidebarMenu examples' Figma page exists -->

# SidebarMenu — Usage Guidelines

> **Editorial guidance — no Figma examples page yet.** Authored from the extracted MCP and Figma artifacts. When a `↳ SidebarMenu examples` Figma page is created and populated, run `figma-extract-usage` to update this file with the authored Do/Don't frames.
>
> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md) · [SidebarMenu-figma.md](./SidebarMenu-figma.md) · [SidebarMenu-audit.md](./SidebarMenu-audit.md)

A sidebar menu is the primary persistent navigation pattern for an application shell. It exposes top-level destinations, optional one-level sub-menus, badges for state, and a collapsible mode that compresses the rail to icon-only when screen real estate is scarce.

---

## Grounding summary

- **Files used:** [props.md](./props.md), [examples.md](./examples.md), [tokens.md](./tokens.md), [accessibility.md](./accessibility.md), [SidebarMenu-figma.md](./SidebarMenu-figma.md), [SidebarMenu-audit.md](./SidebarMenu-audit.md)
- **Files missing:** `SidebarMenu-pui.md` (N/A — PUI MCP confirmed no Platform UI package for `sidebarMenu`; see audit GAP-N/A entry)
- **Internal precedent consulted:** [Breadcrumbs-usage.md](../Breadcrumbs/Breadcrumbs-usage.md), [PopoverMenu-usage.md](../PopoverMenu/PopoverMenu-usage.md) — both navigation category. Mirrored their 6-pair structure and "Decision / Grounded in / Internal precedent" framing.

---

## Pair 1 — Default collapse state

**Decision:** Whether the sidebar should load expanded or collapsed on a fresh session, and how subsequent toggles should persist.
**Grounded in:** `initialCollapsedState: boolean` ([props.md:79](./props.md)); `onCollapseChange` callback ([props.md:82](./props.md)); CONFLICT GAP-009 noting the controlled/uncontrolled API split ([SidebarMenu-audit.md:259–263](./SidebarMenu-audit.md)).
**Internal precedent:** None in the navigation usage docs reviewed.

### ✅ Do — Start expanded on first visit, then persist the user's last toggle
Pass `initialCollapsedState={false}` on the user's first session so all destinations are legible and discoverable. Persist the value reported by `onCollapseChange` (localStorage, user-preferences API, etc.) and pass it back as `initialCollapsedState` on subsequent loads. The toggle is a preference, not a default.

### ❌ Don't — Default to `initialCollapsedState={true}` to "save space"
A collapsed-by-default sidebar hides every label behind an icon-only rail. First-time users must hover or expand to read item names, which adds friction to wayfinding. Only default to collapsed on layouts that are inherently dense (e.g. a workspace shell embedded in a larger frame) and even then, persist the user's override.

---

## Pair 2 — Badge: dot vs count vs none

**Decision:** Which badge variant signals what kind of item state.
**Grounded in:** Badge variants table ([examples.md:277–284](./examples.md)); Figma dot vs counter variants ([SidebarMenu-figma.md:82–83](./SidebarMenu-figma.md)).
**Internal precedent:** None in the navigation usage docs reviewed (Breadcrumbs/PopoverMenu don't surface state badges).

### ✅ Do — Use a count badge only when the number is actionable
Use `hasBadge badgeChildren="5"` when the count drives behaviour ("5 unread messages", "12 tickets to triage"). Use a dot (`hasBadge` without `badgeChildren`) when the item simply has *something new* but the exact number doesn't matter ("new release notes available"). Use no badge for steady-state destinations.

### ❌ Don't — Decorate every item with a badge or surface counts users can't act on
A sidebar where most items wear a badge teaches users to ignore them; the signal collapses. Equally, avoid counts that don't reduce — a permanent "12+" that never changes is visual noise, not status. Choose the lowest-fidelity badge that conveys the state: nothing > dot > count.

---

## Pair 3 — Badge accessibility

**Decision:** When `badgeAriaLabel` is required, not optional.
**Grounded in:** `badgeAriaLabel` prop ([props.md:99,119,138](./props.md)); a11y guidance on truncated counts ([accessibility.md:61](./accessibility.md)); WCAG 4.1.2 / 4.1.3 entries ([accessibility.md:77–78](./accessibility.md)).
**Internal precedent:** None in the navigation usage docs reviewed.

### ✅ Do — Supply `badgeAriaLabel` whenever the badge isn't fully self-describing
For dot badges, set `badgeAriaLabel="new"` (or the localised equivalent) so screen-reader users learn the item has unread state. For truncated counts like `"99+"`, set `badgeAriaLabel="99 unread notifications"` so AT announces meaning, not glyphs. Keep the visual short; let the aria label carry the semantics.

### ❌ Don't — Rely on the visual `"99+"` or a bare dot to communicate to AT
A screen reader announcing `"99 plus"` or skipping the dot entirely conveys nothing. Any badge that isn't a literal, complete number with a clear noun ("3 messages") needs `badgeAriaLabel`. This is the most common a11y regression on sidebar nav.

---

## Pair 4 — Footer slot intent

**Decision:** What kinds of items belong in `isFooter` items (rendered in the `MenuList footer` slot) vs the main list.
**Grounded in:** `isFooter` flag on `SidebarItemProps` ([props.md:95](./props.md)); footer examples showing Help / Feedback / Audit-log events ([examples.md:74–90](./examples.md)); Figma "Secondary Navigation" frame role ([SidebarMenu-figma.md:66](./SidebarMenu-figma.md)).
**Internal precedent:** None in the navigation usage docs reviewed.

### ✅ Do — Reserve the footer for meta, support, and account items
Put items the user reaches occasionally and that aren't the work itself: Help, Send feedback, Audit log, Settings, Sign out. These are *about* the app, not the app's primary destinations. The visual divider above the footer already promises a category change — make the items match the promise.

### ❌ Don't — Park primary destinations in the footer to "shorten" the main list
If a destination is part of the day-to-day workflow, it belongs in the main list even if the list is long. Banishing a workflow item to the footer hides it below the fold on short viewports and below a divider that visually demotes it. Trim the main list by combining destinations into sub-menus, not by moving them to the footer.

---

## Pair 5 — Active state expression

**Decision:** How the active item is communicated visually and to assistive technology.
**Grounded in:** `isActive: boolean` ([props.md:81,114](./props.md)); `active12` token bound to active item background ([tokens.md:36](./tokens.md)); WCAG 1.4.1 "use of color" + `aria-current="page"` mapping ([accessibility.md:59,72](./accessibility.md)).
**Internal precedent:** [Breadcrumbs-usage.md](../Breadcrumbs/Breadcrumbs-usage.md) — "Make the current page the last, non-link item" pair confirms 8x8 navigation convention treats *current location* as semantically distinct and rendered without link affordance. Same principle here: active state is structural, not just stylistic.

### ✅ Do — Pair the `active12` background with a non-color cue and `aria-current="page"`
`isActive={true}` must produce both the `active12` background (see [tokens.md](./tokens.md)) *and* a non-color signal — the bold label weight and active-state icon treatment baked into the Figma `_Menu List Items / Expanded` atom. The interactive element inside the active item also receives `aria-current="page"` so AT announces the current route.

### ❌ Don't — Indicate active by background color alone, or skip `aria-current`
A background-only active cue fails WCAG 1.4.1 for users who can't perceive the color difference (low contrast environments, color vision deficiency). Equally, an active item without `aria-current="page"` looks correct to sighted users but leaves screen-reader users without a "you are here" anchor. Both signals are required, not alternatives.

---

## Pair 6 — Collapse toggle labels and localisation

**Decision:** What text appears on the `CollapseItem` and how it tracks state.
**Grounded in:** `collapseLabel` / `expandLabel` props ([props.md:80–81](./props.md)); `label={isSidebarCollapsed ? expandLabel : collapseLabel}` pattern ([examples.md:259, accessibility.md:63](./examples.md)).
**Internal precedent:** [Breadcrumbs-usage.md](../Breadcrumbs/Breadcrumbs-usage.md) — "Localise `collapsedTitle` and `ariaLabel`" pair establishes the 8x8 convention that any string the component can't infer from props must be passed in as a localised value, never defaulted in English.

### ✅ Do — Pass both labels, swap them by state, and translate them with the app
Always pass both `collapseLabel` (visible when expanded → action collapses) and `expandLabel` (visible when collapsed → action expands), and bind them to the live collapse state via `label={isSidebarCollapsed ? expandLabel : collapseLabel}`. Localise both strings — the component has no fallback for translated UIs.

### ❌ Don't — Use a single static label like "Toggle sidebar" or ship English defaults to translated apps
A label that doesn't change with state forces the user to read the icon to understand what activating the control will do — and screen readers can't reliably announce the icon. A hard-coded English string in a translated product is an obvious regression. The two-label pattern is a small cost that prevents both failure modes.

---

## Axes presented but skipped

These editorial axes are grounded in the extracted files but were not developed into pairs here. Consider them on the next pass if the corresponding Figma frames are added.

- **Config-driven (`<Sidebar>`) vs declarative composition (`SidebarContainer` + `MenuList` + `MenuItem`)** — choosing which API surface to reach for first. Grounded in [examples.md:28–33](./examples.md). Skipped as it's an engineering pattern decision, less editorial than the rest.
- **Sub-menu nesting depth** — `subItems` is one-level only ([props.md:100](./props.md)); deeper hierarchies require a different pattern. Worth a pair if teams are pushing two-level nesting.
- **Position: left vs right** — `position: "left" | "right"` ([props.md:78](./props.md)). Skipped because the right-side use case is rare and not exemplified in extracted Figma frames.
- **Icons on top-level items** — every example top-level item carries an icon ([examples.md:50–88](./examples.md)); collapsed mode leaves only icons visible. A "Do — always provide icons on top-level items; Don't — ship icon-less items that vanish when collapsed" pair is defensible.
- **Label length and wrapping** — examples deliberately include `"Channels with longer text"` to exercise wrap behaviour. Worth a pair if length conventions vary across teams.
- **Router integration (`linkComponent`/`linkProp`)** — documented in props but no example exists; covered by audit GAP-005. Engineering-leaning; revisit when GAP-005 is closed.

## Axes flagged as ungrounded

None — every axis surfaced in this run traces to a real prop, state, or annotation in the SidebarMenu files.

---

## Next steps

1. Review the 6 pairs above; tighten wording where the Figma examples page will need exact captions.
2. Author the matching frames on `↳ SidebarMenu examples` in Figma — one ✅ Do — {reason} frame and one ❌ Don't — {reason} frame per pair. Use the candidate framings here as starter copy.
3. Run `/figma-extract-usage SidebarMenu` once that page exists — it will update this file with the Figma-authored content.
4. Re-run `/doc-audit SidebarMenu` to close audit gap **GAP-008** (usage SOURCE_GAP) and revisit the **GAP-009** CONFLICT on the collapse API surface.
