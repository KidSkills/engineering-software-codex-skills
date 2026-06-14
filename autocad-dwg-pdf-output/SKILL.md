---
name: autocad-dwg-pdf-output
description: Locate installed CAD software and export DWG layouts to checked PDF files. Use when the user asks to convert DWG/CAD/AutoCAD drawings to PDF, batch plot layouts, inspect layout names, use AutoCAD/accoreconsole/COM automation, or troubleshoot missing CAD executables, plot settings, SHX/proxy objects, and generated PDF output.
---

# AutoCAD DWG PDF Output

Use this skill when the user needs a DWG turned into PDFs on the local machine. The effective pattern is: find the CAD engine, inspect layouts, export by layout, then verify the generated PDFs exist and are plausible.

## Discovery Workflow

1. Confirm the DWG path.
   - Use `Test-Path` and `Get-Item` to confirm existence, size, and timestamp.
   - Preserve the original DWG. Write outputs to a separate `pdf_output` or user-specified folder.

2. Locate CAD software.
   - Search common install folders for `acad.exe`, `accoreconsole.exe`, `gcad.exe`, `zwcad.exe`.
   - Check uninstall registry and Start Menu shortcuts for AutoCAD, Tianzheng, GstarCAD, ZWCAD, or similar.
   - Check `.dwg` file association when executable discovery is unclear.

3. Prefer noninteractive export first.
   - Use AutoCAD COM or `accoreconsole.exe` if available.
   - If COM works, open the DWG read-only for layout discovery, then reopen for plotting if needed.
   - If command-line export fails, switch to desktop automation only after confirming the GUI app can open the file.

## Layout Export Pattern

1. Enumerate layouts.
   - Read `doc.Layouts`.
   - Usually export paper-space layouts first, not `Model`, unless the user asks for model-space output.
   - Record layout names exactly, including Chinese names.

2. Plot each layout.
   - Set `BACKGROUNDPLOT` to `0` so export finishes before verification.
   - Use existing layout plot settings when possible.
   - Fall back to common PDF plotter settings only when the DWG lacks usable settings.
   - Name output PDFs by DWG base name plus layout name.

3. Verify output.
   - List PDFs with full path, size, and timestamp.
   - Check that each expected layout produced one PDF.
   - If possible, render or inspect the first page visually for blank pages, crop errors, or missing content.

## Common Failure Modes

- CAD executable is installed in a nonstandard folder outside the default Autodesk path.
- Layouts are named in Chinese and scripts fail from encoding assumptions.
- Only `Model` exports while actual drawings are in paper-space layouts.
- Background plotting returns before PDFs are fully written.
- Missing SHX fonts/proxy objects affect display but do not always block export.

## Final Response Shape

Return:

- CAD executable found.
- DWG file confirmed.
- Layouts detected.
- PDF output paths and sizes.
- Any layout skipped and why.
- Whether visual/page-level verification was performed.
