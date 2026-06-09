---
component: TimeSelector
package: "@8x8/oxygen-time-selector"
category: date_time
role: props
role_description: "API props reference — all component properties with types, defaults, and descriptions"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — CONFLICTs must be resolved first"
audit_verdict: "NO"
files_present:
  - props
  - examples
  - tokens
  - accessibility
  - figma
  - audit
siblings:
  - "[[TimeSelector/examples]]"
  - "[[TimeSelector/tokens]]"
  - "[[TimeSelector/accessibility]]"
  - "[[TimeSelector/timeselector-figma]]"
  - "[[TimeSelector/timeselector-audit]]"
tags:
  - oxygen
  - component/TimeSelector
  - role/props
  - stage/blocked
  - category/date_time
---

# TimeSelector — Props

> **See also:** [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Installation

```bash
# yarn
yarn add @8x8/oxygen-time-selector

# npm
npm install @8x8/oxygen-time-selector
```

**Registry prerequisite** — must be on 8x8 VPN and have the Artifactory registry configured:

`.npmrc`:
```
@8x8:registry=https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/
```

`.yarnrc.yml`:
```yaml
npmScopes:
  8x8:
    npmRegistryServer: "https://artifactory.es.8x8.com/artifactory/api/npm/npm-repository/"

nodeLinker: node-modules
```

## Props

| Prop | Type | Default | Required | Description |
|------|------|---------|----------|-------------|
| `value` | `TimeValue` | — | No | Current time value (`{ hours, minutes, seconds }`) |
| `onChange` | `(value: TimeValue) => void` | — | No | Callback fired when the selected time changes |
| `onOpen` | `() => void` | — | No | Callback fired when the picker opens |
| `onClose` | `() => void` | — | No | Callback fired when the picker closes |
| `size` | `TimeSelectorSize` | `"default"` | No | Size variant — see allowed values below |
| `timeDisplayFormat` | `string` | — | No | Format string controlling how the time is displayed in the input |
| `placeholder` | `string` | — | No | Placeholder text shown when no value is selected |
| `hasError` | `boolean` | `false` | No | Puts the input into an error state (red border + error message slot) |
| `isDisabled` | `boolean` | `false` | No | Disables the component — prevents interaction |
| `isLeftIconVisible` | `boolean` | `false` | No | Shows/hides the leading icon inside the input |
| `iconLeft` | `React.ComponentType<IconProps>` | — | No | Icon component rendered on the left side of the input (requires `isLeftIconVisible: true`) |
| `id` | `string` | — | No | HTML `id` attribute on the input element |
| `testId` | `string` | — | No | `data-testid` attribute for automated testing |
| `portalRef` | `React.RefObject<HTMLElement>` | — | No | Ref to a DOM node where the dropdown portal should be rendered |

## Type definitions

### `TimeSelectorSize`

```ts
type TimeSelectorSize = "small" | "default";
```

The `"default"` size corresponds to the **Medium** size in Figma design specs.

> **Note:** Figma exposes a third size (`Large`) that is not reflected in the current code API — see [timeselector-figma.md](timeselector-figma.md) for the Figma spec.

### `TimeValue`

```ts
type TimeValue = {
  hours: number;
  minutes: number;
  seconds: number;
};
```

## Data gaps

- `onChange`, `onOpen`, `onClose` callbacks appear in Storybook examples but are absent from the published props list — descriptions above are inferred from usage.
- `timeDisplayFormat` has no description in the MCP response; accepted format strings are undocumented.
- `hasError` has no description in the MCP response.

_Source: Oxygen MCP · Extracted 2026-05-07_
