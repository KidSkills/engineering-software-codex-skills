---
name: solidworks-validated-delivery
description: Build or deliver SolidWorks-style mechanical CAD models with independent geometry validation before claiming completion. Use when a user asks to create, repair, inspect, or convert SolidWorks parts/assemblies from images, sketches, dimensions, STL/STEP/DWG/PDF references, especially when prior automation may produce unreliable .SLDPRT/.SLDASM output and the task requires a real deliverable rather than only a modeling plan.
---

# SolidWorks Validated Delivery

Use this skill when the important lesson is "do not confuse a CAD automation attempt with a verified model." Build the model if possible, but always verify the geometry through an independent artifact or check before presenting it as complete.

## Core Workflow

1. Lock the modeling intent.
   - Identify the part function, axes, symmetry, datum surfaces, through holes, mounting holes, counterbores, bosses, ribs, fillets, and manufacturing process.
   - Convert unclear image input into a compact feature list with assumed dimensions marked explicitly.
   - Decide whether the model is best built by revolve, extrude, sweep, loft, sheet metal, weldment, or assembly composition.

2. Build with the most reliable route available.
   - Prefer direct SolidWorks API or macro automation when `SldWorks.Application` is available and stable.
   - Prefer a SolidWorks VBA macro for rerunnable manual execution inside SolidWorks when external COM binding is fragile.
   - If SolidWorks automation fails but the geometry can be deterministically generated, create an STL/STEP/intermediate mesh or BREP and then provide an import macro or instructions for SolidWorks conversion.
   - Keep all output files in a single named output directory and use absolute paths in the final answer.

3. Validate independently before claiming success.
   - Check file existence and size.
   - Inspect or compute basic geometry facts: bounding box, volume, face/triangle count, hole voids, pattern count, counterbore depth, symmetry, and main diameters/lengths.
   - For STL output, verify that intended holes are empty and that important cylinders/flanges exist in the expected size ranges.
   - For SolidWorks output, rebuild, check unsuppressed features, confirm saved file version/type, and inspect mass properties or exported preview where possible.

4. Report honestly.
   - If the `.SLDPRT` or `.SLDASM` was actually created and verified, state that directly.
   - If only an STL/STEP plus a SolidWorks import macro was reliably produced, call that the reliable deliverable and state the limitation.
   - Do not hide failed API calls behind "model completed" language.

## Effective Operation Pattern

Use the pattern learned from the flange sleeve case:

- Generate a deterministic geometry artifact first when SolidWorks API calls are unreliable.
- Verify measurable features outside SolidWorks.
- Create a SolidWorks-side import macro only after the geometry artifact passes checks.
- Final answer should distinguish verified geometry from optional/manual conversion steps.

## Validation Checklist

Before final response, confirm:

- `output_path` exists.
- Main dimensions match the drawing or stated assumptions.
- All required holes/counterbores/patterns exist and are not filled.
- File type matches what was actually produced.
- A rerun path exists: macro/script or clear manual SolidWorks steps.
- Limitations are stated without overpromising.

## Final Response Shape

Return:

- Built/verified file paths.
- Short feature summary.
- Validation results with concrete measurements or counts.
- Any failed automation route and the fallback used.
- Next manual SolidWorks step only if it is genuinely still required.
