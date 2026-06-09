---
component: SkeletonBlock
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
  - "[[SkeletonBlock/examples]]"
  - "[[SkeletonBlock/tokens]]"
  - "[[SkeletonBlock/accessibility]]"
  - "[[SkeletonBlock/SkeletonBlock-figma]]"
  - "[[SkeletonBlock/SkeletonBlock-audit]]"
tags:
  - oxygen
  - component/SkeletonBlock
  - role/props
  - stage/blocked
  - category/feedback_status
---
# SkeletonBlock — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md) · [SkeletonBlock-figma.md](SkeletonBlock-figma.md)

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

## Props — SkeletonBlock

> **SOURCE GAP:** `get-component-props` returned no prop definitions for `SkeletonBlock`. The following variant axes were extracted from Figma (node `31984:56109`) and represent the known configuration surface; React prop names may differ.

| Prop (Figma axis) | Type | Default | Notes |
|---|---|---|---|
| `mode` | `"Light" \| "Dark"` | `"Light"` | Theme mode. In Oxygen apps, typically driven by the theme provider rather than set directly. |
| `size` | see values below | `"40px - heading02"` | Controls the height of the skeleton block. Use the value matching the text style or element being replaced. |

### `size` values (SkeletonBlock)

| Value | Height | Intended use |
|---|---|---|
| `40px - heading02` | 40px | Replaces a `heading02` text element |
| `28px - heading01` | 28px | Replaces a `heading01` text element |
| `24px - bulletList01` | 24px | Replaces a `bulletList01` text element |
| `22px - body02` | 22px | Replaces a `body02` text element |
| `20px - body01` | 20px | Replaces a `body01` text element |
| `16px - label01` | 16px | Replaces a `label01` text element |
| `custom - image` | 240px | Replaces an image or block-level element |

---

## Props — SkeletonCircle

> **SOURCE GAP:** `get-component-props` returned no prop definitions for `SkeletonCircle`. The following size variants were derived from usage documentation.

| Prop | Type | Default | Notes |
|---|---|---|---|
| `size` | see values below | — | Controls the diameter of the circle skeleton. |

### `size` values (SkeletonCircle)

| Value | Diameter | Intended use |
|---|---|---|
| `xlarge` | 80px | Extra-large avatar |
| `large` | 48px | Large avatar |
| `medium` | 40px | Medium avatar |
| `small` | 32px | Small avatar |
| `small` (alt) | 28px | Small icon |
| `xsmall` | 24px | Extra-small icon |
| `xsmall` (alt) | 22px | Extra-small icon |
| `xsmall` (alt) | 20px | Extra-small icon |
| `xsmall` (alt) | 16px | Extra-small icon |

---

## Slots / events

No slots or event callbacks defined. Both components are purely presentational.

---

_Source: Oxygen MCP · Extracted 2026-05-05_
