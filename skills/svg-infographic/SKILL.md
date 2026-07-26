---
name: svg-infographic
description: Create copyable, hand-authored SVG infographics from a claim, process, comparison, system, or conceptual explanation. Use when the user wants selectable text, transparent backgrounds, precise layout control, or an SVG that can be embedded in a page or slide. Do not use for photorealistic art, raster-first illustration, generic Mermaid diagrams, or unattended article-wide batch generation.
---

# SVG Infographic

Turn one bounded idea into a real SVG diagram whose text remains selectable and whose layout can be edited precisely.

The canonical deliverable is SVG source, not a raster image that merely looks like a diagram. Use an optional HTML wrapper when the user needs an easy preview, source-copy button, or browser-side PNG export.

## Before You Draw

Confirm only the choices that materially change the result:

- the claim or relationship the reader should understand;
- standalone image or an insert for an existing page or slide;
- required dimensions, language, brand constraints, and deliverables;
- whether the user wants to review the design card before rendering.

If the input is a long article, select one strong claim or ask the user which section to visualize. Do not silently turn the whole article into a batch.

## Workflow

1. Read [the quality guide](references/quality-guide.md).
2. Reduce the request to one sentence: what should the reader understand after seeing the diagram?
3. Write a compact design card:
   - communication goal;
   - audience and placement;
   - first, second, and third visual stops;
   - chosen diagram grammar and why it matches the relationship;
   - main entities and relations;
   - layout and connector plan;
   - color semantics;
   - two likely layout risks.
4. Choose the structure from the real relationship, not from topic keywords:
   - before/after;
   - pipeline;
   - lifecycle;
   - layered stack;
   - causal chain;
   - feedback loop;
   - hub and spoke;
   - matrix;
   - decision tree;
   - system map.
5. Draft short labels before drawing. Put only essential terms inside nodes and move explanations into bounded captions.
6. Hand-author the SVG. Use explicit node bounds, padding, connector anchors, paint order, and restrained semantic colors.
7. When useful, create a small HTML wrapper that displays the SVG and offers source copy or PNG download in the browser.
8. Render the actual deliverable and inspect it visually. For an embedded diagram, inspect the page or slide context rather than only the raw SVG.
9. Repair and re-render until all hard gates pass.

When the structure is genuinely ambiguous, compare two or three layout candidates while changing one structural variable at a time. Do not create cosmetic variants merely to appear thorough.

## Hard Quality Gates

Do not deliver while any of these remain:

- text is clipped, overflowing, drifting, or touching a border;
- a connector crosses text or has an ambiguous source or destination;
- arrowheads dominate nearby labels or cards;
- color is decorative rather than semantic;
- reading order is unclear;
- the diagram contradicts the design card;
- the embedded result becomes illegible after scaling;
- the visual has not been rendered and inspected, unless rendering is unavailable and that limitation is disclosed.

## Output Contract

Provide:

- the editable `.svg` source;
- a short statement of the diagram’s intended reading order;
- an `.html` preview when requested or useful;
- a `.png` only as an optional derivative, never as a replacement when the user asked for copyable SVG.

For a page or slide that already owns the title and explanatory copy, omit slide-level titles and paragraphs from the SVG. Keep only labels required to understand the diagram.

## Boundaries

- Do not call remote image-generation services by default.
- Do not claim Chinese text is exact unless the rendered output was checked.
- Do not show realistic credentials or secret-looking strings in examples; use abstract placeholders.
- Ask before publishing the generated artifact into a live website, document, slide deck, or social account.
- Treat article-wide or multi-image production as a separate workflow with its own scope and acceptance criteria.
