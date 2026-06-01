---
parent: "[[Accordion]]"
section: composition
---

## Subcomponents

| Component | Relationship | Notes |
|---|---|---|
| `AccordionGroup` | Container | Groups multiple `Accordion` items; manages shared state, height mode, and default props |

`Accordion` is always a child of `AccordionGroup` when shared state is needed. Can also be used standalone for controlled single-accordion scenarios.

---

## Slots that accept components

| Prop | Accepts | Notes |
|---|---|---|
| `iconLeft` | [[Icon]] | Leading icon in header |
| `contentAfterTitle` | [[IconButton]], [[Tooltip]], any `ReactNode` | Slot after title. Requires `expandTrigger="arrow"` when content is interactive |
| `children` | Any `ReactNode` | Panel content — free slot |

---

## Nesting

Max depth: **two levels**.

```tsx
<AccordionGroup>
  <Accordion title="Parent">       {/* level 1 */}
    <AccordionGroup>
      <Accordion title="Child A">  {/* level 2 — max */}
        Content
      </Accordion>
    </AccordionGroup>
  </Accordion>
</AccordionGroup>
```

Do not nest beyond two levels. For deep hierarchies, use [[Tabs]].

---

## Common patterns

### `expandTrigger="arrow"` + `contentAfterTitle`

Use when the area after the title contains interactive elements. The full-header click would conflict with buttons, so narrow the trigger to the chevron only.

```tsx
<Accordion
  title="Section"
  expandTrigger="arrow"
  contentAfterTitle={<IconButton icon={<MoreIcon />} aria-label="Options" />}
>
  Content
</Accordion>
```

### Blocking `AccordionGroup.onChange`

Return `false` from `onChange` to prevent an accordion from opening.

```tsx
<AccordionGroup onChange={(id) => id === 'locked' ? false : true}>
  <Accordion id="open" title="Open">Content</Accordion>
  <Accordion id="locked" title="Locked">Hidden</Accordion>
</AccordionGroup>
```

### Fixed-height group

`hasFixedHeight` constrains the group to the parent container and enforces single-open behaviour.

```tsx
<AccordionGroup hasFixedHeight initialActiveElementId="a">
  <Accordion id="a" title="A">Long content...</Accordion>
  <Accordion id="b" title="B">Long content...</Accordion>
</AccordionGroup>
```

### Standalone forced height

`forcedHeight` on a single `Accordion` caps only that panel — independent of `hasFixedHeight`. Multiple accordions in the same group can still be open simultaneously.

```tsx
<Accordion title="Capped" forcedHeight={200} isContentScrollable>
  {/* many lines */}
</Accordion>
```

---

## Related

- [[Tabs]] — prefer for deep hierarchies or when all content should be navigable without expand/collapse
- [[Form]] pattern — Accordion commonly used to group form sections
