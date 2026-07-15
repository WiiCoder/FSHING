---
name: fs-review
description: Review a FSHING requirement and its implementation. Use only when the user explicitly invokes /fs-review or $fs-review for phase-specific control, or when delegated by fs.
---

# FSHING Review

## Workflow

1. Read **AGENTS.md** and **docs/standards/conversation-and-synchronization.md**, then confirm project mode.
2. Require one existing requirement ID.
3. Read the requirement artifacts, referenced release records, workspace declarations, and actual child-repository changes.
4. Read and execute **.agents/skills/feature-review/SKILL.md**.
5. Classify findings as blocking, non-blocking, or advisory with exact evidence and affected IDs.
6. Proactively present every requirement-versus-implementation ambiguity with impact and recommendation. When the user confirms the intended requirement, run requirement-change and synchronize the requirement artifacts; do not silently change production code.
7. Report confirmed requirement corrections, synchronized files, the verdict, unresolved findings, unsupported status claims, required fixes, and whether **/fs-release** may proceed.

## Guardrails

- Do not treat undocumented behavior as confirmed scope.
- Do not accept self-reported evidence without checking available artifacts.
- Do not silently implement fixes unless the user also authorizes changes.
- Do not mark release-ready while blocking findings remain.
