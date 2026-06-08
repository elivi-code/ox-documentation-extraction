---
parent: "[[TextArea]]"
section: usage
pipeline_stage: draft
audit_verdict: partial
tags:
  - oxygen
  - component/TextArea
  - section/usage
---

<!-- STUB:GAP-001 source="Run figma-extract-usage skill for TextArea once a designer populates the Figma '↳ TextArea examples' page with annotated component instances — the content below is a provisional editorial draft (textarea-usage-draft.md) authored by usage-advisor, not sourced from Figma" -->

> **Draft content** — the canonical `textarea-usage.md` requires a populated Figma `↳ TextArea examples` page. The pairs below are grounded in `props.md`, `examples.md`, `accessibility.md`, and `textarea-figma.md`, with internal precedent from `TextField-usage.md`. Treat as candidate framings pending designer review.

---

## When to use

- The user must enter **multi-line free-form content** — paragraphs, comments, notes, descriptions, messages, code snippets.
- The value is unpredictable in length and structure and benefits from line breaks, soft-wrapping, and visible whitespace.
- The field is part of a form pattern that already mixes `TextField`, `Select`, `Checkbox`, etc., and one input requires more vertical space than a single line.

## When not to use

| Situation | Use instead |
|-----------|-------------|
| Single-line input — name, email, code, search | [[TextField]] — fixed-height, single-line, ships with built-in prefix/suffix/icon affordances |
| One option from a known list | [[Dropdown]], [[Radio]], or [[Checkbox]] |
| Rich-text / formatted content (bold, links, mentions) | A dedicated rich-text editor — Oxygen does not ship one |

---

## Do / Don't

### Pair 1 — Use Textarea for multi-line free-form input; reach for TextField when one line is enough

#### ✅ Do — Use Textarea when the user is writing more than a line

```tsx
<label htmlFor="feedback">What could we improve?</label>
<Textarea
  id="feedback"
  rows={4}
  placeholder="Tell us what didn't work…"
  onChange={(e) => setFeedback(e.target.value)}
/>
```

#### ❌ Don't — Use Textarea for a value that fits on one line

```tsx
// ❌ One-line value inside a 3-row Textarea
<Textarea id="email" placeholder="you@company.com" />

// ✅ Use TextField for single-line values
// <TextField label="Email" placeholder="you@company.com" />
```

---

### Pair 2 — Always pair Textarea with a real `<label>`; never use `placeholder` as a label

#### ✅ Do — Provide a programmatic label every time

```tsx
<label htmlFor="bio">Bio</label>
<Textarea
  id="bio"
  placeholder="A short intro you'd put on a conference badge…"
  rows={3}
  onChange={(e) => setBio(e.target.value)}
/>
```

#### ❌ Don't — Rely on placeholder text as the field's label

```tsx
// ❌ Placeholder-as-label — fails WCAG 1.3.1 and 3.3.2
<Textarea placeholder="Bio" />

// ✅ Real label + placeholder as example
<label htmlFor="bio">Bio</label>
<Textarea id="bio" placeholder="A short intro…" />
```

---

### Pair 3 — Put hints and constraints in a description below the field, not in placeholder

#### ✅ Do — Render hint text as a sibling node and link it via `aria-describedby`

```tsx
<label htmlFor="repro">Steps to reproduce</label>
<Textarea
  id="repro"
  aria-describedby="repro-hint"
  rows={5}
  maxLength={2000}
/>
<span id="repro-hint">List the exact steps so we can recreate the issue.</span>
```

#### ❌ Don't — Pack constraints into the placeholder

```tsx
// ❌ Rule vanishes on first keystroke
<Textarea placeholder="Max 2000 characters. Markdown supported." />
```

---

### Pair 4 — Use `isReadOnly` to display a value the user can read and copy; use `isDisabled` only when the field is genuinely unavailable

#### ✅ Do — Reach for `isReadOnly` when the user needs to see and copy the value but not change it

```tsx
<label htmlFor="report">Generated summary</label>
<Textarea id="report" value={summary} isReadOnly rows={6} />
```

#### ❌ Don't — Disable a Textarea just to display a value

```tsx
// ❌ Screen reader cannot reach it; no text can be copied
<Textarea value={summary} isDisabled />

// ✅ Read-only keeps the field in the tab order
<Textarea value={summary} isReadOnly />
```

---

### Pair 5 — Show errors with `hasError` + an accessible error message; never colour alone

#### ✅ Do — Combine `hasError` with a descriptive error message linked via `aria-describedby`

```tsx
<label htmlFor="message">Message</label>
<Textarea
  id="message"
  aria-describedby={hasError ? 'message-error' : undefined}
  aria-invalid={hasError ? 'true' : undefined}
  hasError={hasError}
  rows={4}
  value={value}
  onChange={(e) => setValue(e.target.value)}
/>
{hasError && (
  <span id="message-error" role="alert">
    Message must be at least 20 characters.
  </span>
)}
```

#### ❌ Don't — Set `hasError` without rendering an accessible message

```tsx
// ❌ Red border with no text — fails WCAG 1.4.1 and 3.3.1
<Textarea id="message" hasError />
```

---

### Pair 6 — Size `rows` to the expected input length

#### ✅ Do — Pick `rows` based on how much text you actually expect

```tsx
{/* Short note */}
<label htmlFor="alias">Display name override</label>
<Textarea id="alias" rows={2} maxLength={80} />

{/* Long-form feedback */}
<label htmlFor="incident">Describe what happened</label>
<Textarea id="incident" rows={8} maxLength={5000} />
```

#### ❌ Don't — Leave every Textarea at `rows={3}` regardless of expected input

```tsx
// ❌ Same height for inputs expecting very different amounts of text
<Textarea id="title" rows={3} />
<Textarea id="description" rows={3} />
<Textarea id="reproSteps" rows={3} />
```

---

### Pair 7 — Lock `resize` to `vertical` or `none` inside structured forms; avoid `horizontal` and `both`

#### ✅ Do — Keep the default `resize="vertical"`, or set `resize="none"` in tight layouts

```tsx
{/* Default — vertical resize allowed */}
<Textarea id="bio" rows={4} maxLength={500} />

{/* Locked in a tight grid cell */}
<Textarea id="note" rows={3} resize="none" maxLength={280} />
```

#### ❌ Don't — Allow horizontal or both-axis resize inside fixed-width form columns

```tsx
// ❌ Lets the user break the grid
<Textarea id="bio" resize="horizontal" />
<Textarea id="bio" resize="both" />
```

---

### Pair 8 — Show a live character counter when `maxLength` represents a hard limit users care about

#### ✅ Do — Surface a visible counter when the limit is a real constraint

```tsx
const MAX = 280;
const [bio, setBio] = useState('');

<label htmlFor="bio">Bio</label>
<Textarea
  id="bio"
  aria-describedby="bio-hint bio-count"
  maxLength={MAX}
  value={bio}
  onChange={(e) => setBio(e.target.value)}
/>
<span id="bio-hint">A short intro for your profile.</span>
<span id="bio-count" aria-live="polite">{bio.length} / {MAX}</span>
```

#### ❌ Don't — Set a long `maxLength` and rely on the browser's silent cut-off

```tsx
// ❌ Silent cap — user has no idea they're near the limit
<Textarea id="bio" maxLength={280} />
```

---

_Source: editorial draft (textarea-usage-draft.md) authored 2026-05-15 · Pending canonical figma-extract-usage output_
