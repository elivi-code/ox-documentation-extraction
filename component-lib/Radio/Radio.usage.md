---
parent: "[[Radio]]"
section: usage
---

<!-- source: editorial — published Oxygen docs page (https://oxygen.8x8.com/components/radiobutton/usage, fetched 2026-05-14) + extracted MCP artifacts -->
<!-- WARN-001: Usage is editorial — mirrors the published Oxygen docs page. No Figma "↳ Radio examples" page with Do/Don't card frames exists. Replace pairs with figma-extract-usage output if such a page is created. -->

Radio Buttons are input controls that let a user **select exactly one option** from a related group. Selecting a new option automatically deselects the previously selected one.

---

## When to use

Reach for Radio Buttons when **all** of these are true:

- The user must pick **exactly one** option from a related set.
- The full list of options is short enough to show at once (typically ≤ 5 options).
- Seeing every option side-by-side helps the user choose — they're comparing alternatives, not searching.

Common surfaces: forms, modals, side panels, full pages, plan pickers, setting confirmations.

## When not to use

| Situation | Why | Use instead |
|-----------|-----|-------------|
| User can pick **more than one** option | Radio is single-select by definition | `Checkbox` / `CheckboxGroup` |
| Control toggles a setting that takes effect **immediately** | Two-option Radio reads as "pick A or B", not "flip this now" | `ToggleButton` |
| **Many** options and vertical space is constrained | Long list overflows and slows scanning | Single-select `Select` / dropdown |
| Purely **visual** / read-only indicator | A radio advertises interactivity | Plain text, `Tag`, or an icon |

---

## Do / Don't

### Pair 1 — Reach for Radio when exactly one option must be selected

#### ✅ Do — Use Radio for mutually-exclusive single-select

```tsx
const [plan, setPlan] = useState<'monthly' | 'annual'>('monthly');

<RadioGroup value={plan} onChange={(v: string) => setPlan(v as 'monthly' | 'annual')}>
  <Radio name="plan" label="Monthly billing" value="monthly" testId="radio-monthly" />
  <Radio name="plan" label="Annual billing"  value="annual"  testId="radio-annual" />
</RadioGroup>
```

#### ❌ Don't — Use Radio when more than one option can be selected

If the user can choose several options simultaneously, the affordance lies: arrow keys will silently switch the selection between unrelated items. Use `Checkbox` / `CheckboxGroup` instead.

```tsx
{/* Wrong — these are independent choices; use Checkbox */}
<RadioGroup value={selectedChannel} onChange={setSelectedChannel}>
  <Radio name="channels" label="Email" value="email" />
  <Radio name="channels" label="SMS"   value="sms" />
  <Radio name="channels" label="Push"  value="push" />
</RadioGroup>
```

---

### Pair 2 — Preselect a default option in every RadioGroup

#### ✅ Do — Ship a `RadioGroup` with one option already selected

> "It's important to know that for default view for a radio button group is to have one of them preselected." — Oxygen docs

```tsx
const [billing, setBilling] = useState('monthly'); // ← preselected

<RadioGroup value={billing} onChange={setBilling}>
  <Radio name="billing" label="Monthly" value="monthly" />
  <Radio name="billing" label="Annual"  value="annual" />
</RadioGroup>
```

#### ❌ Don't — Ship a `RadioGroup` with nothing selected

An unselected `RadioGroup` makes the keyboard pattern awkward and forces the user into an extra step.

```tsx
{/* Wrong — no default committed value */}
<RadioGroup value={undefined} onChange={setBilling}>
  <Radio name="billing" label="Monthly" value="monthly" />
  <Radio name="billing" label="Annual"  value="annual" />
</RadioGroup>
```

---

### Pair 3 — Always wrap related Radios in a `RadioGroup` with a group label

#### ✅ Do — Use `RadioGroup` and give the group an accessible name

```tsx
<>
  <h3 id="billing-cadence">Billing cadence</h3>
  <RadioGroup value={billing} onChange={setBilling} aria-labelledby="billing-cadence">
    <Radio name="billing" label="Monthly" value="monthly" testId="radio-monthly" />
    <Radio name="billing" label="Annual"  value="annual"  testId="radio-annual" />
  </RadioGroup>
</>
```

#### ❌ Don't — Free-float bare `Radio` components without a `RadioGroup` container

Without `RadioGroup`, the `radiogroup` role is absent: arrow keys won't roving-tabindex between options, and the group has no shared `name`.

```tsx
{/* Wrong — no group container, no shared selection state, no group label */}
<Radio name="r1" label="Monthly" value="monthly" />
<p>Some unrelated paragraph.</p>
<Radio name="r2" label="Annual"  value="annual" />
```

---

### Pair 4 — Reserve Radio for short lists; reach for `Select` when the list grows

#### ✅ Do — Use Radio when all options are visible at once

```tsx
<RadioGroup value={plan} onChange={setPlan}>
  <Radio name="plan" label="Basic"      value="basic" />
  <Radio name="plan" label="Standard"   value="standard" />
  <Radio name="plan" label="Enterprise" value="enterprise" />
</RadioGroup>
```

#### ❌ Don't — Stack 10+ options as Radios

A long vertical Radio list overflows and makes arrow-key navigation tedious.

```tsx
{/* Wrong — 200-row country picker; use Select instead */}
<RadioGroup value={country} onChange={setCountry}>
  <Radio name="country" label="Afghanistan" value="AF" />
  <Radio name="country" label="Albania"     value="AL" />
  {/* … 200 more rows … */}
</RadioGroup>
```

---

### Pair 5 — Put short text in `label`; put context in `infoBoxText`

#### ✅ Do — Keep `label` tight; use `infoBoxText` for the "why"

```tsx
<Radio
  name="plan"
  label="Enterprise plan"
  value="enterprise"
  testId="radio-enterprise"
  infoBoxText="Includes advanced features and dedicated support."
  infoBoxButtonLabel="More info about Enterprise plan"
/>
```

#### ❌ Don't — Pack the explanation into `label`

Long labels wrap (radio top-aligns to the first line) and defeat scanning.

```tsx
{/* Wrong — infoBoxText content crammed into label */}
<Radio
  name="plan"
  label="Enterprise plan — includes advanced features, dedicated support, SSO, audit logging, and 24/7 premium phone support."
  value="enterprise"
/>
```

---

### Pair 6 — Use horizontal layout only when labels are short and the set is small

#### ✅ Do — Use `isHorizontal` for binary or near-binary choices with short labels

```tsx
<RadioGroup value={answer} onChange={setAnswer} isHorizontal>
  <Radio name="confirm" label="Yes" value="yes" testId="radio-yes" />
  <Radio name="confirm" label="No"  value="no"  testId="radio-no" />
</RadioGroup>
```

#### ❌ Don't — Force a long-label list into a horizontal row

Horizontal layout breaks down once labels wrap or the row count exceeds three.

```tsx
{/* Wrong — long labels + horizontal = cramped, wrapped, hard to scan */}
<RadioGroup value={plan} onChange={setPlan} isHorizontal>
  <Radio name="plan" label="Basic — for individuals" value="basic" />
  <Radio name="plan" label="Standard — for small teams" value="standard" />
  <Radio name="plan" label="Enterprise — for organisations with advanced needs" value="enterprise" />
</RadioGroup>
```
