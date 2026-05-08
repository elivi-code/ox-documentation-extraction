# DateTimeSelector — Tokens

> **See also:** [props.md](props.md) · [examples.md](examples.md) · [accessibility.md](accessibility.md)

<!-- NOTE: Oxygen MCP returned no theme tokens for @8x8/oxygen-date-time-selector.
     Token values are sourced from Figma design context (DateTimeSelector-figma.md) once extracted.
     See GAP note below. -->

## Theme tokens

No tokens returned by `mcp__oxygen-mcp__get-theme-tokens` for this package.

Token names for DateTimeSelector are expected to follow the UI-Foundations semantic token convention
(`--ui/*`, `--text/*`, `--interactive/*`, `--actions/*`) — refer to [DateTimeSelector-figma.md](DateTimeSelector-figma.md)
for token bindings extracted from the Figma design context.

---

## Known states

Based on the Figma component set (Mode × Size × State × Error × Filled), the following visual states exist:

| State | Expected token role |
|-------|---------------------|
| Rest | Default surface + border |
| Hover | Hover surface |
| Focus | Focus ring (`--interactive/focus01`) |
| Disabled | Disabled text/surface |
| Error (True) | Error border/icon |
| Error (False) | Standard border |
| Filled (True) | Filled input surface |
| Filled (False) | Empty input surface |

---

_Source: Oxygen MCP · Extracted 2026-05-08_
