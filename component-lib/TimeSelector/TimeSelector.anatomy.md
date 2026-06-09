---
parent: "[[TimeSelector]]"
section: anatomy
component: TimeSelector
pipeline_stage: draft
tags:
  - oxygen
  - component/TimeSelector
  - role/spoke
  - section/anatomy
  - category/date_time
---

<!-- source: figma-only -->

## Anatomy

Element structure extracted from the Figma layer tree (node `28996:49849`, frame "Time select").

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | frame | `_base_form_label` | optional slot | Controlled by `Show Label` boolean (default: true). Contains label text, required asterisk, and info icon button. |
| 1a | text | Label text | content | Typography: `$body01`, `--text/textcolor01` |
| 1b | text | Required asterisk (*) | content | Typography: `$bodyBold01`, `--error/error01`. Always red. |
| 1c | instance | Icon Button | fixed sub-component | Info/FAQ icon (`iconSizeM`). Wraps to tooltip/help pattern. |
| 2 | frame | `_Text input` | fixed | The time input field itself. Always present. |
| 2a | frame | `Input Text` | structural | Background container. Carries state-dependent background and border. |
| 2b | frame | `Text → Text Wrap` | content | Holds displayed time value or placeholder. |
| 2c | frame | `Type indicator` (hidden) | optional slot | 1 px × 24 px cursor bar. Visible only in Focus state. |
| 2d | frame | `Focus ring` (hidden) | optional slot | Absolute overlay, 2 px border. Visible only in Focus state. |
| 3 | frame | `_base_form_hint` | optional slot | Controlled by `Show Hint` boolean (default: true). Hint text below input. |
| 4 | frame | `Error Area` | conditional | Shown only when `Error=True`. Contains error icon (16 × 16) + error message text. |

### Sub-component: Icon Button (label area)

| # | Type | Name | Role | Notes |
|---|------|------|------|-------|
| 1 | container | Icon Button | interactive | 2 px padding, 6 px border-radius (hardcoded). Reveals tooltip/help info. |
| 1a | instance | TypeIcon | content | Swap slot — FAQ/help icon at `iconSizeM`. |

---

## Variants / Sizes

### Size axis

<!-- CONFLICT:GAP-001 finding="Figma component set exposes Size=Large (48px height, 120px width, 16px H / 12px V padding, $body02 typography). The TimeSelectorSize enum in the code API only has 'small' | 'default'. 'default' maps to Figma Medium. Large is entirely absent from the API." HUMAN DECISION REQUIRED -->
<!-- CONFLICT:GAP-002 finding="Figma default size is Large (confirmed via Desktop Bridge componentPropertyDefinitions). Code default for size prop is 'default' (≡ Medium). The rendered output when no size is specified differs between Figma and code." HUMAN DECISION REQUIRED -->

| Figma size | Code `size` value | Input height | Input width | Padding | Font style |
|------------|-------------------|-------------|-------------|---------|------------|
| Small | `"small"` | 32 px | 80 px | 8 px all | `$label01` 12 px / lh 16 px |
| Medium | `"default"` *(code default)* | 40 px | 97 px | 12 px H / 8 px V | `$body01` 14 px / lh 20 px |
| Large | *(not in code API — Figma default)* | 48 px | 120 px | 16 px H / 12 px V | `$body02` 16 px / lh 24 px |

**Remaining Figma variant axes:**

| Property | Values | Figma default | Notes |
|----------|--------|---------------|-------|
| Mode | Light, Dark | Light | Theme mode |
| State | Rest, Focus, Disabled | Rest | Persistent interaction states |
| Error | False, True | False | Adds red border + Error Area |
| Filled | No, Yes | No | Whether a time value is filled in |

**Boolean toggles:**

| Property | Default | Notes |
|----------|---------|-------|
| `Show Label` | true | Shows/hides `_base_form_label` (label + asterisk + icon) |
| `Show Hint` | true | Shows/hides `_base_form_hint` hint text below input |

**Text properties:**

| Property | Default |
|----------|---------|
| `Error text` | `"Error message goes here."` |

---

## Interaction states

| State | Trigger | Visual change |
|-------|---------|---------------|
| Rest | Default | `--ui/ui05` background, no border |
| Focus | Keyboard `Tab` / click | `--interactive/focus01` 2 px ring overlay + 1 px type-cursor bar |
| Disabled | `isDisabled=true` | `--interactive/disabled01` background, `--interactive/disabled04` text, no interaction |
| Error (Rest) | `hasError=true` | `--error/error01` 2 px border + Error Area shown below |
| Error (Focus) | Focus while `hasError=true` | Both focus ring and error border visible |
| Filled | Value selected | Time value shown in `--text/textcolor02` |

---

## Structure & spacing

### Container

| Size | Total height |
|------|-------------|
| Small | 76 px (label + 32 px input + hint) |
| Medium | 84 px (label + 40 px input + hint) |
| Large | 92 px (label + ~48 px input + hint) |

### Input field

| Property | Small | Medium | Large | Token |
|----------|-------|--------|-------|-------|
| Height | 32 px | 40 px | 48 px | Hardcoded |
| Width | 80 px | 97 px | 120 px | Hardcoded |
| Padding | 8 px all | 12 px H / 8 px V | 16 px H / 12 px V | Hardcoded |
| Border radius | 6 px | 6 px | 6 px | Hardcoded — no token binding found |

### Internal spacing

| Property | Value | Token |
|----------|-------|-------|
| Gap (label → input → hint) | 4 px | Hardcoded |
| Gap (elements within input row) | 8 px | Hardcoded |
| Error area gap (icon → text) | 4 px | Hardcoded |
| Icon Button padding | 2 px | Hardcoded |
| Error icon size | 16 × 16 px | Hardcoded |

Auto-layout direction: vertical (column) — label → input → hint/error stacked; input internal: horizontal.

---

## Accessibility (from Figma annotations only)

- **ARIA role:** <!-- NOT ANNOTATED IN FIGMA -->
- **Focus order:** <!-- NOT ANNOTATED IN FIGMA -->
- **Keyboard interactions:** <!-- NOT ANNOTATED IN FIGMA -->

<!-- STUB:GAP-009 source="Request designer to add accessibility annotations to the Figma component for ARIA role, keyboard interactions, and focus order." -->

See [[TimeSelector.accessibility]] for the full accessibility specification (inferred from conventions — not from Figma annotations or OX MCP).

---

## Design decisions & annotations

> **Time select — Node 28996:49849:**
> Documentation reference: https://oxygen.8x8.com/docs/components/timeselector/usage

> **Focus ring — Node 81242:2239:**
> "A focus ring is used to indicate the currently focused item."

> **Icon Button (label area) — Node 28172:41855:**
> Icon Button. Documentation: https://zeroheight.com/714056d2f/p/75909b-icons/b/1725fe

---

## Gaps & conflicts

| Type | Description |
|------|-------------|
| CONFLICT (GAP-001) | Figma `Size=Large` has no matching code API value; `size="default"` corresponds to Figma `Medium` |
| CONFLICT (GAP-002) | Figma default size is `Large`; code default is `"default"` (Medium) — different defaults |
| SOURCE_GAP (GAP-009) | No ARIA role, keyboard map, or focus order documented in Figma annotations |
| Missing token | `Input Text.border-radius` is hardcoded 6 px — no design token binding |
| Missing token | `Icon Button.border-radius` is hardcoded 6 px — no design token binding |
| Missing token | All spacing values (padding, gap) are hardcoded — no token bindings observed |
