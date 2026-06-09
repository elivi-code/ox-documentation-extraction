---
parent: "[[Select]]"
section: usage
component: Select
pipeline_stage: doc_rewrite
audit_verdict: NO
tags:
  - oxygen
  - component/Select
  - role/usage
  - stage/doc_rewrite
---

<!-- STUB:GAP-014 source="Request designer to create a '↳ Select examples' Figma page following the figma-draw template convention with ✅ Do and ❌ Don't card frames. Once frames exist, run figma-extract-usage to replace editorial pairs with Figma-grounded output. Current pairs derived editorially from published Oxygen docs page (oxygen.8x8.com/components/dropdown/usage, fetched 2026-05-14) + extracted MCP artifacts." -->

> **Editorial guidance.** No `↳ Select examples` Figma page exists — pairs below are derived from the published Oxygen docs page and extracted artifacts. Two open CONFLICTs (GAP-002 `isAsync` type; GAP-003 `ref` vs `forwardedRef`) are deliberately avoided in all code examples.

---

## Pair 1 — Reach for Select when the option list exceeds five items

### ✅ Do — Use Select for >5 options or a searchable list

```tsx
<Select
  labelValue="Country"
  options={countries} // 200 entries
  placeholder="Select a country"
/>
```

### ❌ Don't — Use Select for a 2–3 option choice

```tsx
{/* Wrong — three options that should be Radios */}
<Select
  labelValue="Billing cadence"
  options={[
    { value: 'monthly', label: 'Monthly' },
    { value: 'annual',  label: 'Annual' },
    { value: 'custom',  label: 'Custom' },
  ]}
/>
```

**Source:** Published docs — Best Practices (verbatim)

---

## Pair 2 — Use `isMulti` (with `hasCheckbox` when helpful) for genuine multi-select

### ✅ Do — Single multi-select when one decision yields several values

```tsx
<Select
  labelValue="Tags"
  isMulti
  hasCheckbox
  multipleSelectMaxRows={2}
  options={tagOptions}
  value={tags}
  onChange={(next) => setTags(next)}
/>
```

### ❌ Don't — Stack single Selects to fake multi-select

```tsx
{/* Wrong — three single Selects for one logical field */}
<Select labelValue="Tag 1" options={tagOptions} />
<Select labelValue="Tag 2" options={tagOptions} />
<Select labelValue="Tag 3" options={tagOptions} />
```

---

## Pair 3 — Use `isAsync` + `loadOptions` for remote or large data

### ✅ Do — Stream options from the server

```tsx
const loadUsers = (inputValue, callback) => {
  fetch(`/api/users?q=${encodeURIComponent(inputValue)}`)
    .then((r) => r.json())
    .then((rows) => callback(rows.map((u) => ({ value: u.id, label: u.name }))));
};

<Select
  labelValue="Assignee"
  isAsync
  loadOptions={loadUsers}
  loadingMessage="Loading users…"
  placeholder="Search by name"
/>
```

### ❌ Don't — Pre-load 10 000 rows into `options`

```tsx
{/* Wrong — huge static list; use isAsync or VirtualMenuList instead */}
<Select options={options10k} />
```

> `isAsync` is type-conflicted in source (`boolean` vs `IsAsync` — GAP-002). The example passes the boolean shorthand only; do not annotate the prop type until the conflict is resolved.

---

## Pair 4 — Always pair Select-in-Modal with `menuPortalTarget` + `menuPlacement="auto"`

### ✅ Do — Portal the menu out of the modal stacking context

```tsx
const [portalTarget, setPortalTarget] = useState<HTMLElement | null>(null);

<Modal portalRef={(el) => setPortalTarget(el)}>
  <ModalContent>
    <Select
      labelValue="Option"
      options={options}
      menuPortalTarget={portalTarget}
      menuPlacement="auto"
    />
  </ModalContent>
</Modal>
```

### ❌ Don't — Drop a vanilla Select into a Modal

```tsx
{/* Wrong — menu clips inside ModalContent's overflow */}
<Modal>
  <ModalContent>
    <Select labelValue="Option" options={options} />
  </ModalContent>
</Modal>
```

> Modal `portalRef` shape should be validated against current `@8x8/oxygen-modal` release (WARN-001).

---

## Pair 5 — Give every Select a meaningful `labelValue`

### ✅ Do — Visible label via `labelValue`; reserve info button for extra detail

```tsx
<Select
  labelValue="Compliance region"
  infoBoxText="Region determines which data-residency policy applies to the workspace."
  infoBoxButtonLabel="More info about compliance region"
  options={regionOptions}
/>
```

### ❌ Don't — Rely on `placeholder` to label the field

```tsx
{/* Wrong — placeholder disappears once a value is chosen */}
<Select
  placeholder="Compliance region"
  options={regionOptions}
/>
```

---

## Pair 6 — Pair `hasError` with a visible message

### ✅ Do — Render `hasError={true}` and a sibling error element

```tsx
const errorId = 'region-error';

<>
  <Select
    labelValue="Compliance region"
    options={regionOptions}
    hasError={!region}
    inputProps={{ 'aria-describedby': errorId }}
  />
  {!region && (
    <p id={errorId} role="alert" className="error-text">
      Pick a region before continuing.
    </p>
  )}
</>
```

### ❌ Don't — Set `hasError` without a message

```tsx
{/* Wrong — colour-only error; screen-reader users get no description */}
<Select labelValue="Compliance region" options={regionOptions} hasError />
```

---

## Pair 7 — Set `isClearable={false}` on required fields

### ✅ Do — Prevent clearing a required field

```tsx
<Select
  labelValue="Plan"
  isRequired
  isClearable={false}
  options={planOptions}
  value={plan}
  onChange={setPlan}
/>
```

### ❌ Don't — Leave `isClearable` at default on a required Select

```tsx
{/* Wrong — default true clear button silently invalidates a required value */}
<Select
  labelValue="Plan"
  isRequired
  options={planOptions}
  value={plan}
  onChange={setPlan}
/>
```

---

## Pair 8 — Keep `placeholder` short and distinct from the label

### ✅ Do — Short verb-phrase hint

```tsx
<Select
  labelValue="Region"
  placeholder="Select a region"
  options={regionOptions}
/>
```

### ❌ Don't — Stuff explanation into `placeholder`

```tsx
{/* Wrong — long placeholder overflows, vanishes on select */}
<Select
  labelValue="Region"
  placeholder="Region — the data-residency region for this workspace, which determines compliance, latency, and billing tier"
  options={regionOptions}
/>
```

---

## When to use

- More than five options
- Searchable, filterable, or async-loaded lists
- Multi-select chip display (`isMulti`)

## When not to use

| Situation | Use instead |
|-----------|-------------|
| Fewer than 5 options, single-select | `Radio` / `RadioGroup` |
| Fewer than 5 options, multi-select | `Checkbox` / `CheckboxGroup` |
| Binary instant-effect toggle | `ToggleButton` |
| Free-form input with autocomplete | Autocomplete pattern (or `isCreatable` if closed list is the source of truth) |

## Related

- [[Radio]] — single selection ≤5 options
- [[Checkbox]] — multiple selection ≤5 options
- [[Modal]] — use `menuPortalTarget` when Select is inside a Modal
