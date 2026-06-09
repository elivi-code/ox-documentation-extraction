---
parent: "[[Label]]"
section: composition
---

<!-- source: figma-only -->

## Subcomponents

`Label` internally renders an [[Icon Button]] when the info box feature is used. The Icon Button is an instance-swap slot inside the Figma `_base_form_label` component.

| Sub-component | Usage | Notes |
|---|---|---|
| [[Icon Button]] | Info/help trigger button | Shown when `infoBoxText` is set; icon is `TypeIcon` at `iconSizeM` |

## Common pairings

Label is nearly always paired with a form control. It does not contain other Oxygen components — the pairing is structural (Label above the control in the DOM), not compositional:

| Component | Relationship | Notes |
|-----------|-------------|-------|
| [[Input]] | Most common pairing — Label names the Input field | `htmlFor` on Label matches `id` on Input |
| [[Checkbox]] | Checkbox bundles its own internal label via its `label` prop — do not wrap with this Label | See Checkbox docs for the correct pattern |
| [[Select]] | Label names the Select field via `htmlFor` | Same pattern as Input |
| [[Button]] | For primary actions — not embedded in Label | Use the `action` prop slot for secondary field-scoped links only |
| [[Tooltip]] | Label's overflow tooltip and info box are self-contained | No separate Tooltip component needed |

## Patterns

| Pattern | Role of Label |
|---------|---------------|
| [[Form]] | Canonical ingredient — every form field uses a Label above its control |

## What Label does NOT contain

The `action` prop adds an inline link as a sibling to the label text, but it is rendered as a native `<a>` / action element, not a Button or Link component from the Oxygen library.

_Source: Figma MCP · Oxygen MCP · Extracted 2026-05-01_
