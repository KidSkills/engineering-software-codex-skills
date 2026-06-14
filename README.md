# Engineering Software Skills for Codex

This repository contains six Codex skills for engineering-software workflows. They are distilled from practical CAD/CAE/CAM-adjacent operations and written as reusable `SKILL.md` folders.

The skills focus on verifiable engineering work: locating local software, opening real project files, exporting or visualizing results, checking output quality, and avoiding overclaiming when automation is unreliable.

## Skills Included

| Skill | Purpose |
| --- | --- |
| `solidworks-validated-delivery` | Build or deliver SolidWorks-style mechanical CAD models with independent geometry validation before claiming completion. |
| `ansys-fluent-visualization` | Open, recover, and visualize Ansys Fluent CFD projects, including mesh display, velocity contours, and pathlines. |
| `autocad-dwg-pdf-output` | Locate installed CAD software and export DWG layouts to checked PDF files. |
| `cad-render-fidelity-review` | Audit architectural renderings against CAD drawings for strict drawing fidelity. |
| `matlab-install-diagnostics` | Diagnose MATLAB installations, installers, licenses, and activation safely. |
| `engineering-dialogue-skill-mining` | Mine prior engineering-software conversations into reusable workflows and skills. |

## Installation

Install any skill by copying its folder into your Codex skills directory.

On Windows, the usual destination is:

```text
%USERPROFILE%\.codex\skills
```

Example:

```powershell
Copy-Item -Recurse .\solidworks-validated-delivery $env:USERPROFILE\.codex\skills\solidworks-validated-delivery
```

Install all six:

```powershell
$target = $env:USERPROFILE\.codex\skills
New-Item -ItemType Directory -Force -Path $target | Out-Null
Get-ChildItem -Directory | Where-Object { $_.Name -notin @('.git') } | ForEach-Object {
  Copy-Item -Recurse -Force $_.FullName (Join-Path $target $_.Name)
}
```

After copying, restart Codex or start a new thread so the skills are discoverable.

## Usage Examples

Use the skill names explicitly when you want to force a specific workflow:

```text
Use $solidworks-validated-delivery to build this flange sleeve from the drawing and verify the output.
```

```text
Use $ansys-fluent-visualization to open my Fluent case and show velocity contours and pathlines.
```

```text
Use $autocad-dwg-pdf-output to convert this DWG into PDFs and check that every layout exported correctly.
```

```text
Use $cad-render-fidelity-review to compare these renderings against the construction drawings.
```

```text
Use $matlab-install-diagnostics to find installed MATLAB versions and troubleshoot activation legally.
```

```text
Use $engineering-dialogue-skill-mining to extract reusable workflows from previous engineering software sessions.
```

## Design Principles

- Verify outputs before calling work complete.
- Prefer real file checks, software discovery, and reproducible commands over vague instructions.
- Keep privacy-sensitive paths and project names out of the reusable skills.
- Treat CAD, CAE, and installer automation as fragile until validated.
- State limitations clearly when a native file, visualization, or activation step was not fully completed.

## Repository Structure

Each skill is a folder with:

```text
skill-name/
  SKILL.md
  agents/
    openai.yaml
```

`SKILL.md` contains the agent-facing workflow. `agents/openai.yaml` contains UI metadata.

## Privacy

This public package is intentionally scrubbed of personal paths, private project names, chat transcripts, local usernames, and session identifiers. The skills describe general workflows rather than private source conversations.

## Notes

These skills do not include proprietary engineering software, licenses, project files, or bypass methods. They only provide Codex workflow instructions for operating user-owned software and files.
