# SVG Infographic Quality Guide

Use this guide while designing, drawing, and checking a hand-authored SVG infographic.

## Visual System

- Default canvas: `1024 × 768` with a transparent background; change it when the target context requires another ratio.
- Typography: system sans-serif with `PingFang SC` and other suitable CJK fallbacks.
- Main labels: normally `18–22px`; verify the effective size after embedding or scaling.
- Neutral card: fill `#f1efe7`, border `#d5d1c7`, text `#18343a`.
- Warning state: fill `#fff1d9`, border `#f1a23a`, text `#7a3f00`.
- Success state: fill `#ddf7ef`, border `#10a98c`, text `#006b61`.
- Information state: fill `#e6f2ff`, border `#4f8fd6`, text `#1b4d7a`.
- Coordination state: fill `#f0e8ff`, border `#8b6fd6`, text `#4b2e83`.
- Give equal logical levels the same color. A color change must communicate state, category, priority, ownership, or direction.
- Keep most diagrams to one accent color, or two to three when the structure genuinely needs them.

These defaults are a starting system, not a required brand. User-provided brand rules take priority.

## Layout Contract

Before placing text:

- assign every label to a known container;
- give every node fixed dimensions and padding;
- define source and target anchors for every connector;
- reserve space for captions and return paths;
- state the intended reading order.

Prefer containment, alignment, spacing, position, and connectors over decorative icons. Reduce scope when the diagram becomes crowded.

## Text

- Keep labels under about 14 Chinese characters when practical.
- SVG text does not wrap automatically; use explicit `tspan` lines where needed.
- Keep at least `18px` horizontal and `16px` vertical visual padding in ordinary cards.
- Use captions with their own bounds instead of leaving explanatory text floating near a node.
- Preserve exact terms when the argument depends on them.

## Connectors

- Default stroke: `2px`; normal maximum: `2.5px`.
- Default arrowhead: roughly `8 × 8px`; normal maximum: `10 × 10px`.
- Prefer explicit inline arrowhead geometry for portable SVG.
- If using markers, set `markerUnits="userSpaceOnUse"`.
- Draw connectors before node labels so paint order cannot place a line over text.
- Reserve an outside lane for feedback and return paths.
- On short gaps, shrink or omit the arrowhead when direction is already obvious.

## Structure Patterns

- Before/after: matching lanes and card dimensions with one visible difference.
- Pipeline: one dominant direction with short stage labels.
- Lifecycle: ordered stages with transition signals.
- Layered stack: foundation below enabling layers and outcomes.
- Causal chain: cause, mechanism, result, and second-order effect.
- Feedback loop: action, signal, adjustment, and improved action, with a clear return path.
- Hub and spoke: one central concept with inputs, outputs, constraints, or stakeholders.
- Matrix: two named dimensions, sparse examples, and explicit quadrants.
- Decision tree: labelled branches and unmistakable terminal actions.
- System map: actors, resources, boundaries, flows, and feedback.

## Rendered QA

Source review is not visual QA. Render the SVG or its final host context and check:

- the claim and topology match the design card;
- labels remain inside their intended containers;
- no text collides with borders, shapes, captions, or connectors;
- arrows remain subordinate and unambiguous;
- alignment, spacing, contrast, and hierarchy are consistent;
- the intended reading order is visible before every label is read;
- the graphic remains legible at the actual embed size;
- no edge is clipped by the canvas or host container.

Repair the SVG source and render again whenever a visible defect remains. If the environment cannot render or screenshot the result, disclose that limitation instead of claiming visual acceptance.

## Export

- Keep SVG source as the source of truth.
- An HTML wrapper may copy SVG source and rasterize it to PNG in the browser.
- Under `file://`, clipboard access may fail; offer a source or file download fallback.
- PNG is a derivative for convenience, not the editable canonical artifact.
