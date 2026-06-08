---
parent: "[[Checkbox]]"
section: accessibility
---

## Accessibility

> Guidance is derived from the component's native `<input type="checkbox">` base, its prop
> definitions, and the WAI-ARIA 1.1 Checkbox pattern / WCAG 2.1 AA — not from Figma annotations
> (none present) or MCP a11y data (none returned). Validate against the rendered component before
> publishing.

### ARIA roles

| Element | Role | Notes |
|---------|------|-------|
| Checkbox input | `checkbox` (native `<input type="checkbox">`) | Role is implicit — no override needed |
| Label | associated via `htmlFor` → `id` | The `label` prop is the accessible name |
| Info button (optional) | `button` | Accessible name from `infoBoxButtonLabel` |
| Info tooltip | `tooltip` | Shown on info-button activation |

### Keyboard

| Key | Behaviour |
|-----|-----------|
| `Tab` / `Shift + Tab` | Move focus to / away from the checkbox |
| `Space` | Toggle checked / unchecked |
| `Enter` | **No action** — per the WAI-ARIA Checkbox pattern |

The info button (`infoBoxText`) is a **separate focus stop** with its own tab order.

### States → ARIA

| State | `aria-*` impact |
|-------|-----------------|
| Unchecked | `aria-checked="false"` (implicit) |
| Checked | `aria-checked="true"` |
| Indeterminate | `aria-checked="mixed"` — set via `isIndeterminate`; **also set the DOM `indeterminate` property** |
| Disabled | `disabled` + `aria-disabled="true"`; removed from focus order |
| Focus | Native `:focus-visible` ring — never suppress with `outline: none` (WCAG 2.4.7) |

### Group accessibility (CheckboxGroup)

- Wrap the group in `<fieldset>` / `<legend>` (or supply `aria-labelledby`) to give the set an accessible name.
- Nested parent/child groups must maintain logical DOM order matching visual order.
- The parent checkbox in an intermediate state has `aria-checked="mixed"`.

<!-- STUB:GAP-011 source="Verify rendered CheckboxGroup DOM output for fieldset/legend presence. Update accessibility.md to reflect actual behavior." -->
> **Unverified (GAP-011).** Whether Oxygen's `CheckboxGroup` emits `<fieldset>` / `<legend>`
> automatically is not confirmed. If it does not, add your own wrapper or supply
> `aria-labelledby` on the container.

### Error state (CheckboxGroup)

When a group fails validation (the `isError` Figma variant — pending in the API, see GAP-008):

- Render the inline error in a live region: `role="alert"` (or `aria-live="polite"` on a persistent container).
- Give the error an `id` and reference it via `aria-describedby` on the submit `Button` (or group container).
- Keep the checkbox **enabled** during error — a disabled control removes both the affordance and the explanation.

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

### WCAG 2.1 AA checklist

| Criterion | Status | Notes |
|-----------|--------|-------|
| 1.3.1 Info and Relationships | Pass (by design) | Native input + label association via `htmlFor` |
| 1.3.3 Sensory Characteristics | Pass | State conveyed by text label, not colour alone |
| 1.4.1 Use of Colour | Verify | Disabled state must not rely solely on colour |
| 1.4.3 Contrast (text) | Verify | Label text in all states / modes |
| 1.4.11 Non-text Contrast | Verify | Unchecked-rest border vs background |
| 2.1.1 Keyboard | Pass (by design) | Native input is keyboard operable |
| 2.4.3 Focus Order | Pass (by design) | Native tab order |
| 2.4.7 Focus Visible | Pass (by design) | `interactive/focus01` ring |
| 3.2.2 On Input | Pass | `onChange` — no unexpected context change |
| 4.1.2 Name, Role, Value | Pass (by design) | Native checkbox; label via `htmlFor`; state via `aria-checked` |
