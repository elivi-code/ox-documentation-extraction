# Tabs — Examples

> **See also:** [props.md](props.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [figma.md](figma.md)

## Usage

> **Status:** Under review

Tabs are used when a user needs to navigate between content within a page.

---

## Basic usage

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

> **Note:** No clean Storybook code snippets are published via Oxygen MCP for this component. The above is constructed from the prop definitions and usage description.

---

## Color modes

The `color` prop on both `<Tabs>` and `<Tab>` controls the light/dark mode:

```tsx
<Tabs color="dark">
  <Tab value="a" isActive color="dark" onClick={handler}>Label</Tab>
  <Tab value="b" color="dark" onClick={handler}>Label</Tab>
</Tabs>
```

---

## Stretched tabs

Use `isStretched` to make a tab fill available space in the container:

```tsx
<Tabs>
  <Tab value="a" isActive isStretched onClick={handler}>Section 1</Tab>
  <Tab value="b" isStretched onClick={handler}>Section 2</Tab>
</Tabs>
```

---

## Figma Design Usage

The following guidance comes directly from the Figma design documentation for this component.

### Icon prop
Use `icon` when there is a decorative element (visual cue) to reinforce the meaning of the tab. Also used in compact view when the label is hidden due to space constraints.

### Badge prop
Use `badge` when the content of a tab includes a list of notifications.

### hasDropdown prop
This prop is active only when the screen or container size is reduced to the point where only one tab is visible. In this scenario the tabs component activates the dropdown trigger and the `hasDropdown` prop will be enabled. See "Progressive overflow" below.

---

## Behaviour: Progressive overflow

The Tabs component uses **container-based** progressive overflow — not fixed breakpoints. It adapts based on the actual width of the tab container and dynamically calculates how many tabs fit at any given moment.

As the container narrows, tabs collapse into a popover menu **one at a time** from right to left, rather than wrapping or scrolling.

### Stages

| Stage | What happens |
|-------|-------------|
| **Full width** | All tabs visible in a single row |
| **Partial collapse** | Container narrows → trailing tabs hide → `tabsDisclosure` button appears to access hidden tabs |
| **Progressive hiding** | More tabs hide → disclosure consolidates all overflow tabs into a single menu trigger |
| **Single tab (selected as trigger)** | Only the active tab remains → it transforms into a popover trigger (`hasDropdown` prop enabled) → expands to 100% container width → the separate `tabsDisclosure` button is removed |

### Active tab visibility guarantee

The currently selected tab is **always visible** in the main tab bar and is never hidden in the overflow menu. When a user selects a different tab, the system swaps the newly active tab's position with a currently visible tab, which moves to the overflow dropdown.

### Last visible tab responsive behaviour

| State | Behaviour |
|-------|-----------|
| **Pre-collapse** | Tab appears in full, uncompressed form |
| **Fluid width** | When horizontal space is limited, the tab expands to 100% of the remaining container width |
| **Truncation** | If width is insufficient to display the full label, text truncates with an ellipsis; dropdown icon remains visible and interactive |
| **Tooltip reveal** | When label is truncated, a tooltip appears on hover or focus showing the full untruncated text |

---

## Figma links

- **Options / variants:** [Figma – node 2644:70](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=2644-70)
- **Split tabs:** [Figma – node 18531:32925](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=18531-32925)
- **Component set (tabs):** [Figma – node 85651:78740](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=85651-78740)
- **Examples page:** [Figma – node 85697:271849](https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/UI-components?node-id=85697-271849)

---

_Source: Oxygen MCP + Figma (file `5YihJ5WuDvnvrlrRMC4sBp`) · Extracted 2026-04-30_
