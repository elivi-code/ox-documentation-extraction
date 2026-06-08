---
parent: "[[Checkbox]]"
section: usage
---

## Usage

Checkboxes let a user **select one or more options** from a list. Each checkbox is independent —
selecting one does not unselect another — unless it is nested under a parent checkbox, in which case
the parent reflects the aggregate state of its children.

### When to use

- Single or multiple checkboxes in forms, for selection from a list of options on a page, modal, or panel.
- A single checkbox for terms-and-conditions — to indicate agreement / disagreement.

### When not to use *(editorial — not on the docs page)*

| Situation | Why | Use instead |
|-----------|-----|-------------|
| The user can pick **only one** option | Checkbox affords independent multi-select; mutual exclusivity needs different ARIA semantics. | [[Radio]] |
| The control toggles a setting that takes effect **immediately** | Checkboxes are committed by form submit; instant-effect toggles read as switches. | [[ToggleButton]] |
| There are **many** options and vertical space is constrained | A long list overflows and slows scanning. | Multi-select `Select` / dropdown with checkbox rows |
| You need a **purely visual** (read-only) indicator | A checkbox advertises interactivity; AT announces it as a control. | Plain text, `Tag`, or an icon |

## Do / Don't

<!-- source: figma-only -->
<!-- STUB:GAP-001 source="If a Figma ↳ Checkbox examples page is ever created with Do/Don't card frames, run figma-extract-usage to replace the editorial draft." -->
> **Editorial pairs (GAP-001).** No Figma `↳ Checkbox examples` page with ✅ Do / ❌ Don't card
> frames exists. The seven pairs below are derived from the published Oxygen docs page (Variants,
> Nesting, Best Practices) cross-validated against the extracted API, token, and accessibility data.
> Replace with `figma-extract-usage` output if such a page is created.

### Pair 1 — Reach for Checkbox when the user can select more than one

**✅ Do** — Use Checkbox for independent, multi-select options; picking A does not preclude picking B.

```tsx
<CheckboxGroup>
  <Checkbox id="email" name="channels" label="Email" value="email" isChecked={email} onChange={(e) => setEmail(e.target.checked)} />
  <Checkbox id="sms"   name="channels" label="SMS"   value="sms"   isChecked={sms}   onChange={(e) => setSms(e.target.checked)} />
  <Checkbox id="push"  name="channels" label="Push"  value="push"  isChecked={push}  onChange={(e) => setPush(e.target.checked)} />
</CheckboxGroup>
```

**❌ Don't** — Use Checkbox when only one selection is allowed. If picking A must clear B, a checkbox lies about the affordance — keyboard and SR users hear "checkbox, not checked" instead of "radio button, not selected". Use [[Radio]].

### Pair 2 — Single Checkbox for binary commitments, not instant-effect toggles

**✅ Do** — Use a single Checkbox for terms-and-conditions or other form-committed binary choices, where the value is committed by a submit / Save.

```tsx
<Checkbox id="terms" name="terms" label="I agree to the terms and conditions"
  value="terms" isChecked={agreed} onChange={(e) => setAgreed(e.target.checked)} />
<Button type="submit" isDisabled={!agreed}>Sign up</Button>
```

**❌ Don't** — Use a Checkbox for a setting that takes effect immediately. Reserve [[ToggleButton]] for instant-effect settings.

### Pair 3 — Pair `isIndeterminate` with a real "select all" parent

**✅ Do** — Use `isIndeterminate` only on a parent that has at least one selected child. The dash glyph means "some — but not all — children are selected".

```tsx
<Checkbox id="select-all" name="selectAll" label="Select all items" value="all"
  isChecked={allSelected} isIndeterminate={someSelected && !allSelected} onChange={handleSelectAll} />
```

**❌ Don't** — Set `isIndeterminate` to convey "loading", "partial validation", or "unknown". Screen readers announce `aria-checked="mixed"` — anything other than a real parent/child group confuses AT users.

### Pair 4 — Always ship a Checkbox with an accessible name

**✅ Do** — Pass a `label` (or a visually-equivalent labelled node); it is wired to `<label htmlFor={id}>` and is **the** accessible name. Keep it concise and action-oriented.

**❌ Don't** — Ship a Checkbox with no `label` and rely on adjacent body copy. SR users hear "checkbox, not checked" with no context.

### Pair 5 — Group related options in a `CheckboxGroup`

**✅ Do** — Wrap related Checkboxes in a `CheckboxGroup` with a group label so SR users hear the group context before each option.

**❌ Don't** — Free-float related Checkboxes without a group container. AT users get no signal the items belong together, and the `$spacing03` rhythm breaks down.

### Pair 6 — Don't disable a Checkbox to hide a validation error

**✅ Do** — Keep the Checkbox enabled and surface the error inline (`role="alert"` + `aria-describedby` on the submit button). See [[Checkbox.accessibility]].

**❌ Don't** — Disable the submit until every box is ticked with no explanation; SR users hear nothing about the unmet requirement.

### Pair 7 — Use `infoBoxText` for explanatory tooltips; keep the label tight

**✅ Do** — Put short, action-shaped text in `label`; put the "why / how does this affect me?" context in `infoBoxText` (a separate focus stop named by `infoBoxButtonLabel`).

**❌ Don't** — Pack the explanation into the `label`. Long labels wrap, defeat scanning, and overflow the `showLabelTooltipOnOverflow` tooltip (meant for graceful truncation, not essay-length help).
