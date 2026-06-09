---
parent: "[[SlideOut]]"
section: composition
pipeline_stage: spec_ready
tags:
  - oxygen
  - component/SlideOut
  - role/composition
---

<!-- STUB:GAP-001 source="No SlideOut-figma.md exists (no Figma design). Composition patterns below are inferred from source/props.md and source/examples.md. Replace with figma-extract output once a Figma source is authored." -->

## Subcomponents

SlideOut has no built-in subcomponents. It is a thin container — it ships no header, footer, close button, or scrim. Consuming applications compose those elements inside `children`.

## Common consumer patterns

| Pattern | How |
|---|---|
| Panel header + close button | Compose inside `children`; not a component-provided slot |
| Scrollable content body | Wrap children in `<div style={{ overflowY: 'auto', flex: 1 }}>` |
| Resizable inspector | `isResizable` + `defaultWidth` / `minWidth` / `maxWidth` + `onResize` callback |
| Controlled open/close | External `useState` → `isVisible`; trigger button with `aria-expanded` |

## Relationship to related components

| Component | Relationship |
|---|---|
| [[Modal]] | Peer — use Modal for blocking decisions requiring explicit user action; SlideOut for non-blocking supplementary content |
| [[Drawer]] | Peer — use Drawer for persistent primary navigation; SlideOut for intent-driven, dismissible panels |
| [[Tooltip]] | Peer — use Tooltip for single-line contextual hints; SlideOut for panels with actionable or scrollable content |
