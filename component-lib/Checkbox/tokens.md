---
component: Checkbox
package: "@8x8/oxygen-checkbox"
category: form_inputs
role: tokens
role_description: "Design tokens — color, spacing, and typography token bindings"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Checkbox/props]]"
  - "[[Checkbox/examples]]"
  - "[[Checkbox/accessibility]]"
  - "[[Checkbox/checkbox-figma]]"
  - "[[Checkbox/checkbox-pui]]"
  - "[[Checkbox/checkbox-audit]]"
tags:
  - oxygen
  - component/Checkbox
  - role/tokens
  - stage/spec_ready
  - category/form_inputs
---
# Checkbox — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

> **Data gap:** The Oxygen MCP returned 0 theme token matches for the `checkbox` search term.
> The Figma variables API was inaccessible (permissions). No checkbox-specific design tokens could
> be extracted from either source. The spacing references below come verbatim from usage documentation.

---

## Spacing tokens (from documentation text)

| Usage | Token | Notes |
|-------|-------|-------|
| Between group label and first checkbox | `$spacing04` | Verbatim from anatomy docs |
| Between checkbox labels (vertical list) | `$spacing03` | Verbatim from anatomy docs |

---

## Color palette (available in design system)

No checkbox-specific semantic color tokens were returned by the MCP. The full design system
color palette includes these base ramps (resolved hex values from Oxygen MCP):

| Ramp | Key values |
|------|-----------|
| Blue | blue01 `#00112D` … blue10 `#D7E3F9` |
| Gray | gray01 `#141414` … gray10 `#F1F1F1` |
| Red | red01 `#29070A` … red10 `#FAEAEC` |
| Green | green01 `#062715` … green10 `#E4F8ED` |

Interactive / primary accent: likely `blue05 #0056E0` / `blue06 #246FE5` (inferred from palette, unconfirmed).

---

## Figma variant axes (not tokenised — raw values unavailable)

The following variant axes were found in Figma but no bound token values could be retrieved:

| Axis | Values | Notes |
|------|--------|-------|
| Mode | Light, Dark | Theming dimension |
| State | Rest, Hover | Transient — not API props |
| isChecked | False, True | Matches `isChecked` prop |
| isIndeterminate | False, True | Matches `isIndeterminate` prop |
| isDisabled | False, True | Matches `isDisabled` prop |
| isFocused | False, True | Transient — not API prop |

---

## What to investigate

To get actual token bindings for Checkbox:
1. Enable the Figma Desktop Bridge plugin in the UI-components file
2. Re-run extraction with `figma_get_variables(namePattern="checkbox", resolveAliases=true)`
3. Alternatively search the Oxygen design token source for `checkbox` in the semantic layer

_Source: Oxygen MCP + Figma figma-console MCP · Extracted 2026-04-29_
