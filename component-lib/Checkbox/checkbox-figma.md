<!-- FIGMA FILE: 5YihJ5WuDvnvrlrRMC4sBp (UI-components) -->
<!-- NODE: 51776:5078 (canvas root for Checkbox) -->
<!-- EXTRACTED: 2026-04-29 -->
<!-- COLOR STRATEGY: B — >3 state/variant combos; states as columns -->

# Checkbox — Figma Design Spec

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [tokens.md](tokens.md) · [accessibility.md](accessibility.md)

## Screenshot

![Checkbox component variants — Light and Dark mode, all states]
<!-- Screenshot captured from Figma node 51776:5078 showing:
  Left: info card (Beta badge, Documentation + Storybook links)
  Center-left: Checkbox Input variants (20×20 input only, Light + Dark columns)
  Center: Full Checkbox variants (input + label, Light + Dark columns)
  Right: Checkbox Group variants (Light + Dark, with error states) -->

---

## 1. Anatomy

Three component sets are defined at this Figma location:

### 1a. Checkbox Input (`51776:5081`)
The bare checkbox input square — no label. Used as a sub-component inside Checkbox and CheckboxGroup.

| Layer | Type | Role | Notes |
|-------|------|------|-------|
| Checkbox Input | COMPONENT_SET | Container | 72×424 px bounding box (all 24 variants) |
| Each variant | COMPONENT | Input state | 20×20 px |

### 1b. Checkbox (full component) (`51776:5160`)
Checkbox Input + label text, composed horizontally.

| Layer | Type | Role | Notes |
|-------|------|------|-------|
| Checkbox | COMPONENT_SET | Container | 286×424 px (all 24 variants) |
| Each variant | COMPONENT | Full checkbox row | 128×20 px (Light column), 128×20 px (Dark column) |

### 1c. Checkbox Group (`52682:566`)
Container for multiple Checkbox items with optional header, footer, and error state.

| Layer | Type | Role | Notes |
|-------|------|------|-------|
| Checkbox Group | COMPONENT_SET | Container | 672×377 px (all 4 variants) |
| Each variant | COMPONENT | Group | 320×168 px |
| `header` | BOOLEAN | Optional slot | Default: true |
| `footer` | BOOLEAN | Optional slot | Default: true |

---

## 2. Properties and API

### Checkbox Input variant axes

| Property | Type | Default | Values |
|----------|------|---------|--------|
| Mode | VARIANT | Light | Light, Dark |
| State | VARIANT | Rest | Rest, Hover |
| isChecked? | VARIANT | False | True, False |
| isIndeterminate? | VARIANT | False | False, True |
| isDisabled? | VARIANT | False | False, True |
| isFocused? | VARIANT | False | True, False |

**Total variants: 24** (not all axis combinations are present — Hover and isFocused are only
defined for enabled states; disabled variants don't have Hover/Focus).

### Checkbox (full) variant axes

Identical axes to Checkbox Input:

| Property | Type | Default | Values |
|----------|------|---------|--------|
| Mode | VARIANT | Light | Light, Dark |
| State | VARIANT | Rest | Rest, Hover |
| isChecked | VARIANT | False | False, True |
| isIndeterminate | VARIANT | False | False, True |
| isDisabled | VARIANT | False | False, True |
| isFocused | VARIANT | False | False, True |

**Total variants: 24**

### Checkbox Group variant axes

| Property | Type | Default | Values |
|----------|------|---------|--------|
| header | BOOLEAN | true | true, false |
| footer | BOOLEAN | true | true, false |
| Mode | VARIANT | Light | Light, Dark |
| isError | VARIANT | False | False, True |

**Total variants: 4** (Mode × isError)

### State classification

| State | Type | Maps to API prop |
|-------|------|-----------------|
| isChecked | Persistent | `isChecked` prop |
| isIndeterminate | Persistent | `isIndeterminate` prop |
| isDisabled | Persistent | `isDisabled` prop |
| isFocused | Transient | No API prop — CSS only |
| State=Hover | Transient | No API prop — CSS only |

---

## 3. Color and token bindings

<!-- NOT FOUND IN FIGMA RESPONSE -->

Variables API returned an error (insufficient permissions). Figma styles returned 0 results.
No token bindings could be extracted.

**What is known:**
- The component set boundaries are stroked with `rgba(0.592, 0.278, 1, 1)` — this is a Figma
  organizational annotation colour, not a design token.
- The design system colour palette available in Oxygen MCP contains `blue05 #0056E0` as the
  likely primary interactive colour for the checked state (unconfirmed without token data).

**To retrieve token bindings:**
1. Run Figma Desktop Bridge plugin in the UI-components file
2. Re-run `figma_get_variables(namePattern="checkbox", resolveAliases=true)`

---

## 4. Structure and spacing

### Checkbox Input dimensions

| Element | Width | Height |
|---------|-------|--------|
| Input control (each variant) | 20 px | 20 px |
| Component set bounds | 72 px | 424 px |

### Checkbox (full) dimensions

| Element | Width | Height |
|---------|-------|--------|
| Full row (each variant) | 128 px | 20 px |
| Component set bounds | 286 px | 424 px |
| Light/Dark column gap | ~15 px | — |

> Gap between input and label: visible in layout but exact px value not returned without
> design context access. Oxygen docs state label is "always positioned to the right" with
> vertical stacking.

### Checkbox Group dimensions

| Element | Width | Height |
|---------|-------|--------|
| Each variant | 320 px | 168 px |
| Component set bounds | 672 px | 377 px |

> Padding between group label and first item: `$spacing04` (from Oxygen usage docs)
> Padding between items: `$spacing03` (from Oxygen usage docs)

---

## 5. Visual record and accessibility annotations

### Screenshot (captured 2026-04-29)

Figma node `51776:5078` screenshot confirmed the following visual structure (left to right):

1. **Info card** — Beta badge, Documentation and Storybook links, contact line
2. **Checkbox Input variants** — Two columns (Light | Dark), rows showing:
   - Unchecked rest
   - Unchecked focused
   - Unchecked disabled
   - Checked rest
   - Checked focused
   - Checked disabled
   - Indeterminate rest
   - Indeterminate focused
   - Indeterminate disabled
   - Hover states (unchecked, checked, indeterminate)
3. **Checkbox (full) variants** — Same state matrix with "Example Label" text, Light + Dark
4. **Checkbox Group variants** — Label slot ("Example Label*"), info icon, Slot placeholder,
   hint text, error message row; Light and Dark side-by-side; with and without error state

### Figma annotations

<!-- NOT FOUND IN FIGMA RESPONSE -->
No design annotations were embedded in the metadata or component descriptions (known Figma API
limitation — description field absent without Desktop Bridge).

### Accessibility notes from Figma

<!-- NOT FOUND IN FIGMA RESPONSE -->

---

## Gaps & conflicts

| Gap | Severity | Recommended action |
|-----|----------|--------------------|
| No Figma design context (spacing/padding exact values) | Medium | Connect Figma Desktop Bridge and re-run `get_design_context` |
| No variable/token bindings | High | Enable Desktop Bridge; check Figma Enterprise plan for Variables API |
| No component descriptions (Figma API bug) | Low | Run Desktop Bridge plugin to surface descriptions |
| Token coverage % unknown | Medium | Re-run extraction with Desktop Bridge for enrichment data |
| Figma styles returned 0 results | Low | Styles may live in a library file, not this document |
| Hover/Focus variants not present for isDisabled=True | Note | Intentional — disabled elements are not interactive |

_Source: Figma claude.ai MCP + figma-console MCP · fileKey: 5YihJ5WuDvnvrlrRMC4sBp · nodeId: 51776:5078 · Extracted 2026-04-29_
