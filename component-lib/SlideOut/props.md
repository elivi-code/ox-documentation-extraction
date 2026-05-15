---
component: SlideOut
package: "@8x8/oxygen-slide-out"
category: layout_overlay
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: PARTIAL
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - audit
siblings:
  - "[[SlideOut/examples]]"
  - "[[SlideOut/tokens]]"
  - "[[SlideOut/accessibility]]"
  - "[[SlideOut/SlideOut-usage]]"
  - "[[SlideOut/SlideOut-audit]]"
tags:
  - oxygen
  - component/SlideOut
  - role/props
  - stage/spec_ready
  - category/layout_overlay
---
# SlideOut — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```sh
# yarn
$ yarn add @8x8/oxygen-slide-out

# npm
$ npm install @8x8/oxygen-slide-out
```

> **Registry prerequisite:** Add the 8x8 Artifactory registry to your `.npmrc` or `.yarnrc.yml` before installing. VPN access is required.
>
> `.npmrc`:
> ```
> @8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
> ```

## Package

`@8x8/oxygen-slide-out`

## Props

| Prop | Type | Required | Default | Description |
|------|------|----------|---------|-------------|
| `children` | `ReactNode` | yes | — | Component content |
| `isVisible` | `boolean` | no | — | Whether the slide-out panel is visible |
| `isResizable` | `boolean` | no | — | Whether the panel can be resized by dragging |
| `hasAnimation` | `boolean` | no | — | _(no description in MCP — see SOURCE_GAP note below)_ |
| `defaultWidth` | `number` | no | — | _(no description in MCP — see SOURCE_GAP note below)_ |
| `minWidth` | `number` | no | — | _(no description in MCP — see SOURCE_GAP note below)_ |
| `maxWidth` | `number` | no | — | _(no description in MCP — see SOURCE_GAP note below)_ |
| `className` | `string` | no | — | CSS class name for the root element |
| `testId` | `string` | no | — | Test ID for automated testing |

## Observed but undocumented props

The following prop was observed in the Storybook documentation story but is **not listed** in the MCP props registry. It may be an omission from the source.

| Prop | Type | Description |
|------|------|-------------|
| `onResize` | `(newWidth: number) => void` | Callback fired when the panel is resized; receives the new width in pixels |

> **SOURCE_GAP:** `hasAnimation`, `defaultWidth`, `minWidth`, `maxWidth` — descriptions are empty in the MCP source. `onResize` is present in the example story but absent from the props definition.

_Source: Oxygen MCP · Extracted 2026-05-05_
