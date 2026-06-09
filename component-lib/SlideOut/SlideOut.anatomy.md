---
parent: "[[SlideOut]]"
section: anatomy
pipeline_stage: spec_ready
tags:
  - oxygen
  - component/SlideOut
  - role/anatomy
---

<!-- STUB:GAP-001 source="Request Figma design creation for SlideOut from the design owner. Once a Figma node exists, run figma-extract to produce SlideOut-figma.md and re-run doc-rewrite to replace this spoke with confirmed anatomy." -->
<!-- source: figma-only -->

> **No Figma design exists for SlideOut.** Anatomy, variants, and states below are inferred from [source/props.md](source/props.md) and [source/examples.md](source/examples.md). Replace this spoke with `figma-extract` output once a Figma source is authored.

## Anatomy (inferred)

1. **Trigger** — any focusable element outside the panel that sets `isVisible`. The trigger owns the accessible name of the panel and should reflect open/closed state via `aria-expanded`. Not a component part — provided by the consuming application.
2. **Panel container** — the floating side surface that slides in over the trailing edge. Sized between `minWidth` and `maxWidth`, opening at `defaultWidth`. No visual token bindings are available (see [[SlideOut.tokens]]).
3. **Resize handle** _(optional — only when `isResizable={true}`)_ — drag affordance on the leading edge that fires `onResize(newWidth)`. Must have a programmatic accessible name and be keyboard-operable.
4. **Children** — arbitrary React content rendered inside the panel. The component ships no header, footer, or close button; consuming applications compose those inside `children`.
5. **No backdrop / scrim** — SlideOut does not dim or block the rest of the page. This is its distinguishing trait against Modal.

## Variants

No variant axis is documented in the MCP source. The component is configured through props (`isResizable`, `hasAnimation`, `defaultWidth` / `minWidth` / `maxWidth`) rather than named variants.

## States

| State | Trigger |
|---|---|
| Hidden | `isVisible={false}` |
| Visible | `isVisible={true}` |
| Resizing | User dragging the resize handle (only when `isResizable={true}`) |
