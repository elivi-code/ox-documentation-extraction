---
component: Label
package: "@8x8/oxygen-label"
category: data_display
role: usage
role_description: "Usage guidelines — Do/Don't editorial guidance, derived from extracted MCP/Figma artifacts (no Figma Do/Don't cards and no published docs page)"
pipeline_stage: editorial
pipeline_note: "Authored editorially on 2026-05-13. The Figma '↳ Label examples' page does not exist, so figma-extract-usage cannot run. The published Oxygen docs page at https://oxygen.8x8.com/components/label/usage returns HTTP 404 (fetched 2026-05-13 via WebFetch). Do/Don't pairs are derived end-to-end from props.md, examples.md, tokens.md, accessibility.md, Label-figma.md, and label-pui.md, cross-validated against label-audit.md. Re-run /doc-audit Label after creation. Replace pairs with figma-extract-usage output if a Figma examples page is ever populated with Do/Don't cards, or transcribe verbatim once the published Label docs page goes live."
source_type: editorial
audit_verdict: null
siblings:
  - "[[Label/props]]"
  - "[[Label/examples]]"
  - "[[Label/tokens]]"
  - "[[Label/accessibility]]"
  - "[[Label/Label-figma]]"
  - "[[Label/label-pui]]"
  - "[[Label/label-audit]]"
tags:
  - oxygen
  - component/Label
  - role/usage
  - stage/editorial
  - category/data_display
---
<!-- SOURCE: editorial — derived from extracted MCP/Figma artifacts. Published Oxygen docs page (/components/label/usage) returned HTTP 404 on 2026-05-13; no Figma "↳ Label examples" page with Do/Don't cards exists. -->
<!-- FIGMA EXAMPLES PAGE: absent — figma-extract-usage cannot run -->
<!-- PUBLISHED DOCS PAGE: 404 — fetched 2026-05-13 via WebFetch -->
<!-- GROUNDING: full — props.md, examples.md, tokens.md, accessibility.md, Label-figma.md, label-pui.md, label-audit.md -->
<!-- DRAFTED: 2026-05-13 -->
<!-- MODE: derivation-only -->
<!-- PAIRS: 8 (derived from extracted artifacts cross-validated against accessibility, Figma anatomy, and the props API) -->
<!-- STATUS: editorial draft — replace with figma-extract-usage output if/when a Figma "↳ Label examples" page is created, or transcribe verbatim once the published Label docs page goes live. -->

# Label — Usage Guidelines

> **See also:** [props.md](./props.md) · [examples.md](./examples.md) · [tokens.md](./tokens.md) ·
> [accessibility.md](./accessibility.md) · [Label-figma.md](./Label-figma.md)

> **Editorial guidance — derived from extracted artifacts.** Neither a Figma `↳ Label examples` page with Do/Don't cards nor a published Oxygen docs page exists today. The published URL `https://oxygen.8x8.com/components/label/usage` returned **HTTP 404** when fetched on 2026-05-13. Pairs below are derived from [props.md](./props.md), [examples.md](./examples.md), [tokens.md](./tokens.md), [accessibility.md](./accessibility.md), [Label-figma.md](./Label-figma.md), and [label-pui.md](./label-pui.md), cross-validated against the audit findings in [label-audit.md](./label-audit.md). Format follows the [DataTable-usage.md](../DataTable/DataTable-usage.md) precedent. Replace with `figma-extract-usage` output once a Figma examples page is created.

Label is the textual identifier that names what a form control is asking for. It is the canonical pairing partner for `Input`, `Checkbox`, `Select`, and other Oxygen form components — rendered as a native HTML `<label>` element so it inherits the browser's built-in "click the label, focus the control" behaviour and screen-reader announcement. A well-formed Label is short, action-shaped, programmatically associated with its control via `htmlFor`, and consistent in placement and rhythm across the form surface. See [accessibility.md:33-42](./accessibility.md) and [props.md:64-75](./props.md).

---

## ⚠️ Open audit conflicts

Two conflicts in [label-audit.md](./label-audit.md) are unresolved at the time of writing. They **do not block** the editorial guidance below, but they constrain what you can confidently say about token authority and the info-icon API.

- **CONFLICT — Token name/size for label text.** The Oxygen MCP returns `label01` (Inter 12px / 16px line height, weight 400) at [tokens.md:30-45](./tokens.md). Figma resolves the same surface to `typography/body01` (Inter 14px / 20px, weight 400) at [Label-figma.md:130](./Label-figma.md). One is authoritative for the React `Label` component — the other is a parallel ramp used elsewhere. The pairs below therefore avoid prescribing a specific type-ramp token; rules are stated at the "use the canonical component, don't restyle" level rather than at the token level. Tracked under `scores.tokens` in [label-audit.md](./label-audit.md).
- **CONFLICT — Figma `information` boolean ↔ Oxygen `infoBoxText` / `infoBoxButtonLabel` mapping.** [Label-figma.md:79-80](./Label-figma.md) shows a single boolean `information` that shows/hides an Icon Button slot. The React API exposes three related props — `infoBoxText`, `infoBoxShowOn`, `infoBoxButtonLabel` ([props.md:74-77](./props.md)) — and the exact mapping is unverified. Pairs that talk about *whether* to use the info affordance are fine and grounded in [accessibility.md:59-61](./accessibility.md); pairs that talk about *which* prop drives the visibility are deferred. Tracked in the [Label-figma.md:211](./Label-figma.md) Gaps & conflicts table.

---

## Anatomy

The Figma `_base_form_label` node ([Label-figma.md:47-56](./Label-figma.md)) composes the Label from up to four numbered parts plus an optional inline action exposed only via the React API:

1. **Label text** — the visible string that names the associated control. Driven by the `value` prop ([props.md:65](./props.md)). Rendered with `text/textColor01` (`#26252A` Light / `#FFFFFF` Dark) at [Label-figma.md:107](./Label-figma.md). The published Oxygen MCP and Figma disagree on the type ramp — see Conflict above.
2. **Required asterisk `*`** *(optional)* — shown when `isRequired={true}` ([props.md:66](./props.md), [Label-figma.md:80](./Label-figma.md)). Rendered with `error/error01` (`#CB2233` Light / `#F24D5F` Dark) at [Label-figma.md:115](./Label-figma.md). The asterisk is a **visual** signal only — the programmatic required signal must come from `aria-required="true"` (or the native `required` attribute) on the associated form control. The label itself does not carry the requirement state.
3. **Info icon button** *(optional)* — an `Icon Button` slot ([Label-figma.md:55](./Label-figma.md), [Label-figma.md:60-64](./Label-figma.md)) that opens an explanatory tooltip on hover or click. It is a **separate keyboard focus stop** with its own accessible name supplied by `infoBoxButtonLabel`; trigger behaviour is controlled by `infoBoxShowOn` (e.g. `hover`, `click` — see [accessibility.md:59-61](./accessibility.md)).
4. **Inline action link** *(optional, React only)* — exposed via the `action`, `actionLabel`, `actionTarget`, and `otherActionProps` props ([props.md:70-73](./props.md)). Used for adjacent affordances like "Forgot password?" next to a password field. Not represented as a Figma variant on the current `_base_form_label` node — its visual is therefore best-effort.

Two additional behaviours are exposed by the React API but not numbered in Figma anatomy:

5. **Overflow tooltip** *(`showTooltipOnOverflow`)* — a tooltip surfaces the full label text when it is truncated in a narrow container ([props.md:69](./props.md), [accessibility.md:65-67](./accessibility.md)).
6. **Wrapped text** *(`shouldWrapText`)* — allows the label string to break across multiple lines instead of truncating ([props.md:68](./props.md)).

> **Layout.** The Figma anatomy uses a horizontal H Stack with `items-center`, a 4 px hardcoded gap between the label text and the icon button, and the icon button wrapper itself has 2 px padding and a 6 px corner radius ([Label-figma.md:150-156](./Label-figma.md)). The hardcoded values are flagged as missing spacing tokens — tracked under the Gaps table below.

**Source:** [Label-figma.md:47-99](./Label-figma.md) · [props.md:62-77](./props.md) · [accessibility.md:33-67](./accessibility.md).

---

## Overview

A single Oxygen package, `@8x8/oxygen-label`, exports one component plus a typed export for `actionTarget` ([props.md:54-85](./props.md)):

| Component | Use for | Key props |
|-----------|---------|-----------|
| `Label` | The visible name of a form control — paired with `Input`, `Checkbox`, `Select`, etc. | `value`, `htmlFor`, `isRequired`, `isDisabled`, `shouldWrapText`, `showTooltipOnOverflow`, `action` + `actionLabel` + `actionTarget`, `infoBoxText` + `infoBoxShowOn` + `infoBoxButtonLabel` |
| `ActionTarget` *(secondary export)* | Type for the `actionTarget` prop — values like `_blank`, `_self` | — |

A Label renders an HTML `<label>` element. When `htmlFor` matches the `id` of a form control, the browser provides:

- **Click affordance.** Clicking the label moves keyboard focus to the associated control ([accessibility.md:46](./accessibility.md)).
- **Screen-reader announcement.** Assistive technology announces the label text when the user reaches the associated control.
- **Programmatic association.** The connection is exposed via the accessibility tree without extra ARIA — see WCAG 1.3.1 in [accessibility.md:79](./accessibility.md).

This is the foundational reason every example in [examples.md](./examples.md) — basic, required, disabled, with-action, with-info-box, overflow-tooltip, wrapped-text — passes `htmlFor` and an associated `id` on the next control.

---

## Behaviour

### Visible states

The Figma `_base_form_label` node currently exposes only a `mode` variant axis (`light` / `dark`) plus the two boolean toggles `information` and `isRequired` ([Label-figma.md:71-81](./Label-figma.md)). React-level states like disabled, wrapped, and overflow-tooltip are not represented as Figma variants — they are surfaced only by props.

| # | State | Trigger | Visual / behavioural effect |
|---|-------|---------|----------------------------|
| 1 | Default | none | Label text in `text/textColor01`, horizontal layout |
| 2 | Required | `isRequired={true}` | Red asterisk `*` rendered in `error/error01` |
| 3 | With info | `infoBoxText` set (and supporting `infoBox*` props) | Icon button slot appears to the right of the label text; opens tooltip on the trigger configured by `infoBoxShowOn` |
| 4 | Disabled | `isDisabled={true}` | Label muted visually — **not represented as a Figma variant** ([Label-figma.md:212](./Label-figma.md)); see Conflict / Source-gap discussion in the audit |
| 5 | Wrapped | `shouldWrapText={true}` | Label text breaks across multiple lines rather than truncating |
| 6 | Overflow tooltip | `showTooltipOnOverflow={true}` | When the label is truncated by its container, a tooltip surfaces the full text on hover/focus |
| 7 | Hover on info icon | pointer over info button | Inherits Icon Button hover styling ([Label-figma.md:174-176](./Label-figma.md)) |

> ⚠️ **Disabled visual is a SOURCE_GAP.** The disabled treatment for the label text itself is not represented in Figma. The React `Label` accepts `isDisabled` and the prop is documented, but the canonical muted colour token is not asserted by either MCP or Figma. Tracked in [Label-figma.md:212](./Label-figma.md). The pairs below talk about *pairing the prop with the control's disabled state*, not about the specific muted colour.

### Keyboard

| Key | Behaviour |
|-----|-----------|
| `Click` on label | Moves focus to the form control referenced by `htmlFor` ([accessibility.md:46](./accessibility.md)) |
| `Tab` | Moves focus into the info icon button if present (separate focus stop) ([accessibility.md:71](./accessibility.md)) |
| `Enter` / `Space` | Activates the info icon button or the inline action link ([accessibility.md:72](./accessibility.md)) |

**Source:** [Label-figma.md:71-91](./Label-figma.md) · [props.md:64-77](./props.md) · [accessibility.md:66-73](./accessibility.md).

---

## Best Practices

### When to use

- To name a form control whose value the user is being asked to provide — input, textarea, select, checkbox, radio group, toggle, etc.
- When the control needs an inline secondary action that semantically belongs to "this field" (e.g. "Forgot password?" next to a password input).
- When a field needs a brief explanatory tooltip that's longer than a placeholder allows but shorter than helper text deserves (e.g. "Where do I find this?").
- For required-field signalling — pair `isRequired` on the Label with `aria-required="true"` (or the native `required` attribute) on the control.

### When not to use

| Situation | Why | Use instead |
|-----------|-----|-------------|
| You need helper or error text below the field | Helper text is the responsibility of the form control's own slot (e.g. Input's helper-text affordance), not the Label | The host component's helper/error slot — see [Input-usage.md](../Input/Input-usage.md) |
| You need a placeholder | Placeholders live inside the field's value affordance and disappear on focus — they are not labels | `placeholder` on the control (sparingly) **plus** a real Label |
| You need a non-form heading | `<label>` semantics are reserved for form controls; using it for arbitrary section titles confuses assistive technology | A heading element (`h2`–`h4`) or `Heading`/`Title` typography component |
| You need a clickable affordance with no associated control | `<label>` exists to forward focus — without an associated control its click behaviour is undefined | A `Button` or `Link` |

**Source:** [accessibility.md:33-46](./accessibility.md) (native `<label>` semantics and `htmlFor` association) · [props.md:62-77](./props.md) · [Input-usage.md](../Input/Input-usage.md) (helper/error pattern lives on the form control, not the Label).

---

## Do / Don't

> These pairs are derived editorially from the extracted artifacts. No Figma ✅ Do / ❌ Don't card frames exist for Label at the time of writing (the `↳ Label examples` page is absent) and no published docs page exists either. Replace pairs verbatim if a Figma examples page is created with Do/Don't cards.

### Pair 1 — Always associate the Label with its control via `htmlFor`

**Grounded in:** [accessibility.md:40-46](./accessibility.md) (native `<label>` + `htmlFor` association), [accessibility.md:79](./accessibility.md) (WCAG 1.3.1), [examples.md:34](./examples.md) (every example shows the pairing).

#### ✅ Do — Pass `htmlFor` and match the `id` on the next control

```tsx
<Label value="Email address" htmlFor="email" />
<Input id="email" />
```

The browser then routes label clicks to the input, and screen readers read "Email address, edit text" instead of just "edit text".

#### ❌ Don't — Ship a Label with no `htmlFor`

```tsx
{/* Wrong — clicking the label does nothing; screen readers announce the input with no name */}
<Label value="Email address" />
<Input id="email" />
```

Without the association, the visual pairing is purely cosmetic. Sighted mouse users can still aim at the field, but keyboard users get no focus hop, and assistive technology has no programmatic relationship to read.

---

### Pair 2 — Use `isRequired` for the required signal, not text inside `value`

**Grounded in:** [props.md:66](./props.md) (`isRequired` prop), [Label-figma.md:80-81](./Label-figma.md) (Figma `isRequired` boolean drives the `*`), [accessibility.md:50-52](./accessibility.md) (required indicator + `aria-describedby` pattern), [examples.md:42](./examples.md).

#### ✅ Do — Set `isRequired` and let Oxygen render the indicator

```tsx
<Label value="Password" htmlFor="password" isRequired />
<Input id="password" type="password" aria-required="true" />
```

The component renders the consistent `*` in `error/error01` ([Label-figma.md:115](./Label-figma.md)) and design-system audits stay reliable. Pair `aria-required="true"` (or the native `required` attribute) on the input so assistive technology hears the constraint, not just sees it.

#### ❌ Don't — Bake the indicator into the label text

```tsx
{/* Wrong — drift in style, no programmatic signal, screen reader reads "Password star" */}
<Label value="Password *" htmlFor="password" />
{/* Wrong — verbose, inconsistent across the form, breaks translation */}
<Label value="Password (required)" htmlFor="password" />
```

Inline `*` or `(required)` lose the token-driven colour, can't be localised independently of the label text, and turn into noise when an English screen reader reads "Password asterisk".

---

### Pair 3 — Pair `isDisabled` on the Label with `isDisabled` on the control

**Grounded in:** [accessibility.md:54-56](./accessibility.md) (Label `isDisabled` is visual only — the assistive-tech signal must come from the control's own `aria-disabled`), [props.md:67](./props.md), [examples.md:48](./examples.md).

#### ✅ Do — Disable the Label and the control together

```tsx
<Label value="Username" htmlFor="username" isDisabled />
<Input id="username" isDisabled />
```

Visual muting on the Label communicates "this field is off" to sighted users; `isDisabled` on the control supplies the `disabled` attribute / `aria-disabled="true"` that assistive technology actually uses to announce the state ([accessibility.md:55](./accessibility.md)).

#### ❌ Don't — Disable only the Label and leave the control interactive (or vice versa)

```tsx
{/* Wrong — label looks off, control is still focusable and editable */}
<Label value="Username" htmlFor="username" isDisabled />
<Input id="username" />
```

A muted Label paired with a live Input lies to sighted users about the field's availability and tells assistive technology nothing — the user can still tab into the input, type, and submit. The two states have to move in lockstep.

---

### Pair 4 — Pick one truncation strategy: wrap **or** tooltip-on-overflow, not both

**Grounded in:** [props.md:68-69](./props.md) (`shouldWrapText`, `showTooltipOnOverflow`), [examples.md:78-95](./examples.md).

#### ✅ Do — Choose `shouldWrapText` for stacked forms with vertical room

```tsx
<Label
  value="A label with longer text that needs to wrap across multiple lines"
  htmlFor="my-input"
  shouldWrapText
/>
<Input id="my-input" />
```

Or choose `showTooltipOnOverflow` for tight horizontal grids where vertical drift breaks the row rhythm:

```tsx
<Label
  value="A very long label that might overflow its container"
  htmlFor="my-input"
  showTooltipOnOverflow
/>
<Input id="my-input" />
```

#### ❌ Don't — Enable both, or leave both off when overflow is likely

```tsx
{/* Wrong — wrap defeats the tooltip-on-overflow trigger; the tooltip never fires */}
<Label value="A very long label…" shouldWrapText showTooltipOnOverflow htmlFor="my-input" />

{/* Wrong — overflow clips silently; sighted users see "A very long lab…" with no recourse */}
<Label value="A very long label that might overflow its container" htmlFor="my-input" />
```

Combining `shouldWrapText` and `showTooltipOnOverflow` is contradictory: wrapping prevents the overflow that the tooltip is designed to surface, so the tooltip never fires. Leaving both off in a tight container lets the browser hard-clip the string — sighted users lose the latter part of the label and keyboard users get nothing to fall back to.

---

### Pair 5 — Reserve the inline `action` link for **one** affordance that belongs to "this field"

**Grounded in:** [props.md:70-73](./props.md) (`action`, `actionLabel`, `actionTarget`, `otherActionProps`), [examples.md:54-62](./examples.md) (canonical "Forgot password?" example).

#### ✅ Do — Use one short action link for a per-field secondary affordance

```tsx
<Label
  value="Password"
  htmlFor="password"
  actionLabel="Forgot password?"
  action={() => navigate('/reset-password')}
/>
<Input id="password" type="password" />
```

The Oxygen example sets the pattern: a single inline action sits to the right of the field name and points at a destination semantically tied to that field — "Forgot password?", "Generate", "Reset", "Learn how to find this".

#### ❌ Don't — Stack multiple actions inside the Label, or use it as a primary submit affordance

```tsx
{/* Wrong — the Label's action slot is for one secondary affordance, not a toolbar */}
<Label value="Password" actionLabel="Forgot password? · Reset · Generate" action={...} />

{/* Wrong — primary actions belong in a Button, not embedded in the Label */}
<Label value="Save changes" actionLabel="Save" action={submitForm} />
```

Stacking multiple inline links in the Label clutters the row, ambiguates the accessible name of the action, and competes with the primary Submit button for visual weight. Use a `Button` for primary actions; reserve the Label's action slot for a single, field-scoped secondary link.

---

### Pair 6 — Use the info icon for short context, not for instructions or required help

**Grounded in:** [accessibility.md:59-61](./accessibility.md) (info button is a separate focus stop with its own accessible name from `infoBoxButtonLabel`), [Label-figma.md:55](./Label-figma.md) (Icon Button slot), [props.md:74-77](./props.md). *(See the CONFLICT note above — this pair addresses **when** to use the info affordance, not which props are authoritative.)*

#### ✅ Do — Put short, "what does this mean?" copy in the info tooltip — and always supply `infoBoxButtonLabel`

```tsx
<Label
  value="API Key"
  htmlFor="api-key"
  infoBoxText="Your API key can be found in your account settings."
  infoBoxButtonLabel="More information about API key"
/>
<Input id="api-key" />
```

Reach for the info icon when the user needs orientation about what the field is — provenance, expected format, where to find the value, why we ask. Keep it to one or two sentences. `infoBoxButtonLabel` is required for the button to have an accessible name — without it the trigger is announced as an unnamed button ([accessibility.md:59-60](./accessibility.md)).

#### ❌ Don't — Use the info icon for instructions, format hints, or error guidance

```tsx
{/* Wrong — instructions and format hints belong in helper text on the control, not inside a hover tooltip */}
<Label
  value="Password"
  infoBoxText="Must be 8+ characters, include one uppercase letter, one digit, and one symbol. Cannot reuse the last 5 passwords."
  infoBoxButtonLabel="Password rules"
/>

{/* Wrong — error guidance belongs in the control's error slot so it persists; tooltips disappear */}
<Label
  value="Email"
  infoBoxText="That email is already registered. Try signing in instead."
  infoBoxButtonLabel="Email error"
/>
```

Instructions and format hints need to be visible the whole time the user is typing — that's helper text on the form control itself. Error guidance must persist after focus moves on — that's the control's error slot. The info tooltip is "orientation on demand", not "guidance you need while typing".

---

### Pair 7 — Keep label text short, sentence-case, and free of trailing punctuation

**Grounded in:** [accessibility.md:82](./accessibility.md) (WCAG 2.4.6 — labels descriptive enough to identify the purpose), the recurring pattern in [examples.md](./examples.md) where every example uses 1–3 word labels with no terminal punctuation, and consistency with [Input-usage.md](../Input/Input-usage.md) Pair 7.

#### ✅ Do — Use 1–3 word labels in sentence case, with no terminal punctuation

```tsx
<Label value="Email address" htmlFor="email" />
<Label value="Password" htmlFor="password" />
<Label value="Phone number" htmlFor="phone" />
```

Sentence case scans faster than Title Case, matches OS-level form conventions, and avoids capitalising prepositions inconsistently. Skipping trailing colons or periods keeps the visual rhythm clean across the form and prevents screen readers from announcing "Email address colon".

#### ❌ Don't — Write sentence-shaped or punctuated labels

```tsx
{/* Wrong — instruction-shaped; sounds like the field is a question */}
<Label value="Please enter your email address below:" htmlFor="email" />

{/* Wrong — Title Case + colon noise; ugly in dense grids */}
<Label value="Email Address:" htmlFor="email" />

{/* Wrong — verb-led; labels should name the field, not narrate the action */}
<Label value="Enter password" htmlFor="password" />
```

Long, sentence-shaped labels stretch form rows unpredictably, fight with `showTooltipOnOverflow`, and waste screen-reader time on filler words. Reserve verbs and full sentences for helper text on the control.

---

### Pair 8 — Stack the Label above the form control with consistent vertical rhythm

**Grounded in:** [Input-usage.md](../Input/Input-usage.md) (precedent — Label above Input is the canonical Oxygen form-row pattern), the `Label` → `Input` ordering in every snippet in [examples.md](./examples.md), and [Label-figma.md:159-165](./Label-figma.md) (horizontal auto-layout inside the Label itself; the Label-to-control gap is owned by the form layout).

#### ✅ Do — Place the Label directly above the control, with a consistent gap across the form

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

A single repeating Label-then-control rhythm — same gap, same alignment to the left edge — makes the form scannable, lets sighted users predict where the next field begins, and gives keyboard users a reliable mental model of which Label belongs to which control.

#### ❌ Don't — Free-float Labels, mix left-aligned and stacked patterns, or skip the Label entirely on "obvious" fields

```tsx
{/* Wrong — inline-left labels break form-row symmetry and clash with Oxygen's stacked default */}
<div style={{ display: 'flex' }}>
  <Label value="Email address" htmlFor="email" style={{ width: 120 }} />
  <Input id="email" />
</div>

{/* Wrong — relying on the placeholder as the label; both visually and programmatically broken */}
<Input id="email" placeholder="Email address" />

{/* Wrong — Label visually associated by proximity only, no htmlFor, two controls share the visual space */}
<Label value="Phone" />
<Input id="phone-country" />
<Input id="phone-number" />
```

Inline-left labels are a different design pattern than Oxygen's default stacked rhythm — mixing them within one form breaks visual scanning. Replacing the Label with a placeholder erases the affordance the moment the user starts typing and fails WCAG 3.3.2 (Labels or Instructions). Ambiguous Label-to-control proximity (one Label "covering" two fields) leaves screen-reader users with no way to tell which input is being named.

---

## Accessibility quick reference

Cross-references to [accessibility.md](./accessibility.md):

- Renders a native HTML `<label>` — implicit `role="none"`, programmatic association via `htmlFor` ↔ `id` ([accessibility.md:33-46](./accessibility.md)).
- Clicking the Label moves focus to the associated control — native browser behaviour, not a JS handler ([accessibility.md:46](./accessibility.md)).
- `isRequired` paints the visual `*` only. Programmatic required state must come from `aria-required="true"` (or the native `required` attribute) on the associated control ([accessibility.md:50-52](./accessibility.md)).
- `isDisabled` mutes the Label visually but **does not** suppress assistive-technology announcement; pair with `isDisabled` on the control to convey the disabled state through `aria-disabled` ([accessibility.md:54-56](./accessibility.md)).
- The info button (`infoBoxText` + `infoBoxButtonLabel`) is a **separate focus stop**. Always supply `infoBoxButtonLabel` — without it the trigger has no accessible name ([accessibility.md:59-61](./accessibility.md)).
- When `showTooltipOnOverflow` is on, the tooltip content must be reachable by keyboard and announced by assistive technology — verify with the surface's testing tools ([accessibility.md:65-67](./accessibility.md)).
- WCAG 2.1 AA criteria explicitly addressed by Label: 1.3.1 (Info and Relationships), 1.4.3 (Contrast), 2.1.1 (Keyboard), 2.4.6 (Headings and Labels), 3.3.2 (Labels or Instructions), 4.1.2 (Name, Role, Value) — see [accessibility.md:78-86](./accessibility.md).

---

## Related components

- **`Input`** — the most common Label pairing. Form-row rhythm, helper text, and error slot live on Input, not on the Label. See [Input-usage.md](../Input/Input-usage.md).
- **`Checkbox`** — bundles its own internal label via the `label` prop; do **not** wrap a Checkbox with this Label component. See [Checkbox/checkbox-usage.md](../Checkbox/checkbox-usage.md) Pair 4.
- **`Select`** — accepts a Label alongside it via `htmlFor` like Input.
- **`Button`** — for primary actions or any clickable affordance that does not belong to a single form field; do not use the Label's inline `action` slot as a Button substitute. See Pair 5.

---

## Gaps

| Item | Type | Description |
|------|------|-------------|
| Figma Do/Don't examples | SOURCE_GAP | No `↳ Label examples` Figma page with Do/Don't card frames exists. Pairs above are editorially derived from extracted artifacts. Re-run `figma-extract-usage` if such a page is created. |
| Published docs page | SOURCE_GAP | `https://oxygen.8x8.com/components/label/usage` returned HTTP 404 on 2026-05-13 — verify the URL with the Oxygen docs team or wait for publication, then transcribe verbatim. |
| Token authority for label text | CONFLICT (see [label-audit.md](./label-audit.md) `scores.tokens`) | MCP says `label01` (12px); Figma says `typography/body01` (14px). Pairs avoid prescribing a specific ramp until resolved. |
| Info-icon prop mapping | CONFLICT (see [Label-figma.md:211](./Label-figma.md)) | Figma `information` boolean ↔ Oxygen `infoBoxText` / `infoBoxButtonLabel` mapping unverified. Pair 6 addresses *when* to use the affordance, not which prop drives it. |
| Disabled visual treatment | SOURCE_GAP (see [Label-figma.md:212](./Label-figma.md)) | The `isDisabled` state is not represented as a Figma variant on the `_base_form_label` node. Pair 3 talks about the prop pairing, not the muted colour token. |
| `shouldWrapText` / `showTooltipOnOverflow` variants | SOURCE_GAP (see [Label-figma.md:213](./Label-figma.md)) | Neither behaviour is represented as a Figma variant; specs live only in the React API. |
| Hardcoded spacing | DOC_GAP (see [Label-figma.md:206-208](./Label-figma.md)) | H Stack gap (4 px), Icon Button padding (2 px), and corner radius (6 px) have no token bindings. Pair 8 talks about form-row rhythm at the form-layout level rather than at the Label's internal spacing. |
| Inline-action prop signatures | DOC_GAP (GAP-002 in [label-audit.md](./label-audit.md)) | `action` is typed as `ActionProps['action']` without the underlying signature documented. Pair 5 uses a `() => void` shape pulled from the [examples.md:54](./examples.md) snippet — replace with the canonical signature once `ActionProps` is documented. |
| Editorial "When not to use" | DOC_GAP | The four "When not to use" rows above are editorial — they have no published-docs source to anchor to, since no Label docs page exists. <!-- TODO: confirm rows with the Oxygen team and either promote to published docs or trim. --> |

---

## Editorial derivation trail

> Axis-selection audit trail — kept in-file to avoid a separate `label-usage-draft.md` that goes stale.

### Grounding

- **Files used:** [props.md](./props.md), [examples.md](./examples.md), [tokens.md](./tokens.md), [accessibility.md](./accessibility.md), [Label-figma.md](./Label-figma.md), [label-pui.md](./label-pui.md), [label-audit.md](./label-audit.md). All seven expected sources present.
- **Published docs page:** `https://oxygen.8x8.com/components/label/usage` returned **HTTP 404** on 2026-05-13. Pairs are derived end-to-end from extracted artifacts.
- **Internal precedent scanned:** [Checkbox/checkbox-usage.md](../Checkbox/checkbox-usage.md), [Input/Input-usage.md](../Input/Input-usage.md), [DataTable/DataTable-usage.md](../DataTable/DataTable-usage.md), [Button/Button-usage.md](../Button/Button-usage.md), [Accordion/Accordion-usage.md](../Accordion/Accordion-usage.md). DataTable is the closest format match (derivation-only, no docs page).

### Axes considered

| # | Axis | Grounded in | Outcome |
|---|------|-------------|---------|
| 1 | `htmlFor` association | [accessibility.md:40-46](./accessibility.md), WCAG 1.3.1 | → Pair 1 |
| 2 | `isRequired` indicator vs. text in `value` | [props.md:66](./props.md), [Label-figma.md:80](./Label-figma.md) | → Pair 2 |
| 3 | `isDisabled` paired with control state | [accessibility.md:54-56](./accessibility.md) | → Pair 3 |
| 4 | `shouldWrapText` vs. `showTooltipOnOverflow` | [props.md:68-69](./props.md) | → Pair 4 |
| 5 | Inline `action` link — when and how many | [props.md:70-73](./props.md), [examples.md:54](./examples.md) | → Pair 5 |
| 6 | Info icon (`infoBox*`) — when to use vs. inline help | [accessibility.md:59-61](./accessibility.md), [Label-figma.md:55](./Label-figma.md) | → Pair 6 (scope: *when* to use; prop-name choice deferred — CONFLICT-002) |
| 7 | Label text — length, case, terminal punctuation | [accessibility.md:82](./accessibility.md) (WCAG 2.4.6) | → Pair 7 |
| 8 | Pairing with Input/form control — placement | [Input-usage.md](../Input/Input-usage.md), [examples.md:31](./examples.md) | → Pair 8 |

### CONFLICT-blocked axes (skipped)

- **Token authority for label text.** MCP `label01` (12px) vs. Figma `typography/body01` (14px) — see [label-audit.md](./label-audit.md) `scores.tokens`. Any "don't override the label type ramp" pair depends on knowing which is authoritative. Deferred until CONFLICT resolves.
- **`information` boolean → `infoBoxText` / `infoBoxButtonLabel` mapping.** Unverified — see [Label-figma.md:211](./Label-figma.md). Pair 6 covers *when* to use the info affordance; prop-level guidance deferred.

### Figma push

No `↳ Label examples` Figma page exists. Once one is created, the 8 pairs above can be ported via `figma-draw` and `figma-extract-usage` can replace this doc. This file is the canonical Do/Don't source of truth until then.

---

_Source: Editorial — derived from [props.md](./props.md), [examples.md](./examples.md), [tokens.md](./tokens.md), [accessibility.md](./accessibility.md), [Label-figma.md](./Label-figma.md), [label-pui.md](./label-pui.md), and [label-audit.md](./label-audit.md). Published Oxygen docs page (`/components/label/usage`) returned 404 on 2026-05-13 via WebFetch. No Figma `↳ Label examples` page exists. Format follows [DataTable-usage.md](../DataTable/DataTable-usage.md) precedent (derivation-only mode)._
