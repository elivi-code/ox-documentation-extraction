---
parent: "[[Accordion]]"
section: usage
---

<!-- STUB:GAP-001 source="Designer must add Do/Don't frames to the '↳ Accordion examples' Figma page (79430:614) following the figma-draw template convention, then re-run figma-extract-usage to replace derived pairs below with Figma-sourced ones." -->
> **Partial source:** Do/Don't pairs below are derived from the [oxygen.8x8.com/components/accordion/usage](https://oxygen.8x8.com/components/accordion/usage) Best Practices section (2026-05-11), not extracted from Figma. Replace when designer adds frames to examples page.

## When to use

- When you want to reduce clutter and display information one section at a time.
- When the content is long and window real estate is limited.

## When not to use

- When the page permits all content to be visible without conflicting with the user's workflow.
- When information must be structured in a deep hierarchy with multiple sublevels — use [[Tabs]] instead.

---

## Best practices

- The title must reflect the content inside the collapsed accordion.
- Avoid putting important information inside collapsed accordions.
- Offer "Expand all" / "Collapse all" for variable-height groups. Not applicable when accordions have fixed height.

---

## Do / Don't

### Title accuracy

| | Guidance |
|---|---|
| ✅ Do | Make the title reflect the content inside. A scannable title lets users decide whether to expand. |
| ❌ Don't | Use vague titles ("More info", "Details") that don't preview the content. Users must expand every accordion to find what they need. |

### Content importance

| | Guidance |
|---|---|
| ✅ Do | Use accordions for secondary or supplementary information users may skip without consequence. |
| ❌ Don't | Hide critical, time-sensitive, or required-to-act information inside collapsed accordions. |

### Group controls

| | Guidance |
|---|---|
| ✅ Do | Offer "Expand all" / "Collapse all" controls for variable-height groups so users can scan everything at once. |
| ❌ Don't | Add "Expand all" / "Collapse all" to fixed-height groups — only one accordion can be open at a time, so the controls have no effect. |

---

## Related patterns

**Patterns:** [[Form]]
