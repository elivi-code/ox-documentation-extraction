---
parent: "[[SidebarMenu]]"
section: usage
component: SidebarMenu
package: "@8x8/oxygen-sidebar-menu"
category: navigation
pipeline_stage: draft
source_type: editorial
tags:
  - oxygen
  - component/SidebarMenu
  - role/usage
  - stage/draft
  - category/navigation
---

> **Editorial guidance — no Figma examples page yet.** Authored from the extracted MCP and Figma artifacts. When a `↳ SidebarMenu examples` Figma page is created and populated, run `figma-extract-usage` to update this file with the authored Do/Don't frames.

A sidebar menu is the primary persistent navigation pattern for an application shell. It exposes top-level destinations, optional one-level sub-menus, badges for state, and a collapsible mode that compresses the rail to icon-only when screen real estate is scarce.

---

## Pair 1 — Default collapse state

**Decision:** Whether the sidebar should load expanded or collapsed on a fresh session, and how subsequent toggles should persist.
**Grounded in:** `initialCollapsedState: boolean` ([props](SidebarMenu.props.md)); `onCollapseChange` callback; CONFLICT GAP-009 noting the controlled/uncontrolled API split.

### ✅ Do — Start expanded on first visit, then persist the user's last toggle

Pass `initialCollapsedState={false}` on the user's first session so all destinations are legible and discoverable. Persist the value reported by `onCollapseChange` (localStorage, user-preferences API, etc.) and pass it back as `initialCollapsedState` on subsequent loads. The toggle is a preference, not a default.

### ❌ Don't — Default to `initialCollapsedState={true}` to "save space"

A collapsed-by-default sidebar hides every label behind an icon-only rail. First-time users must hover or expand to read item names, which adds friction to wayfinding. Only default to collapsed on layouts that are inherently dense (e.g. a workspace shell embedded in a larger frame) and even then, persist the user's override.

---

## Pair 2 — Badge: dot vs count vs none

**Decision:** Which badge variant signals what kind of item state.
**Grounded in:** Badge variants table (composition spoke); Figma dot vs counter variants (anatomy spoke).

### ✅ Do — Use a count badge only when the number is actionable

Use `hasBadge badgeChildren="5"` when the count drives behaviour ("5 unread messages", "12 tickets to triage"). Use a dot (`hasBadge` without `badgeChildren`) when the item simply has *something new* but the exact number doesn't matter ("new release notes available"). Use no badge for steady-state destinations.

### ❌ Don't — Decorate every item with a badge or surface counts users can't act on

A sidebar where most items wear a badge teaches users to ignore them; the signal collapses. Equally, avoid counts that don't reduce — a permanent "12+" that never changes is visual noise, not status. Choose the lowest-fidelity badge that conveys the state: nothing > dot > count.

---

## Pair 3 — Badge accessibility

**Decision:** When `badgeAriaLabel` is required, not optional.
**Grounded in:** `badgeAriaLabel` prop; a11y guidance on truncated counts (accessibility spoke); WCAG 4.1.2 / 4.1.3.

### ✅ Do — Supply `badgeAriaLabel` whenever the badge isn't fully self-describing

For dot badges, set `badgeAriaLabel="new"` (or the localised equivalent) so screen-reader users learn the item has unread state. For truncated counts like `"99+"`, set `badgeAriaLabel="99 unread notifications"` so AT announces meaning, not glyphs. Keep the visual short; let the aria label carry the semantics.

### ❌ Don't — Rely on the visual `"99+"` or a bare dot to communicate to AT

A screen reader announcing `"99 plus"` or skipping the dot entirely conveys nothing. Any badge that isn't a literal, complete number with a clear noun ("3 messages") needs `badgeAriaLabel`. This is the most common a11y regression on sidebar nav.

---

## Pair 4 — Footer slot intent

**Decision:** What kinds of items belong in `isFooter` items (rendered in the `MenuList footer` slot) vs the main list.
**Grounded in:** `isFooter` flag on `SidebarItemProps`; footer examples showing Help / Feedback / Audit-log events; Figma "Secondary Navigation" frame role (anatomy spoke).

### ✅ Do — Reserve the footer for meta, support, and account items

Put items the user reaches occasionally and that aren't the work itself: Help, Send feedback, Audit log, Settings, Sign out. These are *about* the app, not the app's primary destinations. The visual divider above the footer already promises a category change — make the items match the promise.

### ❌ Don't — Park primary destinations in the footer to "shorten" the main list

If a destination is part of the day-to-day workflow, it belongs in the main list even if the list is long. Banishing a workflow item to the footer hides it below the fold on short viewports and below a divider that visually demotes it. Trim the main list by combining destinations into sub-menus, not by moving them to the footer.

---

## Pair 5 — Active state expression

**Decision:** How the active item is communicated visually and to assistive technology.
**Grounded in:** `isActive: boolean`; `active12` token bound to active item background (tokens spoke); WCAG 1.4.1 "use of color" + `aria-current="page"` mapping (accessibility spoke).

### ✅ Do — Pair the `active12` background with a non-color cue and `aria-current="page"`

`isActive={true}` must produce both the `active12` background *and* a non-color signal — the bold label weight and active-state icon treatment baked into the Figma `_Menu List Items / Expanded` atom. The interactive element inside the active item also receives `aria-current="page"` so AT announces the current route.

### ❌ Don't — Indicate active by background color alone, or skip `aria-current`

A background-only active cue fails WCAG 1.4.1 for users who can't perceive the color difference (low contrast environments, color vision deficiency). Equally, an active item without `aria-current="page"` looks correct to sighted users but leaves screen-reader users without a "you are here" anchor. Both signals are required, not alternatives.

---

## Pair 6 — Collapse toggle labels and localisation

**Decision:** What text appears on the `CollapseItem` and how it tracks state.
**Grounded in:** `collapseLabel` / `expandLabel` props; `label={isSidebarCollapsed ? expandLabel : collapseLabel}` pattern (composition spoke).

### ✅ Do — Pass both labels, swap them by state, and translate them with the app

Always pass both `collapseLabel` (visible when expanded → action collapses) and `expandLabel` (visible when collapsed → action expands), and bind them to the live collapse state via `label={isSidebarCollapsed ? expandLabel : collapseLabel}`. Localise both strings — the component has no fallback for translated UIs.

### ❌ Don't — Use a single static label like "Toggle sidebar" or ship English defaults to translated apps

A label that doesn't change with state forces the user to read the icon to understand what activating the control will do — and screen readers can't reliably announce the icon. A hard-coded English string in a translated product is an obvious regression. The two-label pattern is a small cost that prevents both failure modes.

---

## Axes presented but skipped

These editorial axes are grounded in the extracted files but were not developed into pairs here:

- **Config-driven (`<Sidebar>`) vs declarative composition** — choosing which API surface to reach for first. See the composition spoke for both patterns.
- **Sub-menu nesting depth** — `subItems` is one-level only; deeper hierarchies require a different pattern.
- **Position: left vs right** — `position: "left" | "right"`. Skipped because the right-side use case is rare and not exemplified in extracted Figma frames.
- **Icons on top-level items** — every example top-level item carries an icon; collapsed mode leaves only icons visible.
- **Label length and wrapping** — examples deliberately include `"Channels with longer text"` to exercise wrap behaviour.
- **Router integration (`linkComponent`/`linkProp`)** — documented in props but covered by audit GAP-005 (now resolved). See composition spoke Pattern 3.
