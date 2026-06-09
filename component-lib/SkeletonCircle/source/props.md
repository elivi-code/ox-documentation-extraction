---
component: SkeletonCircle
package: "@8x8/oxygen-skeletons"
category: feedback_status
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - figma
  - audit
siblings:
  - "[[SkeletonCircle/examples]]"
  - "[[SkeletonCircle/tokens]]"
  - "[[SkeletonCircle/accessibility]]"
  - "[[SkeletonCircle/SkeletonCircle-figma]]"
  - "[[SkeletonCircle/SkeletonCircle-audit]]"
tags:
  - oxygen
  - component/SkeletonCircle
  - role/props
  - stage/blocked
  - category/feedback_status
---
# SkeletonCircle — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [SkeletonCircle-figma.md](SkeletonCircle-figma.md)

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

> **SOURCE GAP:** `get-component-props` returned no prop definitions for `SkeletonCircle`. The following variant axes were extracted from Figma (node `31984:56124`) and represent the known configuration surface; React prop names may differ.

| Prop (Figma axis) | Type | Default | Notes |
|---|---|---|---|
| `mode` | `"Light" \| "Dark"` | `"Light"` | Theme mode. In Oxygen apps, typically driven by the theme provider rather than set directly. |
| `size` | see values below | `"80px - xlarge"` | Controls the diameter of the circle. Use the value matching the avatar or icon size being replaced. |

### `size` values

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

---

## Slots / events

No slots or event callbacks defined. `SkeletonCircle` is purely presentational.

---

_Source: Oxygen MCP · Figma design context · Extracted 2026-05-05_
