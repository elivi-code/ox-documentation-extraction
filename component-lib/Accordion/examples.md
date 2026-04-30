# Accordion — Examples

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) · [accessibility.md](./accessibility.md) · [accordion-figma.md](./accordion-figma.md)

---

> **Note:** The Oxygen MCP returned 0 clean Storybook examples for the `accordion` package.
> The examples below are derived from prop documentation, usage guidelines, and Figma annotations.

---

## Basic group

```tsx
import { Accordion, AccordionGroup } from '@8x8/oxygen-accordion';

<AccordionGroup>
  <Accordion title="Section 1">
    Content for section 1
  </Accordion>
  <Accordion title="Section 2">
    Content for section 2
  </Accordion>
  <Accordion title="Section 3">
    Content for section 3
  </Accordion>
</AccordionGroup>
```

---

## Controlled expansion

```tsx
const [isOpen, setIsOpen] = useState(false);

<Accordion
  title="My Accordion"
  isExpanded={isOpen}
  onChange={(id, expanded) => setIsOpen(expanded)}
>
  Content here
</Accordion>
```

---

## With secondary text and leading icon

```tsx
import { Accordion } from '@8x8/oxygen-accordion';
import { VideoIcon } from '@8x8/oxygen-icons';

<Accordion
  title="Recording"
  text="Today, 11:48"
  iconLeft={<VideoIcon />}
>
  <p>Recording content here</p>
</Accordion>
```

---

## Custom trigger mode — `expandTrigger="arrow"`

Use when `contentAfterTitle` contains interactive elements (e.g. `IconButton`).
With `expandTrigger="header"` (the default), interactive content in `contentAfterTitle`
would conflict with the header click handler.

```tsx
import { Accordion } from '@8x8/oxygen-accordion';
import { IconButton } from '@8x8/oxygen-icon-button';
import { MoreIcon } from '@8x8/oxygen-icons';

<Accordion
  title="Accordion title"
  expandTrigger="arrow"
  contentAfterTitle={
    <IconButton
      icon={<MoreIcon />}
      aria-label="More options"
      onClick={handleMore}
    />
  }
>
  Content here
</Accordion>
```

---

## Fixed-height group (one open at a time)

In this mode the group fills its parent container's height and the open accordion's
content panel fills the remaining space. Content becomes scrollable automatically.

```tsx
<AccordionGroup
  hasFixedHeight
  initialActiveElementId="section-2"
  onChange={(id, isExpanded) => console.log(id, isExpanded)}
>
  <Accordion id="section-1" title="Section 1">
    Long scrollable content...
  </Accordion>
  <Accordion id="section-2" title="Section 2">
    Long scrollable content...
  </Accordion>
  <Accordion id="section-3" title="Section 3">
    Long scrollable content...
  </Accordion>
</AccordionGroup>
```

---

## Nested accordion (max 2 levels)

The design system supports a maximum of two nested accordion levels.

```tsx
<AccordionGroup>
  <Accordion title="Parent section">
    <AccordionGroup>
      <Accordion title="Child section A">
        Nested content A
      </Accordion>
      <Accordion title="Child section B">
        Nested content B
      </Accordion>
    </AccordionGroup>
  </Accordion>
</AccordionGroup>
```

---

## Without padding in content area

```tsx
<Accordion title="No padding" hasPadding={false}>
  <div style={{ padding: 0 }}>Custom padded content</div>
</Accordion>
```

---

## Custom translations (i18n)

```tsx
<Accordion
  title="Settings"
  translations={{
    expand: 'Expand Settings section',
    collapse: 'Collapse Settings section',
  }}
>
  Settings content
</Accordion>
```

---

## Blocking navigation from `AccordionGroup.onChange`

Return `false` from `AccordionGroup.onChange` to prevent an accordion from opening.

```tsx
<AccordionGroup
  onChange={(id, isExpanded) => {
    if (id === 'locked-section') return false; // blocks open
    return true; // allows
  }}
>
  <Accordion id="normal-section" title="Normal">Content</Accordion>
  <Accordion id="locked-section" title="Locked">Hidden content</Accordion>
</AccordionGroup>
```

---

_Source: Oxygen MCP + usage guidelines · Extracted 2026-04-28_
