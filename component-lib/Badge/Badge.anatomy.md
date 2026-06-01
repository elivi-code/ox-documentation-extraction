---
parent: "[[Badge]]"
section: anatomy
---

## Anatomy, variants & states

<!-- STUB:GAP-001 source="Run figma-extract for Badge using the Figma UI-components file (file key 5YihJ5WuDvnvrlrRMC4sBp; Badge node 2565:14) with Desktop Bridge active to produce badge-figma.md and a screenshot PNG." -->
<!-- source: figma-only -->

> **Source gap (blocker):** `badge-figma.md` does not exist — `figma-extract` was never run for Badge. The Figma component-set structure, variant axes, inner layer tree, anatomy labels, and spacing/token bindings are unknown. Run `figma-extract` for Badge (node `2565:14`) to populate this spoke.

### What is known from code/MCP (not Figma-confirmed)

Three Figma `type` values are referenced in [[Badge.props]] but their layer anatomy is unverified:

| Figma type | Description |
|---|---|
| `counter` | Pill with numeric children |
| `dot` | Circular indicator, no children |
| `mention` | `@` indicator |

Code-side size states: `small`, `medium` (default), `big`. Code-side type variants: `primary` (default), `secondary`. The `AIBadge` is a separate exported variant (star icon + text).
