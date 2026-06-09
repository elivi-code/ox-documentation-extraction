---
parent: "[[Tabs]]"
section: accessibility
pipeline_stage: doc_rewrite
tags:
  - oxygen
  - component/Tabs
  - role/spoke
  - section/accessibility
---

## Accessibility

_Guidelines to ensure compliant, and keyboard-accessible interactions within the Tabs component._

---

### Focus indicators

All interactive elements in the Tabs component support keyboard navigation with visible focus indicators.

| Property | Value |
|----------|-------|
| Style | 2px solid blue border (`interactive/focus01`, `#0056e0`) |
| Placement | Appears around the entire clickable area |
| Border radius | Maintained (rounded corners preserved on disclosure button) |

#### Focus behaviour

| Rule | Detail |
|------|--------|
| **Focus-visible only** | Appears during keyboard navigation; does **not** appear on mouse clicks |
| **High contrast** | Meets WCAG 2.1 Level AA contrast requirements |
| **Persistent** | Remains visible until focus moves to another element |

#### Elements that receive focus

- Tab buttons in the main tab bar
- Disclosure dropdown button (`tabsDisclosure`)
- Menu items in the overflow popover

---

### Keyboard interactions

| Key | Action |
|-----|--------|
| `Tab` | Moves focus forward between interactive elements (tabs → disclosure button → dropdown items) |
| `Shift + Tab` | Moves focus backwards through interactive elements |
| `←` Left Arrow | Moves focus to the previous tab in the tablist (WAI-ARIA tablist pattern — unconfirmed in OX implementation; see WARN-002) |
| `→` Right Arrow | Moves focus to the next tab in the tablist (WAI-ARIA tablist pattern — unconfirmed in OX implementation; see WARN-002) |
| `Enter` / `Space` | Activates the focused tab, or opens/closes the disclosure dropdown |
| `Escape` | Closes the dropdown menu when open |

#### Focus order

1. Visible tabs (left to right)
2. Disclosure button (if present)
3. Dropdown menu items (when dropdown is open)

---

### WCAG 2.1 Level AA compliance

| Criterion | Status | Description |
|-----------|--------|-------------|
| **1.4.1 Use of Color** | ✅ | Selected state signalled by 2px `actions/action01` underline **and** bold weight (`typography/bodyBold01`) — two non-color indicators |
| **2.1.1 Keyboard** | ✅ | All functionality available via keyboard |
| **2.1.2 No Keyboard Trap** | ✅ | Users can navigate away from all components |
| **2.4.7 Focus Visible** | ✅ | Clear focus indicators on all interactive elements |
| **3.2.1 On Focus** | ✅ | No unexpected context changes when receiving focus |
| **4.1.2 Name, Role, Value** | ✅ | Semantic HTML provides proper roles and states |

#### Recommended enhancements (not yet in OX baseline)

- Add `aria-label` or `aria-labelledby` to the tab container
- Implement `aria-selected="true/false"` on each tab for clearer active tab communication
- Add `aria-controls` relationships between tabs and their associated content panels
- Consider `aria-live` announcements when the active tab changes via the overflow dropdown

---

### ARIA roles (inferred from component nature)

> **WARN-002:** These roles are "inferred from component nature" — the Oxygen implementation may render as plain `div`/`button` elements without explicit ARIA roles. Verify against the rendered DOM before shipping docs that assert these roles as shipped.

| Element | Recommended role |
|---------|-----------------|
| Tab container | `role="tablist"` |
| Individual tab | `role="tab"` |
| Active tab | `aria-selected="true"` |
| Inactive tab | `aria-selected="false"` |
| Disabled tab | `aria-disabled="true"` |
| Content panel | `role="tabpanel"` with `aria-labelledby` pointing to its tab |
| Disclosure button | `aria-haspopup="true"`, `aria-expanded="true/false"` |
| Overflow menu | `role="menu"` |
| Overflow menu item | `role="menuitem"` |

---

### Screen reader guidance

- The active tab must be communicated via `aria-selected="true"` so screen readers announce the current section.
- When a tab selection changes via the overflow dropdown, an `aria-live` region or focus management should announce the change.
- Truncated tab labels (in overflow mode) must retain their full accessible name — the tooltip text or `aria-label` must contain the untruncated label.
- The `tabsDisclosure` button should have an accessible label such as `"More tabs"` or `"Show hidden tabs"`.

_Source: Figma accessibility documentation (node `86302:721`, file `5YihJ5WuDvnvrlrRMC4sBp`) · Extracted 2026-04-30 · GAP-009 + GAP-010 applied 2026-06-09_
