---
parent: "[[Select]]"
section: composition
component: Select
pipeline_stage: doc_rewrite
audit_verdict: NO
tags:
  - oxygen
  - component/Select
  - role/composition
  - stage/doc_rewrite
---

<!-- STUB:GAP-001 source="Run figma-extract Select (node 2105:2, file 5YihJ5WuDvnvrlrRMC4sBp) to extract the composition section — specifically the leading-visuals frame (node 69857:19373) showing icon/status/avatar options, and any annotation about sub-component containment." -->

## Sub-components

Select exports named sub-components that override react-select internals via the `components` prop:

| Export | Replace to | When to use |
|--------|------------|-------------|
| `VirtualMenuList` | `components={{ MenuList: VirtualMenuList }}` | Datasets with 1000+ options — prevents scroll jank via `react-window` virtualised rendering |
| `ClearIndicator` | `components={{ ClearIndicator: MyIndicator }}` | Custom clear (×) button styling or behaviour |
| `DropdownIndicator` | `components={{ DropdownIndicator: MyIndicator }}` | Custom dropdown chevron |
| `SingleValue` | `components={{ SingleValue: MyValue }}` | Custom selected value display in single-select mode |
| `MultiValue` | `components={{ MultiValue: MyValue }}` | Custom chip display in multi-select mode |
| `ValueContainer` | `components={{ ValueContainer: MyContainer }}` | Custom wrapper around selected values |

```tsx
import Select, { VirtualMenuList, ClearIndicator } from '@8x8/oxygen-select';

<Select
  options={options}
  components={{
    MenuList: VirtualMenuList,
    ClearIndicator: MyClearIndicator,
  }}
/>
```

## Pattern membership

| Pattern | Role |
|---------|------|
| [[Form]] | Standard form control — appears in form layouts alongside Label, TextField, Checkbox |
| [[Modal]] | Select-in-Modal requires `menuPortalTarget` to avoid clipping (see [[Select.usage]]) |

## Relationships

- **Related:** [[Radio]], [[Checkbox]] — for ≤5 options; Select is the alternative for longer lists
- **Related:** [[ToggleButton]] — for instant-effect binary settings (not value-picking)
- **Related:** [[Tooltip]] — the `infoBoxText` prop renders an Oxygen Tooltip on the ⓘ button
- **Subcomponent consumer:** None — Select is not structurally contained inside other Oxygen components
