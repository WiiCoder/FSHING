---
name: fs-implement
description: Implement a planned FSHING requirement. Use when the user invokes /fs-implement, $fs-implement, supplies a scheduled requirement ID, asks to execute approved tasks across declared child repositories, or requests code changes with task-to-commit traceability.
---

# FSHING Implement

## Workflow

1. Read **AGENTS.md** and confirm project mode.
2. Require one scheduled or in-progress requirement ID.
3. Read its current Spec, design, tasks, test plan, and workspace repository declarations.
4. Read and execute **.agents/skills/feature-implement/SKILL.md**.
5. After implementation, ensure every completed TASK records repository ID, component ID, changed files, and available commit or PR evidence.
6. Refresh affected workspace lock entries only from actual child Git state.
7. Report completed tasks, remaining tasks, tests run, code evidence, requirement status, and whether **/fs-test** may start.

## Guardrails

- Stop and route to **/fs-requirement** when approved behavior must change.
- Preserve unrelated child-repository changes.
- Do not fabricate commits, PRs, tests, or approvals.
- Do not mark release-ready or released.
