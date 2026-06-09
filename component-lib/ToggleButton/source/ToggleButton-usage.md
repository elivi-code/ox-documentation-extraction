---
component: ToggleButton
package: "@8x8/oxygen-toggleButton"
category: form_inputs
role: usage
role_description: "Usage guidelines — editorial draft from Oxygen web docs (oxygen.8x8.com/components/toggle/usage) + extracted MCP/Figma artifacts; Figma examples page has no Do/Don't card frames yet"
pipeline_stage: editorial
pipeline_note: "Pairs are editorial. Replace this file wholesale with figma-extract-usage output once `✅ Do —` / `❌ Don't —` card frames are authored on the Figma examples page. ToggleButton-audit.md GAP-003 is now partial-resolved-editorial; the Figma-card half of the gap remains."
source_type: editorial
audit_verdict: null
siblings:
  - "[[ToggleButton/props]]"
  - "[[ToggleButton/examples]]"
  - "[[ToggleButton/tokens]]"
  - "[[ToggleButton/accessibility]]"
  - "[[ToggleButton/ToggleButton-figma]]"
  - "[[ToggleButton/ToggleButton-pui]]"
  - "[[ToggleButton/ToggleButton-audit]]"
tags:
  - oxygen
  - component/ToggleButton
  - role/usage
  - stage/editorial
  - category/form_inputs
---
<!-- SOURCE: editorial — Oxygen web docs (https://oxygen.8x8.com/components/toggle/usage) + props.md + examples.md + ToggleButton-figma.md + accessibility.md + ToggleButton-audit.md -->
<!-- FIGMA EXAMPLES PAGE: exists (file 5YihJ5WuDvnvrlrRMC4sBp, node 50606:95349) but has no `✅ Do — …` / `❌ Don't — …` card frames yet -->
<!-- GROUNDING: full — every sibling file is present in component-lib/ToggleButton/ -->
<!-- DRAFTED: 2026-05-15 -->
<!-- MODE: editorial (web-anchored, not usage-advisor) -->
<!-- PAIRS: 5 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output once Do/Don't card frames are authored on the Figma examples page -->

# ToggleButton — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [ToggleButton-figma.md](./ToggleButton-figma.md) · [ToggleButton-pui.md](./ToggleButton-pui.md) · [ToggleButton-audit.md](./ToggleButton-audit.md)

> **Editorial guidance — Figma Do/Don't cards have not been authored yet.** This file mirrors the canonical Oxygen web documentation at [oxygen.8x8.com/components/toggle/usage](https://oxygen.8x8.com/components/toggle/usage) and grounds the additional pairs in the extracted MCP and Figma artifacts in this folder. It **partially** resolves [ToggleButton-audit.md](./ToggleButton-audit.md) **GAP-003**: the `ToggleButton-usage.md` file is now present, but the upstream `✅ Do — …` / `❌ Don't — …` card frames on the Figma examples page (`50606:95349`) are still missing. When designers author those cards, run `figma-extract-usage ToggleButton` and replace this file wholesale. The structural precedent is [Tabs-usage.md](../Tabs/Tabs-usage.md).

`ToggleButton` is a controlled binary switch with an associated label. The consuming application owns `isChecked` and is responsible for updating it from `onChange` ([props.md:98](./props.md)). The package also exports `ToggleButtonGroup`, a vertical or horizontal wrapper for multiple toggles ([props.md:87-92](./props.md)).

---

## Anatomy

> Anatomy below is grounded in [ToggleButton-figma.md](./ToggleButton-figma.md) (component sets `51776:7539` Toggle Input, `51776:7580` Toggle, `52689:99119` Toggle Group) and [props.md](./props.md). Replace with `figma-extract` output if the design is restructured.

1. **Toggle Input (switch-only, 40×24px)** — the pill-shaped switch on its own, with a circular knot that sits left when off and right when on ([ToggleButton-figma.md:52-59](./ToggleButton-figma.md)).
2. **Toggle (switch + label, 148×24px default)** — Toggle Input fixed at the left, then a 12px gap, then the form-control label. The label is top-aligned (`items-start`) so multiline labels keep the switch pinned to the first line ([ToggleButton-figma.md:61-68](./ToggleButton-figma.md), [ToggleButton-figma.md:279](./ToggleButton-figma.md)).
3. **Optional info icon button** — rendered only when `infoBoxText` is set; opens a Tooltip on click and is treated as a separate focus stop from the Toggle itself ([props.md:75-76](./props.md), [accessibility.md:66-68](./accessibility.md)).
4. **ToggleButtonGroup wrapper** — vertical by default, horizontal when `isHorizontal`. Optional header (label + info icon button) and footer (helper or error message) slots ([props.md:87-92](./props.md), [ToggleButton-figma.md:70-76](./ToggleButton-figma.md)).
5. **Focus ring scope differs by variant** — on Toggle Input the ring surrounds only the switch; on Toggle (with label) the ring covers the **entire switch + label area**, because the whole row is the interactive target ([ToggleButton-figma.md:58](./ToggleButton-figma.md), [ToggleButton-figma.md:66-67](./ToggleButton-figma.md), [accessibility.md:51-56](./accessibility.md)).

---

## Behaviour

### Controlled component — parent owns `isChecked`

`isChecked` is a presentational flag. The Oxygen component does not track its own state — the consuming application stores a boolean and updates it from `onChange` ([props.md:98](./props.md), [examples.md:33-50](./examples.md)).

### The whole row is the click + focus target

Per Figma annotation, "the focus includes the entire Toggle item, from the Toggle Switch to the label. The whole area of the item is interactive, clickable, and responsive to hover actions" ([ToggleButton-figma.md:285](./ToggleButton-figma.md), [accessibility.md:51-56](./accessibility.md)). Don't render a separate hit target for the label.

### Multiline labels keep the switch top-aligned

When the label wraps to a second line, the switch stays aligned to the top of the row, not centred vertically ([ToggleButton-figma.md:279](./ToggleButton-figma.md), [accessibility.md:77](./accessibility.md)). This is what `items-start` in the auto-layout produces; don't override it to `center` for "balance."

### `isIndeterminate` has an unresolved aria-checked caveat

The OX docs state that the indeterminate state is communicated via `aria-checked="mixed"` or the `indeterminate` property ([accessibility.md:36](./accessibility.md)), but native HTML checkboxes only expose `.indeterminate` and do **not** update `aria-checked` automatically — [ToggleButton-audit.md WARN-001](./ToggleButton-audit.md) flags this as needing source-level confirmation. Until that's confirmed, reserve indeterminate for genuine partial-selection cases (a "Select all" parent whose children are partly checked) and verify the announced state in a screen reader before shipping.

---

## When to use

- Use a toggle for users to **switch between two binary states**.
- Use toggles when the corresponding action **takes effect immediately** — no Save button, no confirmation step.

> Both lines are quoted verbatim from [oxygen.8x8.com/components/toggle/usage](https://oxygen.8x8.com/components/toggle/usage).

## When not to use

- **Do not use toggles when the users will choose from a list of items.** Use Radio (single-select) or Checkbox (multi-select) instead.
- **Do not use toggles when a Save button is needed to apply or save a selection.** Use Checkbox inside the form; the form's Save commits the value.
- **Do not use a single toggle for a mutually-exclusive pair of options.** Two options that need a label each (e.g. "Monthly / Yearly") read as a SegmentedControl or Radio group — the toggle itself only announces on/off, not the names of the two states.

> The first two lines are quoted verbatim from the Oxygen web page. The third is derived from the API shape (`isChecked: bool`, [props.md:77](./props.md)) and the absence of a paired-label slot.

---

## Do / Don't

### Pair 1 — Use Toggle for binary states with immediate effect; don't use it for list selection or save-button flows

#### ✅ Do — Flip a single setting that takes effect the moment the user toggles it

```tsx
{/* Right — one binary preference; the change persists immediately on toggle */}
function NotificationsRow({ userId }: { userId: string }) {
  const [isChecked, setIsChecked] = React.useState(false);

  const handleChange = () => {
    setIsChecked(prev => {
      const next = !prev;
      void api.updateNotificationPref(userId, next); // applies immediately
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

#### ❌ Don't — Use a toggle as a list selector or to defer a value behind a Save button

```tsx
{/* Wrong — three toggles modelling a mutually-exclusive choice from a list.
    This is a Radio group; toggles can't communicate "which one is selected"
    because each one only announces its own on/off state. */}
<ToggleButton label="Monthly"    name="billing" value="monthly"    isChecked={plan === 'monthly'}    onChange={() => setPlan('monthly')} />
<ToggleButton label="Quarterly"  name="billing" value="quarterly"  isChecked={plan === 'quarterly'}  onChange={() => setPlan('quarterly')} />
<ToggleButton label="Yearly"     name="billing" value="yearly"     isChecked={plan === 'yearly'}     onChange={() => setPlan('yearly')} />

{/* Wrong — the user must press Save for the toggle to do anything. Toggles
    advertise immediate effect; pairing them with a Save button breaks that
    contract and confuses users who expect their click to have already taken. */}
<form onSubmit={save}>
  <ToggleButton label="Enable two-factor auth" name="2fa" value="2fa" isChecked={twoFa} onChange={() => setTwoFa(p => !p)} />
  <Button type="submit">Save</Button>
</form>
```

**Why it matters:** the Oxygen web doc is explicit — toggles are for two binary states with immediate effect, and not for list selection or save-button flows. Mis-using a toggle for either case forces users to relearn what a toggle means in your product.

**Source:** [oxygen.8x8.com/components/toggle/usage](https://oxygen.8x8.com/components/toggle/usage) · [props.md:77](./props.md).

---

### Pair 2 — Drive `isChecked` from a single source of truth in the parent; don't leave it uncontrolled or run parallel booleans

#### ✅ Do — Hold one boolean, update it from `onChange`, and pass it back via `isChecked`

`ToggleButton` is a **controlled component** ([props.md:98](./props.md)). The parent owns the state; the component renders whatever `isChecked` says.

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

#### ❌ Don't — Render without `isChecked`/`onChange`, or duplicate the state across two booleans

```tsx
{/* Wrong — no isChecked + no onChange means the toggle is fixed at its
    default (false). Users will click it and nothing will visually change;
    AT will announce a control that does not respond. */}
<ToggleButton label="Enable notifications" name="notifications" value="notifications" />

{/* Wrong — two booleans modelling one piece of state. The moment they drift,
    the component shows one thing and your business logic believes another. */}
const [uiChecked, setUiChecked]       = React.useState(false);
const [serverChecked, setServerChecked] = React.useState(false);

<ToggleButton
  label="Enable notifications"
  name="notifications"
  value="notifications"
  isChecked={uiChecked}
  onChange={() => { setUiChecked(p => !p); /* serverChecked never updates here */ }}
/>
```

**Why it matters:** the API has no internal fallback — without a controlled `isChecked` paired with an `onChange` that updates it, the toggle is effectively read-only. Avoid the "isChecked with no onChange" anti-pattern called out in [accessibility.md:87](./accessibility.md): "controlled toggles with no handler will appear non-interactive to AT."

**Source:** [props.md:98](./props.md) · [examples.md:33-50](./examples.md) · [accessibility.md:87](./accessibility.md).

---

### Pair 3 — Use the label-less Toggle Input only when surrounding context makes its function obvious

#### ✅ Do — Drop the label inside table cells, list rows, or any container whose header already explains the column

The Toggle Input variant (switch only, 40×24px) is designed for "scenarios where the function of the Toggle is clear from the context or design of the interface… a cell within a table or an item in a list" ([ToggleButton-figma.md:265](./ToggleButton-figma.md)).

```tsx
{/* Right — the column header "Active" labels the toggle for every row,
    so a per-row label would be noise */}
<DataTable>
  <thead>
    <tr><th>Name</th><th>Active</th></tr>
  </thead>
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

When the surrounding context isn't enough on its own, give the **parent container** an accessible name via `aria-label` or `aria-labelledby` ([accessibility.md:85](./accessibility.md)) so screen-reader users still hear what the switch controls.

#### ❌ Don't — Render a free-floating label-less switch in open UI

```tsx
{/* Wrong — there is nothing around this switch that explains what it does.
    Sighted users see a meaningless control; AT users hear "switch, off" with
    no accessible name. Use the labelled Toggle variant instead. */}
<section style={{ padding: 24 }}>
  <ToggleButton
    label={null}
    name="setting"
    value="setting"
    isChecked={enabled}
    onChange={() => setEnabled(p => !p)}
  />
</section>

{/* Wrong — dropping the label and "fixing" it with a sibling <span> doesn't
    associate the text with the control: there's no htmlFor, no aria-labelledby,
    and the click target loses the label half of the row */}
<div>
  <span>Enable notifications</span>
  <ToggleButton label={null} name="setting" value="setting" isChecked={x} onChange={fn} />
</div>
```

**Why it matters:** the Toggle Input variant exists specifically to remove visual redundancy when context already labels the switch — using it without that context strips the accessible name and breaks the "whole row is the click target" guarantee ([ToggleButton-figma.md:285](./ToggleButton-figma.md)).

**Source:** [examples.md:97-114](./examples.md) · [ToggleButton-figma.md:265](./ToggleButton-figma.md) · [accessibility.md:85](./accessibility.md).

---

### Pair 4 — Always pair `infoBoxText` with `infoBoxButtonLabel`; never render the info icon without an accessible name

#### ✅ Do — Supply both props together so the info icon button has a clear `aria-label`

`infoBoxText` renders an info icon that opens a Tooltip on click. `infoBoxButtonLabel` is the icon button's accessible name and is **required** for accessibility — both props must be supplied together ([props.md:75-76](./props.md), [props.md:100](./props.md), [accessibility.md:43-46](./accessibility.md)).

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

#### ❌ Don't — Set `infoBoxText` without `infoBoxButtonLabel`, or reuse the toggle's label as the button name

```tsx
{/* Wrong — info icon button has no accessible name. Screen-reader users hear
    an unnamed button and have no way to know what activating it will do. */}
<ToggleButton
  label="Advanced mode"
  name="advanced"
  value="advanced"
  isChecked={isChecked}
  onChange={handleChange}
  infoBoxText="Enabling this will expose additional configuration options."
/>

{/* Wrong — reusing the toggle label is misleading; AT users will hear
    "Advanced mode, button" twice and not know the second one opens help text */}
<ToggleButton
  label="Advanced mode"
  name="advanced"
  value="advanced"
  infoBoxText="…"
  infoBoxButtonLabel="Advanced mode"
/>
```

**Why it matters:** the info icon is a separate focus stop from the toggle ([accessibility.md:66-68](./accessibility.md)), so it must announce its own purpose. The docs make the pairing a hard requirement, not a recommendation.

**Source:** [props.md:75-76](./props.md) · [props.md:100](./props.md) · [accessibility.md:43-46](./accessibility.md).

---

### Pair 5 — Compose error messaging below `ToggleButtonGroup` manually until the API exposes `isError`

#### ✅ Do — Render the validation message as a sibling element below the group

The Figma Toggle Group component set has an `isError` variant that swaps the footer to an `InlineValidationMessage` with red error text using `--error/error01` ([ToggleButton-figma.md:105-107](./ToggleButton-figma.md), [tokens.md:80](./tokens.md)). The OX implementation does **not** expose an `isError` prop — only `isHorizontal` and `children` ([props.md:87-92](./props.md), [ToggleButton-audit.md GAP-002](./ToggleButton-audit.md)). Until that prop ships, render the error message yourself.

```tsx
{/* Right — group renders the toggles; the validation message is a sibling
    element using the same error token the Figma design specifies. */}
<>
  <ToggleButtonGroup>
    <ToggleButton label="Marketing" name="prefs" value="marketing" isChecked={a} onChange={fa} />
    <ToggleButton label="Product"   name="prefs" value="product"   isChecked={b} onChange={fb} />
    <ToggleButton label="Account"   name="prefs" value="account"   isChecked={c} onChange={fc} />
  </ToggleButtonGroup>

  {error && (
    <p role="alert" style={{ color: 'var(--error-error01)', marginTop: 8 /* $spacing03 */ }}>
      {error}
    </p>
  )}
</>
```

#### ❌ Don't — Pass `isError` to `ToggleButtonGroup` or rely on a Figma-only variant in code

```tsx
{/* Wrong — isError is not part of the OX ToggleButtonGroup API. This prop is
    silently dropped; no red text appears; users see no validation feedback. */}
<ToggleButtonGroup isError={hasError}>
  <ToggleButton label="Marketing" name="prefs" value="marketing" isChecked={a} onChange={fa} />
  <ToggleButton label="Product"   name="prefs" value="product"   isChecked={b} onChange={fb} />
</ToggleButtonGroup>

{/* Wrong — adding a `data-error` styling hook that flips the group red without
    rendering a visible message: screen-reader users hear nothing about the error,
    and sighted users see colour-only feedback which fails WCAG 1.4.1. */}
<ToggleButtonGroup data-error={hasError}>…</ToggleButtonGroup>
```

**Why it matters:** the design spec and the API have diverged — see [ToggleButton-audit.md GAP-002](./ToggleButton-audit.md). The composition pattern above is the workaround documented for consumers; using the Figma variant name in code creates a silent failure.

**Source:** [props.md:87-92](./props.md) · [ToggleButton-figma.md:105-107](./ToggleButton-figma.md) · [tokens.md:80](./tokens.md) · [ToggleButton-audit.md GAP-002](./ToggleButton-audit.md).

---

## Gaps & open questions

- **GAP-003 partial resolution** — this file now satisfies the "ToggleButton-usage.md present" half of [ToggleButton-audit.md GAP-003](./ToggleButton-audit.md). The other half — Figma `✅ Do —` / `❌ Don't —` card frames on the examples page (`50606:95349`) — remains a SOURCE_GAP. When designers author the cards, run `figma-extract-usage ToggleButton` and replace this file wholesale.
- **GAP-002 (ToggleButtonGroup `isError`)** — Pair 5 documents the consumer-composition workaround. If a future release adds `isError` to the OX API, replace Pair 5's "Do" with a direct prop usage and move the composition pattern into the "Don't" column for older versions.
- **WARN-001 (indeterminate `aria-checked="mixed"`)** — the Behaviour section calls this out as needing source-level confirmation against `SwitchBase`. Once verified, soften or remove the "verify in a screen reader before shipping" guidance.

_Drafted as an editorial-source usage guide · 2026-05-15_
