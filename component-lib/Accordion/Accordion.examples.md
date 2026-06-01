---
parent: "[[Accordion]]"
section: examples
---

> **WARN-001:** All examples below are derived from prop documentation, usage guidelines, and Figma annotations — the Oxygen MCP returned 0 clean Storybook examples. Import paths (e.g. `@8x8/oxygen-icons`, `@8x8/oxygen-icon-button`) have not been verified against a running Storybook. Validate before publishing.

## Basic group

```tsx
import { Accordion, AccordionGroup } from '@8x8/oxygen-accordion';

<AccordionGroup>
  <Accordion title="Section 1">Content for section 1</Accordion>
  <Accordion title="Section 2">Content for section 2</Accordion>
  <Accordion title="Section 3">Content for section 3</Accordion>
</AccordionGroup>
```

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

## With secondary text and leading icon

```tsx
import { Accordion } from '@8x8/oxygen-accordion';
import { VideoIcon } from '@8x8/oxygen-icons';

<Accordion title="Recording" text="Today, 11:48" iconLeft={<VideoIcon />}>
  <p>Recording content here</p>
</Accordion>
```

## Custom trigger — `expandTrigger="arrow"`

Use when `contentAfterTitle` contains interactive elements.

```tsx
import { Accordion } from '@8x8/oxygen-accordion';
import { IconButton } from '@8x8/oxygen-icon-button';
import { MoreIcon } from '@8x8/oxygen-icons';

<Accordion
  title="Accordion title"
  expandTrigger="arrow"
  contentAfterTitle={
    <IconButton icon={<MoreIcon />} aria-label="More options" onClick={handleMore} />
  }
>
  Content here
</Accordion>
```

## Fixed-height group (one open at a time)

```tsx
<AccordionGroup
  hasFixedHeight
  initialActiveElementId="section-2"
  onChange={(id, isExpanded) => console.log(id, isExpanded)}
>
  <Accordion id="section-1" title="Section 1">Long scrollable content...</Accordion>
  <Accordion id="section-2" title="Section 2">Long scrollable content...</Accordion>
  <Accordion id="section-3" title="Section 3">Long scrollable content...</Accordion>
</AccordionGroup>
```

## Forced height on a standalone accordion

`forcedHeight` caps a single accordion's content area independently of `AccordionGroup.hasFixedHeight`. Other accordions in the same group can still be open simultaneously.

```tsx
<Accordion title="Long content section" forcedHeight={200} isContentScrollable={true}>
  <p>Line 1</p>
  {/* … many lines … */}
</Accordion>
```

## Nested accordion (max 2 levels)

```tsx
<AccordionGroup>
  <Accordion title="Parent section">
    <AccordionGroup>
      <Accordion title="Child section A">Nested content A</Accordion>
      <Accordion title="Child section B">Nested content B</Accordion>
    </AccordionGroup>
  </Accordion>
</AccordionGroup>
```

## Without padding in content area

```tsx
<Accordion title="No padding" hasPadding={false}>
  <div style={{ padding: 0 }}>Custom padded content</div>
</Accordion>
```

## Custom translations (i18n)

```tsx
<Accordion
  title="Settings"
  translations={{ expand: 'Expand Settings section', collapse: 'Collapse Settings section' }}
>
  Settings content
</Accordion>
```

## Blocking `AccordionGroup.onChange`

Return `false` to prevent an accordion from opening.

```tsx
<AccordionGroup
  onChange={(id) => {
    if (id === 'locked-section') return false;
    return true;
  }}
>
  <Accordion id="normal-section" title="Normal">Content</Accordion>
  <Accordion id="locked-section" title="Locked">Hidden content</Accordion>
</AccordionGroup>
```

## Dark mode and theming

Dark mode is controlled via CSS custom properties, not a component prop. The Accordion resolves design tokens automatically when the Oxygen theme class is applied to a parent element. There is no `mode` or `theme` prop — apply theming at the application level. See [[Accordion.tokens]] for resolved values.
