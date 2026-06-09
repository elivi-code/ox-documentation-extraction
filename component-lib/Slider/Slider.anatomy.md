---
component: Slider
parent: "[[Slider]]"
section: anatomy
role: spoke
pipeline_stage: spec_ready
audit_verdict: PARTIAL
siblings:
  - "[[Slider]]"
  - "[[Slider.props]]"
  - "[[Slider.tokens]]"
  - "[[Slider.usage]]"
  - "[[Slider.accessibility]]"
  - "[[Slider.platform]]"
  - "[[Slider.composition]]"
tags:
  - oxygen
  - component/Slider
  - role/spoke
  - section/anatomy
  - stage/spec_ready
---

<!-- STUB:GAP-001 source="Run figma-extract targeting file 5YihJ5WuDvnvrlrRMC4sBp node 22902:37514 to produce source/slider-figma.md — then re-run doc-rewrite to populate this spoke" -->

> **Anatomy data unavailable.** `slider-figma.md` was not produced by `figma-extract` (audit GAP-001, blocker). The section below is derived from partial Figma data embedded in `source/tokens.md` and `source/examples.md` during the combined extraction session. Run `figma-extract` against node `22902:37514` to produce the canonical anatomy file and replace this stub.

## Known elements (from partial Figma data)

The Figma reference pattern is named **"Audio Volume"** (node `22902:37514`, file `5YihJ5WuDvnvrlrRMC4sBp`).

| Element | Description |
|---------|-------------|
| Label | Optional text above the slider row (`--text/textcolor01` / `--interactive/disabled01`) |
| Left icon | Optional icon to the left of the track (e.g. `volume-off`, 20×20 px) |
| Track | Horizontal bar split into active (left) and inactive (right) segments, height 4 px, border-radius 4 px |
| Active track fill | Colour shifts by state: `--ui/ui04` (Default/Hover), `--actions/action01` (Active/Focus), `--interactive/disabled04` (Disabled) |
| Inactive track fill | SVG image asset — token not resolved (see [[Slider.tokens]] GAP-005) |
| Thumb (Handle) | Draggable knob: 16 px default, 32 px Hover/Active (with ripple overlay), 24 px Focus |
| Right icon | Optional icon to the right of the track (e.g. `volume-up`, 20×20 px) |
| Focus ring | 2 px solid border + 4 px inner shadow on thumb, border-radius 1000 px |

## Modes / functional variants

| Mode | Prop | `value` shape |
|------|------|--------------|
| Single-thumb | (default) | `number` |
| Range (two-thumb) | `isMultiple` | `[number, number]` |
| Track-draggable range | `isMultiple` + `isTrackDraggable` | `[number, number]` |

## States

| State | Track fill | Thumb size | Thumb appearance |
|-------|------------|------------|------------------|
| Default | `--ui/ui04` | 16 px | Normal |
| Hover | `--ui/ui04` | 32 px | + ripple overlay |
| Active | `--actions/action01` | 32 px | + ripple overlay |
| Focus | `--actions/action01` | 24 px | + focus ring |
| Disabled | `--interactive/disabled04` | 16 px | Muted SVG asset |

States apply in both **Light** and **Dark** modes (token values differ — see [[Slider.tokens]]).

## Figma source

- File: `5YihJ5WuDvnvrlrRMC4sBp` (UI-components)
- Node: `22902:37514` ("Audio Volume")
- Figma URL: `https://www.figma.com/file/5YihJ5WuDvnvrlrRMC4sBp?node-id=22902:37514`

_Source: Partial — derived from source/tokens.md + source/examples.md (Figma data embedded during combined extraction 2026-04-29). Full anatomy pending figma-extract run._
