---
parent: "[[Spinner]]"
section: composition
component: Spinner
pipeline_stage: draft
siblings:
  - "[[Spinner]]"
  - "[[Spinner.props]]"
  - "[[Spinner.anatomy]]"
  - "[[Spinner.tokens]]"
  - "[[Spinner.usage]]"
  - "[[Spinner.accessibility]]"
  - "[[Spinner.platform]]"
tags:
  - oxygen
  - component/Spinner
  - role/composition
---

## Subcomponents

Spinner has no structural subcomponents — it renders as a self-contained arc with optional supporting text. The "Spinner complete" terminal-state variants (complete, error) live in a **separate Figma component set** and are swapped in by consuming code when loading ends, rather than being a subcomponent of Spinner itself.

## Related components

| Component | Relationship |
|-----------|-------------|
| [[ProgressBar]] | Alternate loading indicator for **determinate** progress (known percentage). Use ProgressBar when you can measure progress; Spinner for indeterminate waits. |
| [[Skeleton]] | Content-shaped placeholder for known layouts. Prefer Skeleton over Spinner when the structure of incoming content is known — reduces perceived wait and prevents layout shift. |

## Composition patterns

Spinner ships no container surface. Consuming layouts compose it inside the area being loaded:

```tsx
{/* Inside a card */}
{isLoading ? <Spinner size="small" text="Loading" /> : <CardContent />}

{/* Page-level */}
{isBootstrapping ? <Spinner size="default" text="Loading workspace" /> : <App />}
```

## Component swap pattern (Spinner → Spinner complete)

Per the Figma design decisions, terminal states live in a separate component set ("Spinner complete"). In code this means replacing the `Spinner` element rather than updating a variant prop:

```tsx
{loadState === 'loading' && <Spinner size="default" text="Loading" />}
{loadState === 'complete' && <SpinnerComplete state="complete" />}
{loadState === 'error' && <SpinnerComplete state="error" />}
```

This mirrors the Figma design intent: "Spinner complete as separate component set signals that the consuming code should swap the component rather than changing a variant prop when loading ends."

_Source: Figma MCP · usage docs · Extracted 2026-05-05_
