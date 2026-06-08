---
component: Checkbox
package: "@8x8/oxygen-checkbox"
category: form_inputs
role: accessibility
role_description: "Accessibility — ARIA roles, keyboard interactions, and WCAG 2.1 AA guidance"
pipeline_stage: spec_ready
pipeline_note: "Audit verdict YES/PARTIAL — doc-rewrite can run"
audit_verdict: YES
siblings:
  - "[[Checkbox/props]]"
  - "[[Checkbox/examples]]"
  - "[[Checkbox/tokens]]"
  - "[[Checkbox/checkbox-figma]]"
  - "[[Checkbox/checkbox-pui]]"
  - "[[Checkbox/checkbox-audit]]"
tags:
  - oxygen
  - component/Checkbox
  - role/accessibility
  - stage/spec_ready
  - category/form_inputs
---
# Checkbox — Accessibility

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md)

> **Data gap:** The Oxygen MCP returned no explicit accessibility annotations for Checkbox.
> The Figma design context was inaccessible (Figma Desktop not connected). Guidance below is
> derived from the component's interactive nature, prop definitions, and ARIA patterns for
> checkboxes as per WAI-ARIA 1.1 / WCAG 2.1 AA.

---

## ARIA role

| Element | Role | Notes |
|---------|------|-------|
| Checkbox input | `checkbox` (native `<input type="checkbox">`) | Native HTML element — role is implicit |
| Label | associated via `htmlFor` → `id` prop | `id` prop wires `<label htmlFor>` and `<input id>` |
| Info button (optional) | `button` | Aria-label supplied via `infoBoxButtonLabel` prop |
| Info tooltip | `tooltip` | Shown on info button activation |

---

## Keyboard interactions

| Key | Behaviour |
|-----|-----------|
| `Tab` | Moves focus to the checkbox |
| `Shift + Tab` | Moves focus away from the checkbox |
| `Space` | Toggles checked / unchecked state |
| (no `Enter` action) | Enter does not activate checkboxes per WAI-ARIA spec |

---

## States and their accessibility impact

| State | Visual cue | `aria-*` impact |
|-------|-----------|-----------------|
| Unchecked | Empty box | `aria-checked="false"` (implicit via native input) |
| Checked | Filled box with checkmark | `aria-checked="true"` |
| Indeterminate | Filled box with dash | `aria-checked="mixed"` — set via `isIndeterminate` prop; also set `indeterminate` DOM property |
| Disabled | Greyed out | `aria-disabled="true"` / `disabled` attribute — not focusable |
| Focus | Focus ring visible | Native `:focus-visible` ring |
| Hover | Visual hover state | No ARIA impact (transient) |

---

## Screen reader guidance

- The `label` prop is the accessible name for the checkbox. It accepts `node` — if passing a custom
  component, ensure the rendered output produces visible text.
- The `showLabelTooltipOnOverflow` prop shows a tooltip when label text is clipped. Screen readers
  still receive the full label via the `<label>` element regardless of truncation.
- `infoBoxText` content is hidden inside a Tooltip triggered by the info icon button. Screen reader
  users can activate the info button (accessible name = `infoBoxButtonLabel`) to read the tooltip.
- When `isIndeterminate` is used (parent of nested checkboxes), ensure the accessible name clearly
  conveys the "select all" or parent nature (e.g. `label="Select all items"`).

---

## Nesting and group accessibility

When using `CheckboxGroup`:
- Wrap the group in a `<fieldset>` with a `<legend>` to provide a group accessible name.
  The Oxygen `CheckboxGroup` component should handle this — verify in rendered output.
- Nested (parent/child) checkbox groups must maintain logical DOM order matching visual order.
- The parent checkbox in an intermediate state should have `aria-checked="mixed"`.

### Error state accessibility (CheckboxGroup)

When a `CheckboxGroup` fails validation (the `isError` Figma variant — pending in the API, see the
audit GAP-008):

- Render the inline error message in a live region so assistive tech announces it: `role="alert"`
  (or `aria-live="polite"` on a persistent error container).
- Associate the error with the control that triggers submission: give the error element an `id` and
  reference it with `aria-describedby` on the submit `Button` (or on the group container).
- Keep the checkbox **enabled** during error — do not disable it to express invalidity. A disabled
  control removes the affordance and the explanation; the error message carries the meaning instead.

```jsx
<CheckboxGroup>
  <Checkbox id="terms" name="terms" label="I agree to the terms and conditions"
    value="terms" isChecked={agreed} onChange={(e) => setAgreed(e.target.checked)} />
</CheckboxGroup>
{!agreed && submitted ? (
  <p id="terms-error" role="alert">You must accept the terms before continuing.</p>
) : null}
<Button type="submit" aria-describedby="terms-error">Sign up</Button>
```

---

## WCAG 2.1 AA checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.3.1 Info and Relationships | Pass (by design) | Native input + label association via `htmlFor` |
| 1.3.3 Sensory Characteristics | Pass | State conveyed by text label, not colour alone |
| 1.4.1 Use of Colour | Verify | Disabled state must not rely solely on colour — check design |
| 1.4.3 Contrast (text) | Verify | Label text against background in all states / modes |
| 1.4.11 Non-text Contrast | Verify | Checkbox border in unchecked rest state vs background |
| 2.1.1 Keyboard | Pass (by design) | Native input is keyboard operable |
| 2.4.3 Focus Order | Pass (by design) | Native tab order |
| 2.4.7 Focus Visible | Pass (by design) | `isFocused` variant with focus ring shown in Figma |
| 3.2.2 On Input | Pass | `onChange` callback — no unexpected context change |
| 4.1.2 Name, Role, Value | Pass (by design) | Native checkbox; label via `htmlFor`; state via `aria-checked` |

_Source: Oxygen MCP prop definitions + WAI-ARIA Checkbox Pattern · Extracted 2026-04-29_
