# Tabs — Component Spec

> **Status:** Under review
> **Package:** `@8x8/oxygen-tabs`
> **Category:** Layout
> **Figma file:** `5YihJ5WuDvnvrlrRMC4sBp` ([UI components](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components))
> **Extracted:** 2026-04-30
> **Spec produced by:** doc-rewrite · Rubric v1.0

---

## Overview

Tabs are used when a user needs to navigate between content within a page.

The component uses **container-based progressive overflow** — tabs collapse from right to left as the container narrows, with overflow tabs accessible via a disclosure popover. The active tab is always visible in the main tab bar.

### Installation

```sh
# yarn
yarn add @8x8/oxygen-tabs

# npm
npm install @8x8/oxygen-tabs
```

**Registry prerequisite:**

```ini
# .npmrc
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```

```yaml
# .yarnrc.yml
npmScopes:
  8x8:
    npmRegistryServer: "https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/"
nodeLinker: node-modules
```

---

## Props

### `<Tabs>` (default export)

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `ReactNode` | — | ✅ | Component content (one or more `<Tab>` elements) |
| `color` | `"light" \| "dark"` | — | | Color mode |
| `forwardedRef` | `object \| func` | `null` | ✅ | Component ref |

> **WARN-001:** `forwardedRef` is marked required with a `null` default — the API is ambiguous. Downstream type generation may emit a non-optional ref parameter.

<!-- GAP-008: color prop default for <Tabs> is undocumented. Check @8x8/oxygen-tabs source to confirm whether it defaults to 'light', inherits from context, or requires explicit specification. -->

### `<Tab>` (named export)

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `children` | `ReactNode` | — | ✅ | Tab content |
| `color` | `"light" \| "dark"` | — | | Color mode |
| `value` | `any` | — | | Value returned to `onClick` handler |
| `isActive` | `boolean` | `false` | | Whether this tab is the active/selected tab |
| `isDisabled` | `boolean` | `false` | | Whether this tab is non-interactive |
| `isStretched` | `boolean` | `false` | | Stretches tab to fill available space in `<Tabs>` |
| `onClick` | `(ev: React.MouseEvent, value: any) => void` | `noop` | | Click handler; called with the event and the tab's `value` |
| `testId` | `string` | `'TABS'` | | `data-testid` attribute value for automated testing |

<!-- GAP-007: isStretched description is inferred — MCP returned an eslint-disable comment instead of a real doc string. Verify from @8x8/oxygen-tabs source or Storybook. -->
<!-- GAP-008: color prop default for <Tab> is undocumented. -->

### Figma design properties — `tabs` component set (node `85651:78740`)

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `state` | Variant: `"rest" \| "hover"` | `"rest"` | Interaction state |
| `isSelected` | Variant: `"false" \| "true"` | `"false"` | Active/selected state (maps to `isActive` in code) |
| `isDisabled` | Variant: `"false" \| "true"` | `"false"` | Disabled state |
| `tabLabel` | Text | `"Label"` | Tab display label |
| `icon` | Boolean | `false` | Show an icon alongside the label |
| `selectIcon` | Instance swap | <!-- STUB:GAP-006 source="Query figma_get_component for node 85016:131 to retrieve the icon name" --> | The icon component to render |
| `badge` | Boolean | `false` | Show a notification badge on the tab |
| `isFocus` | Boolean | `false` | Force focus ring visible (for prototyping) |
| `hasDropdown` | Boolean | `false` | Active when only this tab is visible; transforms tab into a popover trigger |

### Figma design properties — `tabsDisclosure` component (node `85651:78793`)

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `badge` | Boolean | `false` | Show a notification badge on the disclosure button |

---

## Examples

> **GAP-012 (manual):** No MCP-sourced code examples exist — the Oxygen MCP returned 0 clean snippets. All code below was constructed from prop definitions. Authoritative examples should be sourced from the `@8x8/oxygen-tabs` Storybook or source repository before shipping docs.

### Basic usage

```tsx
import Tabs, { Tab } from '@8x8/oxygen-tabs';

function Example() {
  const [active, setActive] = React.useState('tab1');

  return (
    <Tabs>
      <Tab
        value="tab1"
        isActive={active === 'tab1'}
        onClick={(ev, value) => setActive(value)}
      >
        Section 1
      </Tab>
      <Tab
        value="tab2"
        isActive={active === 'tab2'}
        onClick={(ev, value) => setActive(value)}
      >
        Section 2
      </Tab>
      <Tab
        value="tab3"
        isActive={active === 'tab3'}
        isDisabled
        onClick={(ev, value) => setActive(value)}
      >
        Section 3
      </Tab>
    </Tabs>
  );
}
```

### Color modes

The `color` prop on both `<Tabs>` and `<Tab>` controls the light/dark mode:

```tsx
<Tabs color="dark">
  <Tab value="a" isActive color="dark" onClick={handler}>Label</Tab>
  <Tab value="b" color="dark" onClick={handler}>Label</Tab>
</Tabs>
```

### Stretched tabs

Use `isStretched` to make a tab fill available space in the container:

```tsx
<Tabs>
  <Tab value="a" isActive isStretched onClick={handler}>Section 1</Tab>
  <Tab value="b" isStretched onClick={handler}>Section 2</Tab>
</Tabs>
```

---

## Design Tokens

### Color tokens (from Figma — variable IDs unresolved)

| State | Property | Variable ID | Hex value | Semantic name |
|-------|----------|-------------|-----------|---------------|
| rest (unselected) | bottom border | `20136:253` | `#EBEAE1` | _unresolved — GAP-001_ |
| disabled | bottom border | `20136:324` | `#C8C7BD` | _unresolved — GAP-001_ |
| hover (unselected) | bottom border | `20136:265` | `#26253A` | _unresolved — GAP-001_ |
| selected / active | bottom border | `20136:286` | `#0057E0` | _unresolved — GAP-001_ |

> The selected state uses a **2px** bottom border; all other states use **1px**.

> **GAP-001 (manual):** Semantic token names (e.g. `border03`, `interactive01`) are unresolved. Downstream Storybook controls need these names. Fix: access the Figma variable library for file `5YihJ5WuDvnvrlrRMC4sBp` and resolve each variable ID.

### Focus token

| Token | Value | Usage |
|-------|-------|-------|
| `$focus01` | `#0057E0` (2px solid blue) | Focus ring on tabs, disclosure button, and dropdown menu items |

### Typography tokens

<!-- STUB:GAP-002 source="Inspect the tab label TEXT node inside the selected variant (85651:78786) for text style name and font properties; add to tokens.md" -->

> Typography tokens not captured. The Figma screenshot shows the selected tab label renders bold compared to unselected, but no font size, font weight, line height, letter spacing, or text style token is documented. Re-run `figma-extract` targeting text node inside variant `85651:78786`.

### Spacing

| Element | Property | Value |
|---------|----------|-------|
| `tabs` (default tab) | Padding (all sides) | `16px` |
| `tabs` (default tab) | Height | `52px` (HUG) |
| `tabsDisclosure` | Padding (all sides) | `6px` |
| `tabsDisclosure` | Size | `52 × 52px` |

> No dedicated tab token namespace exists in the Oxygen theme token registry as of extraction date. Color values above are derived from Figma variable bindings.

---

## Usage Guidelines

<!-- STUB:GAP-003 source="Run figma-extract-usage for Tabs to produce Tabs-usage.md with Do/Don't guidelines" -->

> Usage guidelines (Do/Don't pairs) are not yet available. Run `figma-extract-usage` for Tabs after the designer fills the examples page ([Figma – node 85697:271849](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=85697-271849)), then re-run `doc-audit` and `doc-rewrite`.

---

## Design Decisions

### Component anatomy

**File:** `UI components` (`5YihJ5WuDvnvrlrRMC4sBp`)
**Component set:** `tabs` · node `85651:78740` · [Open in Figma](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=85651-78740)

#### Variants

| Variant | isSelected | isDisabled | state | Bottom border |
|---------|-----------|-----------|-------|--------------|
| `state=rest, isSelected=false, isDisabled=false` | false | false | rest | 1px · `#EBEAE1` |
| `state=rest, isSelected=false, isDisabled=true` | false | true | rest | 1px · `#C8C7BD` |
| `state=hover, isSelected=false, isDisabled=false` | false | false | hover | 1px · `#26253A` |
| `state=rest, isSelected=true, isDisabled=false` | true | false | rest | **2px** · `#0057E0` |

<!-- GAP-005 (manual): The Figma screenshot shows the selected tab label renders bold. This typographic state change is not documented in the variant table. Inspect text node inside variant 85651:78786 for font weight / text style; document in variant table and tokens. -->

#### Tab layout

| Property | Value |
|----------|-------|
| Layout mode | VERTICAL (auto-layout) |
| Padding | 16px all sides |
| Sizing | HUG (width and height) |
| Default size | ~68px wide × 52px tall |
| Transition | SMART_ANIMATE, 70ms, cubic-bezier(0.2, 0, 0.38, 0.9) |

#### `tabsDisclosure` — overflow button (node `85651:78793`)

The overflow "more" trigger button; shown when not all tabs fit in the container.

| Property | Value |
|----------|-------|
| Layout mode | VERTICAL (auto-layout) |
| Padding | 6px all sides |
| Size | 52 × 52px |
| Contains | `Icon Button` (chevron-down) + optional badge frame |
| Bottom border | 1px, same token as rest state |

States: `rest` · `hover` · `active` · `focus/selected` · `disabled` · `badge`

> **WARN-003:** `tabsDisclosure` inherits an `active` press state from Icon Button, but the individual tab component set exposes only `rest` and `hover` variant axes. Press-state visual (if any) is undocumented.

#### `.Tabs Popover` atom (node `86115:3520`)

The popover/dropdown that renders overflow tabs. Size: 296 × 200px.

### Visual snapshots

<!-- STUB:GAP-004 source="Re-run figma_take_screenshot for nodes 85651:78740, 85651:78793, 86754:680 and save PNGs to component-lib/Tabs/" -->

> Three screenshots are not yet on disk. Re-capture from Figma:
> - `figma-tabs-variants.png` — node `85651:78740` (all variants)
> - `figma-tabs-disclosure.png` — node `85651:78793` (tabsDisclosure)
> - `figma-tabs-popover-atom.png` — node `86754:680` (.Tabs Popover atom)

### Progressive overflow behaviour

The Tabs component uses **container-based** progressive overflow — not fixed breakpoints. It dynamically calculates how many tabs fit at any given container width, collapsing from right to left.

| Stage | What happens |
|-------|-------------|
| **Full width** | All tabs visible in a single row |
| **Partial collapse** | Container narrows → trailing tabs hide → `tabsDisclosure` appears |
| **Progressive hiding** | More tabs hide → disclosure consolidates all overflow tabs into one menu trigger |
| **Single tab** | Only the active tab remains → transforms into a popover trigger (`hasDropdown` enabled) → expands to 100% container width → `tabsDisclosure` removed |

**Active tab visibility guarantee:** The currently selected tab is always visible in the main tab bar. When a user selects a tab from the overflow menu, the system swaps it into the visible row; the displaced tab moves to the overflow.

**Last visible tab responsive behaviour:**

| State | Behaviour |
|-------|-----------|
| **Pre-collapse** | Tab appears in full, uncompressed form |
| **Fluid width** | Tab expands to 100% of remaining container width |
| **Truncation** | Label truncates with ellipsis; dropdown icon remains interactive |
| **Tooltip reveal** | Tooltip on hover/focus shows full untruncated label |

### Figma prop guidance

**`icon`:** Use when there is a decorative element to reinforce the meaning of the tab. Also used in compact view when the label is hidden due to space constraints.

**`badge`:** Use when the content of a tab includes a list of notifications.

**`hasDropdown`:** Active only when the container is reduced to the point where only one tab is visible. The tab transforms into a popover trigger; the separate `tabsDisclosure` button is removed.

### Legacy / hidden components

| Name | Node ID | Note |
|------|---------|------|
| `Fixed width tabs` | `5178:4112` | COMPONENT_SET, hidden — legacy variant |
| `Rectangle 2` | `5178:4145` | RECTANGLE, hidden — design artifact |

---

## Accessibility

> _Guidelines to ensure compliant, keyboard-accessible interactions within the Tabs component._

### Focus indicators

All interactive elements support keyboard navigation with visible focus indicators.

| Property | Value |
|----------|-------|
| Style | 2px solid blue border (`$focus01`) |
| Placement | Around the entire clickable area |
| Border radius | Maintained (rounded corners preserved on disclosure button) |

| Rule | Detail |
|------|--------|
| **Focus-visible only** | Appears during keyboard navigation; does **not** appear on mouse clicks |
| **High contrast** | Meets WCAG 2.1 Level AA contrast requirements |
| **Persistent** | Remains visible until focus moves to another element |

Elements that receive focus: tab buttons · disclosure dropdown button · overflow menu items.

### Keyboard interactions

| Key | Action |
|-----|--------|
| `Tab` | Moves focus forward: tabs → disclosure button → dropdown items |
| `Shift + Tab` | Moves focus backwards through interactive elements |
| `Enter` / `Space` | Activates the focused tab, or opens/closes the disclosure dropdown |
| `Escape` | Closes the dropdown menu when open |

<!-- GAP-009 (manual): Left/Right arrow key navigation within the tablist is not documented. WAI-ARIA Authoring Practices for the tablist pattern require Left/Right arrows to move focus between tabs without activating them (optionally Home/End for first/last). Confirm whether OX Tabs implements this and add rows if so. -->

**Focus order:** visible tabs (left to right) → disclosure button (if present) → dropdown menu items (when open).

### WCAG 2.1 Level AA

| Criterion | Status | Notes |
|-----------|--------|-------|
| **2.1.1 Keyboard** | ✅ | All functionality available via keyboard |
| **2.1.2 No Keyboard Trap** | ✅ | Users can navigate away from all components |
| **2.4.7 Focus Visible** | ✅ | Clear focus indicators on all interactive elements |
| **3.2.1 On Focus** | ✅ | No unexpected context changes when receiving focus |
| **4.1.2 Name, Role, Value** | ✅ | Semantic HTML provides proper roles and states |

<!-- GAP-010 (manual, depends GAP-005): WCAG 1.4.1 (Use of Color) not yet assessed. The selected tab is differentiated by a blue bottom border. If bold font weight on the selected tab is confirmed as intentional (resolve GAP-005), the component passes — two indicators (color + weight). If color is the sole differentiator, it may fail 1.4.1. Add this row after GAP-005 is resolved. -->

### Recommended enhancements (not yet in OX baseline)

- Add `aria-label` or `aria-labelledby` to the tab container
- Implement `aria-selected="true/false"` on each tab
- Add `aria-controls` relationships between tabs and their content panels
- Consider `aria-live` announcements when the active tab changes via the overflow dropdown

### ARIA roles

> **WARN-002:** Roles below are labelled "inferred from component nature" in the source data. Verify against the rendered DOM before shipping docs — if the implementation does not use `role="tablist"` / `role="tab"` / `aria-selected`, the items below become requirements rather than confirmations.

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

### Screen reader guidance

- Active tab must be communicated via `aria-selected="true"` so screen readers announce the current section.
- When a tab selection changes via the overflow dropdown, an `aria-live` region or focus management should announce the change.
- Truncated tab labels must retain their full accessible name — the tooltip text or `aria-label` must contain the untruncated label.
- The `tabsDisclosure` button should have an accessible label such as `"More tabs"` or `"Show hidden tabs"`.

---

## Platform UI Integration

<!-- NO RELEVANT PUI CONTEXT -->

No Platform UI packages are relevant to this component. Candidates reviewed and rejected:

| Package | Reason rejected |
|---------|-----------------|
| `@8x8/pui-use-navigation` | General shell navigation hook — not Tabs-specific |
| `@8x8/pui-use-navigate-to-base-path` | Keyword match only — not Tabs-specific |
| `@8x8/pui-observability-react-router` | Routing analytics — not Tabs-specific |

---

_Source: Oxygen MCP + Figma (file `5YihJ5WuDvnvrlrRMC4sBp`) · Spec produced by doc-rewrite · Rubric v1.0 · 2026-04-30_
