---
name: cad-render-fidelity-review
description: Audit architectural renderings against CAD drawings for strict drawing fidelity. Use when the user asks whether an effect image/rendering matches DWG/PDF construction drawings, wants renderings revised until they meet drawing requirements, or needs a discrepancy list for facade, roof, windows, balconies, materials, proportions, and style consistency.
---

# CAD Render Fidelity Review

Use this skill to judge whether an architectural rendering is truly based on the drawing, not merely visually similar. The effective operation is to compare architectural facts first, then style and material choices.

## Review Workflow

1. Gather evidence.
   - Inspect the DWG/PDF drawing views, especially plans, elevations, roof plan, sections, and facade notes.
   - Inspect every rendering image under review.
   - If the drawing is DWG, export or render the relevant layouts before comparing.

2. Lock drawing facts.
   - Floor count.
   - Roof type, ridge/eave form, slope direction, overhangs.
   - Front/side facade rhythm.
   - Door and window count, position, scale, and alignment.
   - Balcony/terrace/railing presence and location.
   - Wall material zones, base/plinth, trim lines, roof color, facade colors.
   - Side facade simplification or special openings.

3. Compare from high-risk to low-risk.
   - Massing and floor count.
   - Roof geometry.
   - Door/window/balcony layout.
   - Facade style and linework.
   - Material zoning and color logic.
   - Landscape/background only after the building itself passes.

4. Decide the grade.
   - `strictly matches`: major geometry and facade facts match; only presentation improved.
   - `usable concept`: massing resembles the drawing but important openings/materials differ.
   - `not compliant`: doors/windows/balconies/roof/style are materially changed.

## Discrepancy Report Pattern

Lead with the verdict, then list concrete mismatches:

- front facade openings
- side facade openings
- balconies added/removed
- roof form or proportions changed
- style changed from drawing language
- material zoning changed
- drawing-specific details omitted

Do not soften major geometry errors as "style differences." If the rendering invents windows or balconies, call it noncompliant.

## Revision Guidance

When the user asks to fix the rendering:

- Return to a geometry-lock step before generating another polished rendering.
- Make a deterministic base elevation or annotated geometry brief from the drawing.
- Hard-lock window count/position, balcony positions, roof outline, floor lines, and material zones.
- Only then add rendering improvements: texture, light, glass, paving, low planting, and background.
- Keep the previous accepted style only if it does not conflict with drawing facts.

## Final Response Shape

Return:

- Verdict.
- Numbered discrepancy list ordered by severity.
- Whether the image can be used as a concept image or must be redone.
- Locked items for the next revision.
- Any uncertainty caused by unreadable drawings or missing views.
