---
name: matlab-install-diagnostics
description: Diagnose MATLAB installations, installers, versions, licenses, and activation safely. Use when the user asks to install MATLAB to a drive, find existing R20xx installs, locate setup/activate_matlab, check license files, launch legal activation, or troubleshoot MATLAB startup without using cracks, registry hacks, or unauthorized license bypasses.
---

# MATLAB Install Diagnostics

Use this skill to help with MATLAB installation and activation while keeping licensing clean. The effective pattern is to detect what already exists, find official installers and activation tools, then guide legal activation without importing suspicious crack or registry files.

## Discovery Workflow

1. Check installed versions.
   - Search likely install roots such as `C:\Program Files\MATLAB`, other `Program Files\MATLAB` folders on user-provided drives, and custom paths mentioned by the user.
   - Record versions like `R2022b`, `R2023a`, `R2024a`, their paths, and whether `bin\matlab.exe` exists.

2. Search for installers.
   - Look for `setup.exe`, ISO contents, downloaded MathWorks installer folders, and archive names containing MATLAB/R2024a.
   - Confirm the installer source before running it.
   - Do not assume the newest requested version is available just because older versions exist.

3. Check license and activation files.
   - Look for legitimate license files under MATLAB install folders, MathWorks locations, or user-provided license paths.
   - Identify `activate_matlab.exe` in the installed version's `bin\win64` or activation folder.
   - Treat folders named `Crack`, `license bypass`, suspicious `.reg`, patched DLLs, or replacement executables as unsafe.

## Safe Activation Rules

- Do not import registry files from crack folders.
- Do not replace MATLAB executables or license manager files with unauthorized patched files.
- Do not provide bypass steps for MathWorks licensing.
- Offer legal routes: sign in with a MathWorks account, use an institution license, point to a valid license file, or ask the user to obtain the correct installer/license.
- It is okay to launch the official activation tool when the user asks and the path is verified.

## Installation Decision Tree

- If the requested version is already installed: verify `matlab.exe`, offer to launch, and check activation state.
- If another version is installed: explain the discovered version and ask whether it is acceptable or whether the exact version is required.
- If installer exists: run official installer to the requested drive after confirming target path and disk space.
- If installer is missing: report what was searched and what files are needed.
- If activation fails: collect exact error text, license type, host ID if relevant, and MathWorks account/license status.

## Final Response Shape

Return:

- Installed MATLAB versions and paths.
- Installer files found or missing.
- Activation tool path if found.
- What was launched or checked.
- Legal activation next step.
- Any unsafe files intentionally ignored.
