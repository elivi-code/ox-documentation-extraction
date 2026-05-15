---
component: TextField
package: "@8x8/oxygen-text-field"
category: form_inputs
role: usage
role_description: "Usage guidelines — editorially authored from extracted artifacts and the public Oxygen TextInput usage page; no Figma examples page exists"
pipeline_stage: editorial
pipeline_note: "Authored editorially from extracted artifacts + oxygen.8x8.com/components/textinput/usage — NOT from Figma Do/Don't frames. Re-run doc-audit after creation; replace pairs with figma-extract-usage output when a Figma examples page is created."
source_type: editorial
audit_verdict: null
siblings:
  - "[[TextField/props]]"
  - "[[TextField/examples]]"
  - "[[TextField/tokens]]"
  - "[[TextField/accessibility]]"
  - "[[TextField/figma]]"
  - "[[TextField/TextField-pui]]"
  - "[[TextField/TextField-audit]]"
tags:
  - oxygen
  - component/TextField
  - role/usage
  - stage/editorial
  - category/form_inputs
---
<!-- SOURCE: editorial — no Figma "↳ TextField examples" page exists -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run for this component -->
<!-- REFERENCE PAGE: https://oxygen.8x8.com/components/textinput/usage -->
<!-- GROUNDING: full — props.md, examples.md, accessibility.md, tokens.md, figma.md, TextField-pui.md, TextField-audit.md, oxygen.8x8.com/components/textinput/usage -->
<!-- DRAFTED: 2026-05-15 -->
<!-- MODE: open -->
<!-- PAIRS: 6 -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output when a Figma examples page is created -->

# TextField — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [figma.md](./figma.md) · [TextField-pui.md](./TextField-pui.md) · [TextField-audit.md](./TextField-audit.md)

> **Editorial guidance — not Figma-sourced.** No `↳ TextField examples` Figma page exists, so `figma-extract-usage` cannot run. The Do/Don't pairs below are grounded in `props.md`, `examples.md`, `accessibility.md`, and the public usage page at [oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage). Treat as provisional until a designer reviews them. Replace with `figma-extract-usage` output when a Figma examples page is created.

`TextField` is the canonical single-line input for short-to-moderate free-form text that **cannot be predicted with a fixed set of options** — names, emails, search strings, codes, prices. It is fixed-height, label-first, and the building block of every Oxygen form pattern.

---

## Anatomy

Per [oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage):

1. **Label** — always required; describes what the user is entering ([accessibility.md:36](./accessibility.md)).
2. **Required symbol** — the `*` rendered beside the label when `isRequired` is set ([props.md:74](./props.md)).
3. **Help icon** — the info-tooltip trigger driven by `infoBoxText` / `infoBoxButtonLabel` ([props.md:90–91](./props.md)).
4. **Field / Placeholder** — the input itself; placeholder is **optional and never a label substitute** (see Pair 2).
5. **Helper text** — the `description` prop rendered below the input, associated via `aria-describedby` ([props.md:68](./props.md); [accessibility.md:33](./accessibility.md)).

---

## When to use

- The user must enter **information that cannot be predicted with predetermined options** — names, emails, codes, free-form search terms ([oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage) — "When to use").
- The expected input is **short to moderate**, fits on one line, and the field can stay at a **fixed height** ([oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage) — Overview).
- The value benefits from inline affordances — currency prefix, unit suffix, leading icon, inline action — supplied via `prefix` / `suffix` / `iconLeft` / `iconRight` / `action` ([props.md:81–88](./props.md); [examples.md:126–148](./examples.md)).
- The field is part of a **form or data-collection pattern** where surrounding inputs are also `TextField`s, dropdowns, or checkboxes ([oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage) — Overview).

## When not to use

| Situation | Use instead |
|-----------|-------------|
| The user must pick **one option from a known list** | [Dropdown](../Dropdown/) — per [oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage) — "If the user must select a specific option from known choices, consider using a dropdown, radio button or checkbox instead." |
| The user must pick **one from a small mutually-exclusive set** | [Radio](../Radio/) — same source |
| The user must pick **zero or more from a small set** | [Checkbox](../Checkbox/) — same source |
| The user must enter **multi-line / paragraph** content | A multi-line text area (`<textarea>` — Oxygen does not yet ship a dedicated Textarea component; `TextField` is single-line and fixed-height per [oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage) Overview) |
| The user must enter a **bounded numeric value with arrow stepping** | A numeric input (inferred — common Oxygen UX rule; not stated on the TextInput usage page) |

---

## Do / Don't

<!-- SCREENSHOTS UNAVAILABLE — no Figma examples page exists for TextField -->

### Pair 1 — Use TextField for unpredictable free-form input; reach for Dropdown / Radio / Checkbox for known choices

#### ✅ Do — Use TextField when the value can't be predicted ahead of time

> Names, emails, search queries, referral codes, prices, free-form descriptions — anything where the user is **typing** rather than **picking** belongs in a TextField. Pair it with a clear `label` and, when constraints matter, a short `description` underneath.

```tsx
import { TextField } from '@8x8/oxygen-text-field';

<TextField
  label="Email"
  placeholder="you@company.com"
  description="We'll use this for account recovery."
  onChange={(e) => setValue(e.target.value)}
/>
```

**Grounded in:** [oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage) — "When to use: The user needs to input information that cannot be predicted with predetermined options."; [examples.md:30–48](./examples.md) (Basic + hint-text patterns).

#### ❌ Don't — Use TextField for a fixed set of known choices

> When the answer is one of "Phone / Email / SMS" or "Mon / Tue / Wed / Thu / Fri", a TextField makes the user type the option exactly right and forces validation. A Dropdown, Radio, or Checkbox set lets them pick the canonical value with zero typos.

```tsx
// ❌ Forcing the user to type a known value
<TextField
  label="Preferred contact method"
  placeholder="Phone, Email, or SMS"
/>

// ✅ Use the right control
// <Dropdown options={[{ value: 'phone', label: 'Phone' }, ... ]} />
// <RadioGroup options={[{ value: 'phone', label: 'Phone' }, ... ]} />
```

**Grounded in:** [oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage) — "When not to use: If the user must select a specific option from known choices, consider using a dropdown, radio button or checkbox instead."

---

### Pair 2 — Always provide a real `label`; never use `placeholder` as a label

#### ✅ Do — Pair every TextField with a persistent `label`

> A `<label>` element is read by every screen reader, stays visible after the user starts typing, and is a WCAG 2.1 AA requirement (1.3.1, 3.3.2). Oxygen's `label` prop wires up the `for` / `id` association automatically ([accessibility.md:36](./accessibility.md)). Use `placeholder` only for **example formatting** — the shape of the value the user is about to type — never to communicate what the field is for.

```tsx
<TextField
  label="Phone number"
  placeholder="+1 555 123 4567"
  description="Include country code."
  onChange={(e) => setPhone(e.target.value)}
/>
```

**Grounded in:** [oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage) — Anatomy + "Avoid using placeholders whenever possible as they are not accessible, never use them to communicate important information."; [accessibility.md:36](./accessibility.md) — "Always provide a `label` or a visible alternative; never rely on `placeholder` alone as a label."; WCAG 2.1 AA criteria 1.3.1 and 3.3.2 ([accessibility.md:66, 75](./accessibility.md)).

#### ❌ Don't — Use placeholder text as the only label

> Placeholder text **disappears the moment the user starts typing**, fails colour-contrast in many themes, and is announced inconsistently by screen readers. A placeholder-only field is invisible to anyone who tabs back to review the form or uses a screen reader to navigate it.

```tsx
// ❌ Placeholder-as-label — fails WCAG 1.3.1 and 3.3.2
<TextField placeholder="Email" />

// ❌ Even worse: communicating required info only in the placeholder
<TextField placeholder="Must be 8+ characters with one number" />

// ✅ Use label + description for instructions
<TextField
  label="Password"
  type="password"
  description="Must be 8+ characters with at least one number."
/>
```

**Grounded in:** [oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage) — "Avoid using placeholders whenever possible as they are not accessible, never use them to communicate important information."; [accessibility.md:36, 59](./accessibility.md) — "Placeholder text is read by most screen readers but is not a substitute for a persistent label."

---

### Pair 3 — Put instructional text in `description`, not in `placeholder`

#### ✅ Do — Use `description` for hints, constraints, and format guidance

> Helper text rendered below the field stays visible as the user types, is associated with the input via `aria-describedby` ([accessibility.md:33](./accessibility.md)), and is announced when the field receives focus. This is the right place for "Must be 3–20 characters", "Include country code", "We'll never share this", etc.

```tsx
<TextField
  label="Username"
  description="3–20 characters. Letters, numbers, and underscores only."
  placeholder="jane_doe"
  onChange={(e) => setUsername(e.target.value)}
/>
```

**Grounded in:** [props.md:68](./props.md) — "`description` — Hint / helper text rendered below the input"; [examples.md:42–48](./examples.md) "With hint text"; [accessibility.md:33](./accessibility.md) — "The hint/description text should also be linked via `aria-describedby`."

#### ❌ Don't — Pack constraints or warnings into the placeholder

> Once the user types one character, the placeholder is gone — along with the constraint. If the rule matters enough to state, it matters enough to stay visible.

```tsx
// ❌ Constraint vanishes on first keystroke
<TextField
  label="Username"
  placeholder="Must be 3–20 characters, letters and numbers only"
/>
```

**Grounded in:** [oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage) — "never use [placeholders] to communicate important information."

---

### Pair 4 — Use `isReadOnly` for visible-but-non-editable values; use `isDisabled` only when the field is genuinely unavailable

#### ✅ Do — Reach for `isReadOnly` when the user needs to see and copy a value but not change it

> Read-only inputs stay in the tab order, are announced as read-only by screen readers, and let users select and copy the value — ideal for system-assigned IDs, confirmed emails, generated codes ([accessibility.md:34, 80](./accessibility.md)). Disabled fields are removed from the tab order and disappear from keyboard navigation entirely.

```tsx
<TextField
  label="Account ID"
  value="ACC-00123"
  isReadOnly
/>
```

**Grounded in:** [props.md:72](./props.md); [examples.md:87–92](./examples.md) Read-only pattern; [accessibility.md:34, 80](./accessibility.md) — "If users need to see the value but not edit it, prefer `isReadOnly` instead, which keeps the field in the tab order and is announced by screen readers."

#### ❌ Don't — Disable a field just to display a value

> A disabled input is silent to assistive tech and skipped by keyboard navigation. If a user can read the value with their eyes but a screen reader user can't reach it, the form is broken.

```tsx
// ❌ User can't tab to it or copy the value with a screen reader
<TextField
  label="Account ID"
  value="ACC-00123"
  isDisabled
/>

// ✅ Read-only keeps the field in the tab order
<TextField
  label="Account ID"
  value="ACC-00123"
  isReadOnly
/>
```

Reserve `isDisabled` for fields that are temporarily unavailable because a prerequisite isn't met (e.g. "Billing address" disabled until "Same as shipping" is unchecked) — and in that case, explain *why* in nearby helper text.

**Grounded in:** [accessibility.md:35, 80](./accessibility.md) — "When `isDisabled` is set, the `disabled` attribute is present; disabled fields are removed from the tab order and not announced as interactive."

---

### Pair 5 — Show errors with `hasError` + descriptive text; never colour alone

#### ✅ Do — Combine `hasError` with an error message in `description`

> The error state must include a **text explanation** (WCAG 3.3.1) and visible non-colour signals — Oxygen's error border, icon, and text all activate together when `hasError` is set ([accessibility.md:67–68](./accessibility.md)). Move the error message into the `description` prop so it's linked via `aria-describedby` and read on focus.

```tsx
<TextField
  label="Email"
  type="email"
  value={email}
  hasError={!isValid}
  description={!isValid ? "Enter a valid email address (e.g. you@company.com)." : undefined}
  onChange={(e) => setEmail(e.target.value)}
/>
```

**Grounded in:** [examples.md:65–72](./examples.md) Error state pattern; [props.md:73](./props.md) — "`hasError` — Activates error visual state and shows error styling"; [accessibility.md:32, 58, 67, 74](./accessibility.md) — WCAG 3.3.1 + `aria-describedby` linkage.

#### ❌ Don't — Rely on red colour alone to communicate the error

> Users with low vision, colour-blindness, or in high-glare environments may not perceive a red border. Without a text explanation, they also won't know **what** is wrong or **how to fix it**.

```tsx
// ❌ Red border with no text — fails WCAG 1.4.1 and 3.3.1
<TextField label="Email" hasError />

// ❌ Even worse: vague helper that doesn't say what's wrong
<TextField label="Email" hasError description="Invalid." />

// ✅ Specific, actionable error text
<TextField
  label="Email"
  hasError
  description="This email is already registered. Try signing in instead."
/>
```

**Grounded in:** [accessibility.md:67–68, 74](./accessibility.md) WCAG 1.4.1 + 3.3.1 — "Error state must not rely on colour alone"; "Errors must be described in text. Use `hasError` + `description` with error message."

---

### Pair 6 — Size the field to the expected value; reserve `fullWidth` for stretching forms

#### ✅ Do — Match input width to the content the user is entering

> The Oxygen guidance is explicit: "Input width should be proportional to the content that the user has to insert and align to grid columns." A two-letter state code shouldn't stretch the page; a multi-segment search query shouldn't be squeezed into 120px. Use `size="small" | "default" | "large"` to set the visual scale and let containers + grid columns set the width.

```tsx
{/* Short, predictable values stay compact */}
<TextField label="ZIP" size="small" placeholder="94103" />

{/* Long search queries get full container width inside a form column */}
<TextField label="Search" iconLeft={SearchIcon} fullWidth placeholder="Search messages…" />
```

**Grounded in:** [oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage) — "Input width should be proportional to the content that the user has to insert and align to grid columns."; [props.md:79–80](./props.md) `size` and `fullWidth` props; [examples.md:97–112](./examples.md) Size variants + Full width patterns.

#### ❌ Don't — Stretch every input to the page width regardless of content

> A page where every input — ZIP code, state, country, email, address line 1 — sits at full width breaks the visual rhythm of the form and signals that all fields expect the same amount of content. It also wastes scan-time: the user can no longer infer the kind of value expected from the field's size.

```tsx
// ❌ Same width for every field, no signal of expected content length
<TextField label="ZIP" fullWidth />
<TextField label="State" fullWidth />
<TextField label="Country" fullWidth />
<TextField label="Email" fullWidth />
```

**Grounded in:** [oxygen.8x8.com/components/textinput/usage](https://oxygen.8x8.com/components/textinput/usage) — "Input width should be proportional to the content that the user has to insert and align to grid columns."

---

## Gaps & open questions

| ID | Type | Description |
|----|------|-------------|
| — | Editorial | These Do/Don't pairs are authored from extracted artifacts and the public oxygen.8x8.com TextInput usage page, **not from a Figma examples page**. They should be reviewed by a designer and replaced with Figma-sourced pairs once a `↳ TextField examples` page is created. |
| GAP-USAGE-001 | Source gap | No Figma examples page exists for TextField. The public usage page provides anatomy, behaviour, and a short "When to use / When not to use" — **no Do/Don't cards, no screenshots, no annotated examples**. A Figma examples page would let `figma-extract-usage` run and replace this editorial draft. |
| GAP-USAGE-002 | Source gap | The OX usage page does not address `prefix` / `suffix` / `iconLeft` / `iconRight` / `action` patterns. The guidance in the "When to use" list above is editorial, derived from [props.md:81–88](./props.md) and [examples.md:126–148](./examples.md). |
| GAP-USAGE-003 | Source gap | The OX usage page does not address `maxLength` ergonomics — when to show a live character count, when to truncate vs. block input, etc. Not covered in pairs above. |
| GAP-USAGE-004 | Source gap | The OX usage page does not address `labelOrientation="row"` (label-beside-input) — when to use it, density implications, RTL behaviour. The pattern is documented in [examples.md:153–159](./examples.md) but lacks an editorial recommendation. |
| GAP-USAGE-005 | Source gap | The OX usage page does not address multi-line text input. Pair "When not to use" row 4 above notes Oxygen ships no dedicated Textarea component — confirm with design before adopting an alternative pattern. |

---

_Source: editorial guidance authored from extracted artifacts (props.md, examples.md, accessibility.md, figma.md, TextField-pui.md, TextField-audit.md) and the public usage page at oxygen.8x8.com/components/textinput/usage · No Figma examples page available · 2026-05-15_
