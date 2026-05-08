---
component: Select
package: "@8x8/oxygen-select"
category: form_inputs
role: accessibility
role_description: "Accessibility — ARIA roles, keyboard interactions, and WCAG 2.1 AA guidance"
pipeline_stage: blocked
pipeline_note: "Audit verdict NO — resolve CONFLICTs before rewrite"
audit_verdict: NO
siblings:
  - "[[Select/props]]"
  - "[[Select/examples]]"
  - "[[Select/tokens]]"
  - "[[Select/select-pui]]"
  - "[[Select/Select-audit]]"
tags:
  - oxygen
  - component/Select
  - role/accessibility
  - stage/blocked
  - category/form_inputs
---
# Select — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md)

> **Note:** The Oxygen MCP returned no explicit accessibility documentation for this component. The guidance below is inferred from the component's interactive nature and standard combobox/listbox patterns.

## ARIA Roles

| Element | ARIA role | Notes |
|---------|-----------|-------|
| Select trigger (input) | `combobox` | Provided by react-select. Has `aria-haspopup="listbox"`, `aria-expanded` |
| Dropdown menu | `listbox` | Appears when the select is open |
| Option item | `option` | Each item in the listbox |
| Selected option(s) | `aria-selected="true"` | Applied to the currently selected option(s) |
| Disabled state | `aria-disabled="true"` | Set when `isDisabled={true}` |
| Required field | `aria-required="true"` | Set when `isRequired={true}` |
| Error state | `aria-invalid="true"` | Set when `hasError={true}` |
| Label | Associated via `htmlFor` / `aria-labelledby` | Use `labelValue` to provide visible label text |
| Info button | `aria-label` | Use `infoBoxButtonLabel` to provide accessible label for the info (ⓘ) button |
| Loading state | `aria-busy="true"` | Set when `isLoading={true}` |

## Keyboard Interactions

| Key | Behaviour |
|-----|-----------|
| `Tab` | Move focus to the Select |
| `Shift + Tab` | Move focus away from the Select |
| `Enter` / `Space` | Open dropdown (when closed); select focused option (when open) |
| `↓` Arrow Down | Open dropdown (when closed); move focus to next option (when open) |
| `↑` Arrow Up | Move focus to previous option (when open) |
| `Escape` | Close dropdown without selecting |
| `Home` | Jump to first option in the list |
| `End` | Jump to last option in the list |
| Printable characters | Jump to option starting with typed character(s) |
| `Backspace` / `Delete` | Remove last selected chip (when `isMulti` and there is a selected value) |

## Screen Reader Guidance

- The `labelValue` prop renders a visible `<label>` element associated with the control — always provide a meaningful label.
- When `isRequired={true}`, a required indicator is shown visually; `aria-required` is set programmatically.
- When `hasError={true}`, the error state is communicated via `aria-invalid`. Pair with a visible error message below the field to satisfy 3.3.1.
- Use `infoBoxButtonLabel` to give the info (ⓘ) button an accessible name — without it the button has no text and will be announced as unlabelled.
- For async selects (`isAsync`), loading state is announced via `aria-busy` and the `loadingMessage` string.
- For multi-select, each chip has a remove button — ensure screen readers can reach and activate each one.

## WCAG 2.1 AA Checklist

| Criterion | Level | Status | Notes |
|-----------|-------|--------|-------|
| 1.3.1 Info and Relationships | A | ✅ | `labelValue` programmatically associates label with control |
| 1.4.3 Contrast Ratio (text) | AA | ✅ (verify) | Verify placeholder and disabled text meet 4.5:1 against background |
| 1.4.11 Non-text Contrast | AA | ✅ (verify) | Focus ring and border states should meet 3:1 against adjacent colours |
| 2.1.1 Keyboard | A | ✅ | Fully operable via keyboard (react-select provides complete keyboard support) |
| 2.1.2 No Keyboard Trap | A | ✅ | `Escape` closes the dropdown; Tab moves focus normally |
| 2.4.3 Focus Order | A | ✅ | Select follows document focus order; open state keeps focus within dropdown |
| 2.4.7 Focus Visible | AA | ✅ | Focused state renders visible focus ring (see Figma: `State=Focus`) |
| 3.3.1 Error Identification | A | ✅ | `hasError={true}` + visible error message satisfies this criterion |
| 3.3.2 Labels or Instructions | A | ✅ | `labelValue` provides visible label; `infoBoxText` provides additional instructions |
| 4.1.2 Name, Role, Value | A | ✅ | `combobox`/`listbox`/`option` roles set by react-select; value announced on change |

## Related Components

When fewer options are present:
- **Radio Button** — use for single selection from ≤5 options
- **Checkbox** — use for multiple selection from ≤5 options

_Source: Oxygen MCP · Inferred from component type · Extracted 2026-04-29_
