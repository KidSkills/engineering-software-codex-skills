---
name: ansys-fluent-visualization
description: Open, recover, and visualize Ansys Fluent CFD projects and solution files. Use when the user asks for Ansys/Fluent/Workbench CFD display, airflow state, velocity contours, pathlines, mesh display, aircraft/projectile flow visualization, locating .wbpj/.cas/.cas.h5/.dat/.dat.h5/.msh files, or diagnosing why geometry is not visible in Fluent/CFD-Post.
---

# Ansys Fluent Visualization

Use this skill to turn a CFD project into something the user can actually see: mesh, wall surfaces, velocity contours, and pathlines. The main lesson is to verify installations, running processes, case files, and visible surfaces before giving menu instructions.

## Discovery Workflow

1. Locate Ansys tools.
   - Search for Workbench, Fluent, Fluent Launcher, SpaceClaim, Meshing, and CFD-Post.
   - On Windows, check common Ansys install roots such as `C:\Program Files\ANSYS Inc\...` or any user-provided install drive, and running processes matching `RunWB2`, `AnsysWBU`, `fluent`, `cfdpost`, `ansyslmd`.
   - If an MCP or integration finds paths but process listing fails, use a lightweight local process check.

2. Locate project and solver files.
   - Search the working directory and likely user folders for `.wbpj`, `.agdb`, `.pmdb`, `.msh`, `.cas`, `.cas.h5`, `.dat`, `.dat.h5`, `.stl`, `.step`, `.stp`.
   - Prefer the newest matching files only after checking the user-provided save location.
   - Record the exact case/solution name loaded in Fluent.

3. Open the most direct visualization route.
   - If the user needs Fluent-only output, open Fluent with the case/data files rather than Workbench.
   - If the project is already open, attach mentally to the running app and avoid launching duplicates unless needed.
   - If the model is not visible, first display mesh/wall surfaces before assuming the case is broken.

## Fluent Display Sequence

Use this order for flow visualization:

1. Display the body surface:
   - `Results -> Graphics -> Mesh`
   - Choose wall/body surfaces, often named like `wall-*`.
   - Display edges or shaded mesh to prove geometry is present.

2. Create a cutting plane:
   - `Results -> Surfaces -> Plane`
   - Use a central `x-y`, `x-z`, or user-relevant symmetry plane through the model.
   - Name it clearly, such as `center_velocity_plane`.

3. Display velocity contours:
   - `Results -> Graphics -> Contours`
   - Variable: `Velocity -> Velocity Magnitude`
   - Surface: the created central plane.
   - Use filled contours and a visible color scale.

4. Display pathlines:
   - `Results -> Graphics -> Pathlines`
   - Release From: inlet surface, often `velocity-inlet-*`.
   - Color By: `Velocity Magnitude`.
   - Click `Compute`, then `Display`.

## Troubleshooting Visibility

If the user says they cannot see the airplane/projectile:

- Check whether only a contour plane is displayed; display the wall/body surface too.
- Check that wall surfaces are not hidden, transparent, or outside the camera frame.
- Fit view, reset camera, and display mesh first.
- Verify that the loaded project is the intended one, not only an empty setup.
- Explain that velocity plots on a plane can hide the solid unless the wall surface is also displayed.

## Final Response Shape

Return:

- Detected Ansys/Fluent paths and loaded project/case name.
- Whether Fluent is open and ready.
- Exact menu steps for mesh, contours, and pathlines.
- The surfaces or variables to select.
- The likely reason if geometry is invisible.
