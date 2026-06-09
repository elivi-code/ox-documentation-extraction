---
parent: "[[List]]"
section: composition
pipeline_stage: draft
tags:
  - component/List
  - role/composition
---

## Subcomponents

`ListItem` provides a swappable leading visual slot and auto-rendered trailing visual slot:

| Slot | Position | Accepted types | Controlled by |
|------|----------|----------------|---------------|
| Leading visual | Left edge | [[Icon]], [[Avatar]], Status indicator | `leadingType` instance swap; `leadingVisuals?` boolean toggle |
| Trailing — selection | Right edge | Checkmark (Single Action), Radio, Checkbox | `selected?` axis; visibility tied to selection state |
| Trailing — action | Right edge | Sub Menu chevron, Add icon, Remove icon | Variant-specific (Sub Menu, Add Item, Remove Item) |
| Badge | Text row | Badge container | `hasBadge` boolean toggle |

Selection is communicated by trailing icon visibility only — no background colour change occurs when `selected?=true`.

## Variant composition patterns

Eight `ListItem` visual variants exist in Figma. Whether the Destructive, Checkbox, Radio, Collapsible, Add Item, Sub Menu, and Remove Item patterns map to child composition or undocumented props/exports in `@8x8/oxygen-list` is unconfirmed.

<!-- STUB:GAP-004 source="Inspect @8x8/oxygen-list package exports and Storybook stories to confirm how each variant pattern is achieved at the code level; document the confirmed approach (child composition vs. prop/export) here and in List.props.md" -->

## Common usage patterns

| Pattern | Code |
|---------|------|
| Basic contained list | `<List withBackground><ListItem>…</ListItem></List>` |
| Grouped sub-list | `<List isGroup><ListItem>…</ListItem></List>` |
| Ordered list | `<List isOrdered><ListItem>…</ListItem></List>` |
| Interactive navigation row | `<ListItem onClick={fn} isActive>…</ListItem>` |
| Leading icon slot | `<ListItem><Icon />{/* leading visual via instance swap */}</ListItem>` |

_Source: Figma MCP (Desktop Bridge) · Oxygen MCP · Extracted 2026-05-08_
