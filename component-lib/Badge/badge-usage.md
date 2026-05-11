---
component: Badge
package: "@8x8/oxygen-badge"
category: data_display
role: usage
role_description: "Do/Don't editorial guidelines from Figma examples page"
pipeline_stage: extracted
pipeline_note: "Usage extracted; audit not yet run"
audit_verdict: null
siblings:
  - "[[Badge/props]]"
  - "[[Badge/examples]]"
  - "[[Badge/tokens]]"
  - "[[Badge/accessibility]]"
  - "[[Badge/badge-pui]]"
tags:
  - oxygen
  - component/Badge
  - role/usage
  - stage/extracted
  - category/data_display
---

<!-- SOURCE: Figma — ↳ Badge examples -->
<!-- PAGE: ↳ Badge examples (node 90220:23) -->
<!-- SECTION: Usage Guidelines (frame 90220:66) -->
<!-- EXTRACTED: 2026-05-08 -->
<!-- COMPONENT: Badge -->
<!-- PAIRS: 2 — Do/Don't card frames (naming convention: "Do -" / "Dont -" without ✅/❌ emoji) -->
<!-- SCREENSHOTS: Captured via Figma REST export — no local PNG stored; reference Figma node links below -->

# Badge — Usage Guidelines

> **See also:** [props.md](./props.md) · [tokens.md](./tokens.md) ·
> [examples.md](./examples.md) · [accessibility.md](./accessibility.md)

Usage guidelines extracted from the `↳ Badge examples` Figma page.
2 Do/Don't pairs covering counter and dot badge types.

---

## Pair 1 — Counter badge

### ✅ Do — Use counter badge on notification icons to show unread count

> Use the counter type when a numeric total is meaningful to the user.

<!-- SCREENSHOT: Figma node 90220:72 — https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/branch/daQccyh6OqlqyXWywIEqR4/UI-components?node-id=90220-72 -->

**Component:** `Badge` · `type: counter`

---

### ❌ Don't — Use counter badge with non-numeric content

> The counter slot is for numeric values only. Avoid placing icons or arbitrary text inside it.

<!-- SCREENSHOT: Figma node 90220:77 — https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/branch/daQccyh6OqlqyXWywIEqR4/UI-components?node-id=90220-77 -->

**Component:** `Badge` · `type: counter`

---

## Pair 2 — Dot badge

### ✅ Do — Use dot badge to signal presence without a count

> A dot badge is sufficient when the user only needs to know something is new or active.

<!-- SCREENSHOT: Figma node 90220:83 — https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/branch/daQccyh6OqlqyXWywIEqR4/UI-components?node-id=90220-83 -->

**Component:** `Badge` · `type: dot`

---

### ❌ Don't — Use multiple badge types on the same element

> Stacking badge types creates visual ambiguity. Use one badge per element.

<!-- SCREENSHOT: Figma node 90220:88 — https://www.figma.com/design/5YihJ5WuDvnvrlrRMC4sBp/branch/daQccyh6OqlqyXWywIEqR4/UI-components?node-id=90220-88 -->

**Component:** `Badge` · `type: counter`

---

## Gaps

| Item | Description |
|------|-------------|
| Screenshot images | Figma REST export returns inline images only — no downloadable URL. Screenshots not stored as local PNGs. Reference Figma node links in each section above. |
| Frame naming | Cards use `Do -` / `Dont -` prefix (without `✅`/`❌` emoji) rather than the standard skill convention. Content is equivalent. |

---

_Source: Figma examples page · Extracted 2026-05-08_
