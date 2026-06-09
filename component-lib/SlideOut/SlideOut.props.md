---
parent: "[[SlideOut]]"
section: props
pipeline_stage: spec_ready
tags:
  - oxygen
  - component/SlideOut
  - role/props
---

## Props

| Name | Type | Default | Required | Description | Accepts |
|---|---|---|---|---|---|
| `children` | `ReactNode` | — | yes | Component content | — |
| `isVisible` | `boolean` | — | no | Whether the slide-out panel is visible | — |
| `isResizable` | `boolean` | — | no | Whether the panel can be resized by dragging | — |
| `hasAnimation` | `boolean` | — | no | _(no description in MCP source — see GAP-004)_ | — |
| `defaultWidth` | `number` | — | no | _(no description in MCP source — see GAP-004; unit assumed px per WARN-001)_ | — |
| `minWidth` | `number` | — | no | _(no description in MCP source — see GAP-004; unit assumed px per WARN-001)_ | — |
| `maxWidth` | `number` | — | no | _(no description in MCP source — see GAP-004; unit assumed px per WARN-001)_ | — |
| `className` | `string` | — | no | CSS class name for the root element | — |
| `testId` | `string` | — | no | Test ID for automated testing | — |

<!-- STUB:GAP-004 source="Obtain descriptions for hasAnimation, defaultWidth, minWidth, maxWidth from @8x8/oxygen-slide-out component source, JSDoc comments, or Storybook argTypes. Specify units (px vs CSS value) for all three width props." -->
<!-- SKIP:GAP-006 manual="Default values require component source, Storybook controls panel, or argTypes — not available in MCP extract. Populate the Default column from those sources and update source/props.md." -->

## Observed but undocumented props

The prop below was observed in the Storybook documentation story but is absent from the MCP props registry. Treat as provisional until confirmed from source.

| Name | Type | Description | Accepts |
|---|---|---|---|
| `onResize` | `(newWidth: number) => void` | Callback fired when the panel is resized; receives the new width in pixels — _inferred from Storybook story_ | — |

<!-- STUB:GAP-005 source="Confirm whether onResize is a documented public prop by checking component source or TypeScript types. If confirmed, move to the main props table with type signature and description." -->
