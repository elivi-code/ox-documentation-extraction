---
parent: "[[Label]]"
section: usage
---

<!-- source: editorial — derived from extracted artifacts; published Oxygen docs page (/components/label/usage) returned HTTP 404 on 2026-05-13; no Figma "↳ Label examples" page exists -->

## Open conflicts

Two conflicts are unresolved and constrain what can be stated about token authority and the info-icon API:

- **CONFLICT (GAP-008) — Token name/size for label text.** MCP returns `label01` (12px); Figma resolves to `typography/body01` (14px). Pairs avoid prescribing a specific type-ramp token.
- **CONFLICT (GAP-017) — Figma `information` boolean ↔ Oxygen `infoBoxText` / `infoBoxButtonLabel` mapping.** Unverified. Pair 6 covers *when* to use the info affordance; prop-level guidance deferred.

## Anatomy

The Figma `_base_form_label` node composes Label from four numbered parts plus an optional inline action exposed only via the React API:

1. **Label text** — the visible string naming the associated control. Driven by `value`. Rendered with `text/textColor01`.
2. **Required asterisk `*`** *(optional)* — shown when `isRequired={true}`. Rendered with `error/error01`. Visual signal only — the programmatic required state must come from `aria-required="true"` (or native `required`) on the associated form control.
3. **Info icon button** *(optional)* — an Icon Button slot that opens an explanatory tooltip. Separate keyboard focus stop with its own accessible name from `infoBoxButtonLabel`; trigger behaviour controlled by `infoBoxShowOn`.
4. **Inline action link** *(optional, React only)* — via `action`, `actionLabel`, `actionTarget`, `otherActionProps`. Not represented as a Figma variant.

Additional React-only behaviours:

5. **Overflow tooltip** (`showTooltipOnOverflow`) — surfaces full label text when truncated.
6. **Wrapped text** (`shouldWrapText`) — allows the label string to break across multiple lines.

## Overview

| Component | Use for | Key props |
|-----------|---------|-----------|
| `Label` | Visible name of a form control — pair with Input, Checkbox, Select, etc. | `value`, `htmlFor`, `isRequired`, `isDisabled`, `shouldWrapText`, `showTooltipOnOverflow`, `action` + `actionLabel` + `actionTarget`, `infoBoxText` + `infoBoxShowOn` + `infoBoxButtonLabel` |
| `ActionTarget` *(type export)* | Type for the `actionTarget` prop | — |

Label renders an HTML `<label>` element. When `htmlFor` matches the `id` of a form control, the browser provides click-to-focus, screen-reader announcement, and programmatic association without extra ARIA.

## Behaviour

### Visible states

| # | State | Trigger | Effect |
|---|-------|---------|--------|
| 1 | Default | none | Label text in `text/textColor01`, horizontal layout |
| 2 | Required | `isRequired={true}` | Red `*` in `error/error01` |
| 3 | With info | `infoBoxText` set | Icon Button appears right of label text |
| 4 | Disabled | `isDisabled={true}` | Label visually muted (disabled visual is a SOURCE_GAP — Figma has no disabled variant) |
| 5 | Wrapped | `shouldWrapText={true}` | Text breaks across lines |
| 6 | Overflow tooltip | `showTooltipOnOverflow={true}` | Tooltip surfaces full text when truncated |
| 7 | Hover (info icon) | pointer over info button | Inherits Icon Button hover styles |

### Keyboard

| Key | Behaviour |
|-----|-----------|
| Click on label | Moves focus to form control referenced by `htmlFor` |
| `Tab` | Moves focus to the info icon button (separate focus stop, if present) |
| `Enter` / `Space` | Activates the info icon button or inline action link |

## Best Practices

### When to use

- To name a form control whose value the user is being asked to provide.
- When the control needs an inline secondary action that belongs to "this field" (e.g. "Forgot password?").
- When a field needs a brief explanatory tooltip (e.g. "Where do I find this?").
- For required-field signalling — pair `isRequired` on Label with `aria-required="true"` on the control.

### When not to use

| Situation | Why | Use instead |
|-----------|-----|-------------|
| You need helper or error text below the field | Helper/error text belongs to the form control's own slot | The host component's helper/error slot |
| You need a placeholder | Placeholders live inside the field and disappear on focus — they are not labels | `placeholder` on the control (sparingly) **plus** a real Label |
| You need a non-form heading | `<label>` semantics are reserved for form controls | A heading element or typography component |
| You need a clickable affordance with no associated control | `<label>` without an associated control has undefined click behaviour | A `Button` or `Link` |

## Do / Don't

> Derived editorially from extracted artifacts — no Figma Do/Don't cards and no published docs page exist for Label.

### Pair 1 — Always associate the Label with its control via `htmlFor`

#### ✅ Do

```tsx
<Label value="Email address" htmlFor="email" />
<Input id="email" />
```

#### ❌ Don't

```tsx
{/* Clicking the label does nothing; screen readers announce input with no name */}
<Label value="Email address" />
<Input id="email" />
```

---

### Pair 2 — Use `isRequired` for the required signal, not text inside `value`

#### ✅ Do

```tsx
<Label value="Password" htmlFor="password" isRequired />
<Input id="password" type="password" aria-required="true" />
```

#### ❌ Don't

```tsx
{/* Drift in style, no programmatic signal, screen reader reads "Password star" */}
<Label value="Password *" htmlFor="password" />
<Label value="Password (required)" htmlFor="password" />
```

---

### Pair 3 — Pair `isDisabled` on the Label with `isDisabled` on the control

#### ✅ Do

```tsx
<Label value="Username" htmlFor="username" isDisabled />
<Input id="username" isDisabled />
```

#### ❌ Don't

```tsx
{/* Label looks off, control is still focusable and editable */}
<Label value="Username" htmlFor="username" isDisabled />
<Input id="username" />
```

---

### Pair 4 — Pick one truncation strategy: wrap **or** tooltip-on-overflow, not both

#### ✅ Do

```tsx
{/* For stacked forms with vertical room */}
<Label value="A label with longer text that needs to wrap" htmlFor="my-input" shouldWrapText />

{/* For tight horizontal grids */}
<Label value="A very long label that might overflow" htmlFor="my-input" showTooltipOnOverflow />
```

#### ❌ Don't

```tsx
{/* Combining defeats both: wrap prevents the overflow the tooltip needs */}
<Label value="A very long label…" shouldWrapText showTooltipOnOverflow htmlFor="my-input" />
```

---

### Pair 5 — Reserve the inline `action` link for one affordance that belongs to "this field"

#### ✅ Do

```tsx
<Label
  value="Password"
  htmlFor="password"
  actionLabel="Forgot password?"
  action={() => navigate('/reset-password')}
/>
```

#### ❌ Don't

```tsx
{/* The action slot is for one secondary affordance, not a toolbar */}
<Label value="Password" actionLabel="Forgot password? · Reset · Generate" action={...} />

{/* Primary actions belong in a Button */}
<Label value="Save changes" actionLabel="Save" action={submitForm} />
```

---

### Pair 6 — Use the info icon for short context, not for instructions or required help

#### ✅ Do

```tsx
<Label
  value="API Key"
  htmlFor="api-key"
  infoBoxText="Your API key can be found in your account settings."
  infoBoxButtonLabel="More information about API key"
/>
```

#### ❌ Don't

```tsx
{/* Instructions belong in helper text on the control; tooltips disappear */}
<Label
  value="Password"
  infoBoxText="Must be 8+ characters, one uppercase, one digit, one symbol."
  infoBoxButtonLabel="Password rules"
/>
```

---

### Pair 7 — Keep label text short, sentence-case, and free of trailing punctuation

#### ✅ Do

```tsx
<Label value="Email address" htmlFor="email" />
<Label value="Password" htmlFor="password" />
<Label value="Phone number" htmlFor="phone" />
```

#### ❌ Don't

```tsx
{/* Instruction-shaped; sounds like a question */}
<Label value="Please enter your email address below:" htmlFor="email" />
{/* Title Case + colon noise */}
<Label value="Email Address:" htmlFor="email" />
{/* Verb-led; labels name the field, not the action */}
<Label value="Enter password" htmlFor="password" />
```

---

### Pair 8 — Stack the Label above the form control with consistent vertical rhythm

#### ✅ Do

```tsx
<div className="form-field">
  <Label value="Email address" htmlFor="email" />
  <Input id="email" />
</div>
<div className="form-field">
  <Label value="Password" htmlFor="password" isRequired />
  <Input id="password" type="password" />
</div>
```

#### ❌ Don't

```tsx
{/* Inline-left labels break form-row symmetry */}
<div style={{ display: 'flex' }}>
  <Label value="Email address" htmlFor="email" style={{ width: 120 }} />
  <Input id="email" />
</div>

{/* Placeholder as the label — fails WCAG 3.3.2 */}
<Input id="email" placeholder="Email address" />
```

---

## Accessibility quick reference

- Renders a native HTML `<label>` — programmatic association via `htmlFor` ↔ `id`.
- Clicking the Label moves focus to the associated control — native browser behaviour.
- `isRequired` paints the visual `*` only — programmatic required state must come from `aria-required="true"` on the control.
- `isDisabled` mutes the Label visually but does not suppress AT announcement — pair with `isDisabled` on the control.
- The info button is a **separate focus stop** — always supply `infoBoxButtonLabel`.
- WCAG 2.1 AA criteria: 1.3.1, 1.4.3, 2.1.1, 2.4.6, 3.3.2, 4.1.2 — see [[Label.accessibility]].

## Related components

- **`Input`** — most common Label pairing; helper text and error slot live on Input, not Label.
- **`Checkbox`** — bundles its own internal label via the `label` prop; do not wrap Checkbox with this Label.
- **`Select`** — accepts a Label via `htmlFor` like Input.
- **`Button`** — for primary actions or any clickable affordance not tied to a single form field.

_Source: Editorial — derived from source files. Published Oxygen Label docs page returned 404 on 2026-05-13. No Figma examples page exists._
