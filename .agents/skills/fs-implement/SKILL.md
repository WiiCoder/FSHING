---
name: fs-implement
description: Implement a planned FSHING requirement. Use only when the user explicitly invokes /fs-implement or $fs-implement for phase-specific control, or when delegated by fs.
---

# FSHING Implement

## Workflow

1. Read **AGENTS.md** and **docs/standards/conversation-and-synchronization.md**, then confirm project mode.
2. Require one scheduled or in-progress requirement ID.
3. Read its current Spec, design, tasks, test plan, and workspace repository declarations.
4. Read and execute **.agents/skills/feature-implement/SKILL.md**.
5. When implementation reveals a requirement gap or conflict, proactively present the issue, impact, and recommendation; run **.agents/skills/requirement-change/SKILL.md** after confirmation, synchronize all affected artifacts, and resume only the now-confirmed path.
6. After implementation, ensure every completed TASK records repository ID, component ID, changed files, and available commit or PR evidence.
7. Refresh affected workspace lock entries only from actual child Git state.
8. Report confirmed requirement changes, synchronized files, completed tasks, remaining tasks, tests run, code evidence, requirement status, and whether **/fs-test** may start.

## Guardrails

- Pause only affected work and route through **/fs-requirement** when confirmed behavior must change.
- Preserve unrelated child-repository changes.
- Do not fabricate commits, PRs, tests, or user decisions.
- Do not block implementation solely because approval metadata is absent.
- Do not mark release-ready or released.
