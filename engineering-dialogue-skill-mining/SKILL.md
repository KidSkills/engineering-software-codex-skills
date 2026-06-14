---
name: engineering-dialogue-skill-mining
description: Mine prior Codex sessions and engineering-software conversations into reusable skills. Use when the user asks to read engineering software operation history, find CAD/SolidWorks/Ansys/MATLAB/DWG/engineering-cost operation dialogues, identify successful workflows, summarize command evidence, or convert repeated effective operations into separate SKILL.md files.
---

# Engineering Dialogue Skill Mining

Use this skill to turn prior conversations into reusable engineering-operation skills. The goal is not to dump chat history; it is to extract repeatable patterns with evidence, then write concise skills that another Codex instance can actually use.

## Scope And Privacy

- Read only locations the user authorizes or the current environment permits.
- Start with the current workspace, then Codex session indexes such as `.codex/session_index.jsonl`, `sessions`, and `archived_sessions` when authorized.
- Extract user requests, assistant final answers, tool calls, and command evidence.
- Do not include unrelated private chat content, account secrets, license keys, or full irrelevant transcripts.
- Preserve paths and thread IDs in an audit report when useful, but keep skills themselves free of personal details.

## Search Workflow

1. Build keyword groups.
   - Software: `CAD`, `AutoCAD`, `DWG`, `DXF`, `SolidWorks`, `SLDPRT`, `SLDASM`, `Ansys`, `Fluent`, `Workbench`, `MATLAB`, `Revit`, `BIM`, `COMSOL`.
   - Engineering work: cost estimating, quantity takeoff, drawings, BOQ, budget, rendering, model, modeling.
   - Chinese query equivalents: gongcheng zaojia, suanliang, tuzhi, qingdan, yusuan, xiaoguotu, xuanran, moxing, jianmo.
   - Operations: open, export, convert, save, inspect, run, command, operation, desktop, computer-use.

2. Search efficiently.
   - Use `rg --files` and `rg -n` for text files.
   - Exclude huge Base64/image/cache files that drown real evidence.
   - Parse session indexes to find thread titles and JSONL paths.
   - For each candidate thread, extract only relevant `user_message`, assistant process/final messages, and function/exec calls.

3. Classify threads.
   - Keep threads that include real engineering-software operations or reusable procedural lessons.
   - Drop false positives such as generic PDF/report generation unless they involve CAD/engineering software workflows.
   - Group by software and operation type.

## Skill Extraction Heuristics

Mark a workflow as worth turning into a skill when it has at least two of:

- It solved a real local software/file problem.
- It used a robust discovery sequence.
- It corrected a previous overclaim or failure mode.
- It produced a verifiable artifact.
- It contains menus, commands, file extensions, or validation checks likely to recur.
- It reveals a safety boundary, such as legal activation or not claiming unverified CAD output.

## Output Structure

Produce:

- An audit Markdown report with thread ID, title, path, user request summary, key operations, final result, and reusable lesson.
- A shortlist of candidate skills, each with trigger conditions and the effective operation pattern.
- Separate skill folders when the user asks to formalize them.

## Writing Skills From Dialogues

When creating skills:

- Keep frontmatter descriptions broad enough to trigger on Chinese and English requests.
- Put "when to use" information in the YAML description.
- Keep the body procedural and short.
- Remove personal paths, chat fragments, and one-off project names unless they are needed as examples.
- Include validation and final-response shape so future agents do not repeat vague or unverified delivery.

## Final Response Shape

Return:

- Number of threads reviewed and kept.
- Skills created or updated.
- Where the skill folders are saved.
- Any important limitations, such as garbled encoding or missing session files.
