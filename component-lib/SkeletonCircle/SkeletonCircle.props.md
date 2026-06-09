---
parent: "[[SkeletonCircle]]"
section: props
component: SkeletonCircle
package: "@8x8/oxygen-skeletons"
role: spoke
pipeline_stage: draft
tags:
  - oxygen
  - component/SkeletonCircle
  - role/props
  - stage/draft
---

## Package

```
@8x8/oxygen-skeletons
```

**Components exported:** `SkeletonBlock`, `SkeletonCircle`

### Installation

```bash
# yarn
$ yarn add @8x8/oxygen-skeletons

# npm
$ npm install @8x8/oxygen-skeletons
```

> **Registry prerequisite:** You must be connected to the 8x8 VPN to access the Artifactory registry.
>
> Add to `.npmrc`:
> ```
> @8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
> ```

---

## Props — SkeletonCircle

<!-- STUB:GAP-002 source="Check @8x8/oxygen-skeletons source for all exported SkeletonCircle props, types, and defaults. Replace Figma-axis props with confirmed React props. Remove mode if not a React prop." -->

> **SOURCE GAP (GAP-002):** `get-component-props` returned no prop definitions for `SkeletonCircle`. The following variant axes were extracted from Figma (node `31984:56124`) and represent the known configuration surface; React prop names and types may differ. All props are unconfirmed.

<!-- CONFLICT:GAP-001 finding="SkeletonCircle/props.md uses Figma axis format (80px - xlarge, 40px - medium, etc.) while SkeletonBlock/props.md references SkeletonCircle using short labels (xlarge, medium). React prop enum format unverified. One format is incorrect." HUMAN DECISION REQUIRED -->

| Prop (Figma axis) | Type | Default | Notes |
|---|---|---|---|
| `mode` | `"Light" \| "Dark"` | `"Light"` | Theme mode. In Oxygen apps, likely driven by the theme provider rather than set directly on the component. |
| `size` | see values below | `"80px - xlarge"` | Controls the diameter of the circle. Use the value matching the avatar or icon size being replaced. **Format unverified** — see GAP-001. |

<!-- STUB:GAP-008 source="Confirm via @8x8/oxygen-skeletons source whether mode is a React prop. If not, remove from this table and add a theming note. Depends on GAP-002." -->

### `size` values

<!-- STUB:GAP-007 source="Resolve via GAP-001 source check. If short labels are the React API, document how 32px vs 28px are distinguished. If Figma axis format is correct, the px value disambiguates." -->

| Value | Diameter | Size label | Intended use |
|---|---|---|---|
| `80px - xlarge` | 80px | xlarge | Extra-large avatar |
| `48px - large` | 48px | large | Large avatar |
| `40px - medium` | 40px | medium | Medium avatar |
| `32px - small` | 32px | small | Small avatar |
| `28px - small` | 28px | small | Small icon |
| `24px - xsmall` | 24px | xsmall | Extra-small icon |
| `22px - xsmall` | 22px | xsmall | Extra-small icon |
| `20px - xsmall` | 20px | xsmall | Extra-small icon |
| `16px - xsmall` | 16px | xsmall | Extra-small icon |

> **Two "small" sizes and four "xsmall" sizes:** Both 32px and 28px map to the `small` label; 24/22/20/16px all map to `xsmall`. The px value is the disambiguating factor if the Figma axis format is correct. If the React API uses short labels only, the enum definition must specify how these are distinguished.

---

## Slots / events

No slots or event callbacks defined. `SkeletonCircle` is purely presentational.

---

_Source: Oxygen MCP · Figma design context (node 31984:56124) · Extracted 2026-05-05_
