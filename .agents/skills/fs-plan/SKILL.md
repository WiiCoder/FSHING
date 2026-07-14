---
name: fs-plan
description: Plan an approved FSHING requirement. Use when the user invokes /fs-plan, $fs-plan, provides a requirement ID for release scheduling, technical design, task decomposition, dependency analysis, rollout planning, or acceptance-test coverage before implementation.
---

# FSHING Plan

## Workflow

1. Read **AGENTS.md** and confirm project mode.
2. Require one existing requirement ID and read its Spec plus current index entry.
3. If the Spec is not approved for its current version, stop and report the missing review or approval gate.
4. If the requirement is ready but not scheduled, read **.agents/skills/release-plan/SKILL.md** and schedule it only when the target release and scheduling authority are explicit.
5. Read and execute **.agents/skills/feature-plan/SKILL.md** for the approved Spec version.
6. Verify that design, tasks, tests, repository IDs, component IDs, dependencies, rollout, and rollback all trace to FR/NFR and AC items.
7. Report implementation order, blockers, affected repositories, verification commands, and whether **/fs-implement** may start.

## Guardrails

- Do not write production code.
- Do not plan against an unapproved major Spec version.
- Do not invent product behavior, target releases, owners, or repository mappings.
- Do not create tasks without acceptance and test links.
