---
parent: "[[ToggleButton]]"
section: usage
pipeline_stage: draft
source_type: editorial
tags:
  - oxygen
  - component/ToggleButton
  - role/spoke
  - section/usage
---

<!-- STUB:GAP-003 source="Author Do/Don't card frames on Figma examples page 50606:95349 (node 50606:95349), then run figma-extract-usage ToggleButton to replace this editorial draft wholesale. The 5 pairs below are grounded in oxygen.8x8.com/components/toggle/usage and the extracted MCP/Figma artifacts." -->

> **Editorial draft** — this file was drafted 2026-05-15 from the Oxygen web docs at [oxygen.8x8.com/components/toggle/usage](https://oxygen.8x8.com/components/toggle/usage) combined with extracted MCP/Figma artifacts. Replace wholesale with `figma-extract-usage ToggleButton` output once `✅ Do — …` / `❌ Don't — …` card frames are authored on the Figma examples page (`50606:95349`).

## When to use

- Use a toggle for users to **switch between two binary states**.
- Use toggles when the corresponding action **takes effect immediately** — no Save button, no confirmation step.

## When not to use

- **Do not use toggles when the users will choose from a list of items.** Use Radio (single-select) or Checkbox (multi-select) instead.
- **Do not use toggles when a Save button is needed to apply or save a selection.** Use Checkbox inside the form; the form's Save commits the value.
- **Do not use a single toggle for a mutually-exclusive pair of options.** Two options that each need a label (e.g. "Monthly / Yearly") call for a SegmentedControl or Radio group — the toggle itself only announces on/off, not the names of the two states.

---

## Do / Don't

### Pair 1 — Binary state with immediate effect; not list selection or save-button flows

#### ✅ Do — Flip a single setting that takes effect the moment the user toggles it

```tsx
function NotificationsRow({ userId }: { userId: string }) {
  const [isChecked, setIsChecked] = React.useState(false);

  const handleChange = () => {
    setIsChecked(prev => {
      const next = !prev;
      void api.updateNotificationPref(userId, next);
      return next;
    });
  };

  return (
    <ToggleButton
      label="Email me about new replies"
      name="email-notifications"
      value="email-notifications"
      isChecked={isChecked}
      onChange={handleChange}
    />
  );
}
```

#### ❌ Don't — Use a toggle as a list selector or behind a Save button

```tsx
{/* Wrong — three toggles modelling a mutually-exclusive choice. This is a Radio group. */}
<ToggleButton label="Monthly"   name="billing" value="monthly"   isChecked={plan === 'monthly'}   onChange={() => setPlan('monthly')} />
<ToggleButton label="Quarterly" name="billing" value="quarterly" isChecked={plan === 'quarterly'} onChange={() => setPlan('quarterly')} />
<ToggleButton label="Yearly"    name="billing" value="yearly"    isChecked={plan === 'yearly'}    onChange={() => setPlan('yearly')} />

{/* Wrong — toggle paired with Save button breaks the "immediate effect" contract. */}
<form onSubmit={save}>
  <ToggleButton label="Enable two-factor auth" name="2fa" value="2fa" isChecked={twoFa} onChange={() => setTwoFa(p => !p)} />
  <Button type="submit">Save</Button>
</form>
```

---

### Pair 2 — Single source of truth for `isChecked`; no uncontrolled or parallel booleans

#### ✅ Do — Hold one boolean, update it from `onChange`, pass it back via `isChecked`

```tsx
const [isChecked, setIsChecked] = React.useState(false);

<ToggleButton
  label="Enable notifications"
  name="notifications"
  value="notifications"
  isChecked={isChecked}
  onChange={() => setIsChecked(prev => !prev)}
/>;
```

#### ❌ Don't — Render without `isChecked`/`onChange`, or split state across two booleans

```tsx
{/* Wrong — no isChecked + no onChange. Toggle is fixed at false; AT hears a non-responsive control. */}
<ToggleButton label="Enable notifications" name="notifications" value="notifications" />

{/* Wrong — two booleans modelling one piece of state. Will drift. */}
const [uiChecked, setUiChecked]         = React.useState(false);
const [serverChecked, setServerChecked] = React.useState(false);
```

---

### Pair 3 — Toggle Input (label-less) only when surrounding context makes purpose obvious

#### ✅ Do — Drop the label inside table cells or list rows with a header column

```tsx
<DataTable>
  <thead><tr><th>Name</th><th>Active</th></tr></thead>
  <tbody>
    {users.map(u => (
      <tr key={u.id}>
        <td>{u.name}</td>
        <td>
          <ToggleButton
            label={null}
            name={`active-${u.id}`}
            value={u.id}
            isChecked={u.active}
            onChange={() => setActive(u.id, !u.active)}
          />
        </td>
      </tr>
    ))}
  </tbody>
</DataTable>
```

When the surrounding context alone isn't enough, give the parent container an `aria-label` or `aria-labelledby` so screen-reader users still hear what the switch controls.

#### ❌ Don't — Free-floating label-less switch in open UI

```tsx
{/* Wrong — nothing explains what the switch does. AT hears "switch, off" with no name. */}
<section style={{ padding: 24 }}>
  <ToggleButton label={null} name="setting" value="setting" isChecked={enabled} onChange={() => setEnabled(p => !p)} />
</section>
```

---

### Pair 4 — Always pair `infoBoxText` with `infoBoxButtonLabel`

#### ✅ Do — Supply both props so the info icon button has a clear `aria-label`

```tsx
<ToggleButton
  label="Advanced mode"
  name="advanced"
  value="advanced"
  isChecked={isChecked}
  onChange={handleChange}
  infoBoxText="Enabling this will expose additional configuration options."
  infoBoxButtonLabel="More information about advanced mode"
/>
```

#### ❌ Don't — Set `infoBoxText` without `infoBoxButtonLabel`

```tsx
{/* Wrong — info icon button has no accessible name. */}
<ToggleButton
  label="Advanced mode"
  name="advanced"
  value="advanced"
  isChecked={isChecked}
  onChange={handleChange}
  infoBoxText="Enabling this will expose additional configuration options."
/>
```

---

### Pair 5 — Compose error messaging below `ToggleButtonGroup` manually until the API exposes `isError`

#### ✅ Do — Render the validation message as a sibling element below the group

The Figma Toggle Group has an `isError` variant (red `InlineValidationMessage` using `--error/error01`). OX `ToggleButtonGroup` does **not** expose an `isError` prop — only `isHorizontal` and `children`. Compose the error message yourself until that prop ships.

```tsx
<>
  <ToggleButtonGroup>
    <ToggleButton label="Marketing" name="prefs" value="marketing" isChecked={a} onChange={fa} />
    <ToggleButton label="Product"   name="prefs" value="product"   isChecked={b} onChange={fb} />
    <ToggleButton label="Account"   name="prefs" value="account"   isChecked={c} onChange={fc} />
  </ToggleButtonGroup>

  {error && (
    <p role="alert" style={{ color: 'var(--error-error01)', marginTop: 8 }}>
      {error}
    </p>
  )}
</>
```

#### ❌ Don't — Pass `isError` to `ToggleButtonGroup`

```tsx
{/* Wrong — isError is not part of the OX ToggleButtonGroup API. Prop is silently dropped. */}
<ToggleButtonGroup isError={hasError}>
  <ToggleButton label="Marketing" name="prefs" value="marketing" isChecked={a} onChange={fa} />
</ToggleButtonGroup>
```

---

## Behaviour notes

- **Controlled component:** `isChecked` is presentational; the consuming application owns the boolean and updates it from `onChange`.
- **Whole row is the click + focus target:** the focus and click area covers the full switch + label row, not just the switch pill.
- **Multiline labels:** switch stays top-aligned; do not override `items-start` to `center`.
- **`isIndeterminate` caveat:** aria-checked="mixed" requires explicit implementation in `SwitchBase` — see WARN-001 in the audit. Reserve indeterminate for genuine partial-selection cases and verify in a screen reader before shipping.

_Drafted as an editorial-source usage guide · 2026-05-15_
