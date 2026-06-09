---
parent: "[[Tabs]]"
section: composition
pipeline_stage: doc_rewrite
tags:
  - oxygen
  - component/Tabs
  - role/spoke
  - section/composition
---

## Composition

### Subcomponents

| Component | Role | Condition |
|-----------|------|-----------|
| [[Tab]] | Tab item child — required structural child of `<Tabs>` | One or more required |
| [[Icon]] | Leading icon in a tab label | When `icon=true` on a `<Tab>` |
| [[Badge]] | Notification indicator on a tab or disclosure button | When `badge=true` on `<Tab>` or `tabsDisclosure` |
| [[IconButton]] | Base component for `tabsDisclosure` overflow button | Rendered automatically when tabs overflow |
| `.Tabs Popover` | Dropdown menu listing hidden overflow tabs | Rendered by the container when overflow occurs (node `86115:3520`) |

---

### Progressive overflow assembly

The `<Tabs>` container automatically manages the overflow lifecycle. The consuming application only controls `<Tab>` children; `tabsDisclosure` and `.Tabs Popover` are rendered by the container as needed.

| Stage | Components rendered |
|-------|-------------------|
| All tabs fit | `<Tabs>` + N × `<Tab>` |
| Some tabs overflow | `<Tabs>` + visible `<Tab>`s + `tabsDisclosure` button + `.Tabs Popover` (when open) |
| Single tab (selected is last) | `<Tabs>` + 1 × `<Tab hasDropdown>` + `.Tabs Popover` (when open); no separate `tabsDisclosure` button |

The active tab is always visible in the main row. When a user selects an overflowed tab, it swaps into a visible slot and the displaced tab moves to overflow. The overflow algorithm preserves the **currently active** tab, not the most-used tabs.

---

### Patterns using Tabs

Tabs is commonly used as a container for sibling content sections within a single page:

| Pattern | Tabs role |
|---------|-----------|
| User/entity record (Overview / Activity / Files) | Top-level section switcher |
| Settings pane (Profile / Security / Notifications) | Top-level section switcher |
| Analytics view (Summary / Trends / Breakdown) | Metric dimension switcher |
| Inbox/Sent/Archived email view | Content-type switcher |

---

### When to prefer an alternative

| Scenario | Preferred alternative |
|----------|-----------------------|
| Binary or small-count mutually exclusive choice | [[SegmentedControl]] or [[Radio]] |
| App-level destination switching (route changes) | Application shell navigation |
| Linear step-by-step flow requiring completion order | [[Stepper]] |
| Many sections (8+) with frequent overflow at default widths | Side nav or [[Accordion]] |
| Container is reliably narrow (single-tab state is the norm) | [[Select]] |

_Source: Figma (file `5YihJ5WuDvnvrlrRMC4sBp`) + usage documentation · 2026-04-30_
