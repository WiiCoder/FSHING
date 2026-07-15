---
name: fs-plan
description: Plan a confirmed, plan-ready FSHING requirement. Use when the user invokes /fs-plan, $fs-plan, provides a requirement ID for release scheduling, technical design, task decomposition, dependency analysis, rollout planning, or acceptance-test coverage before implementation.
---

# FSHING Plan

## Workflow

1. Read **AGENTS.md**, **docs/standards/conversation-and-synchronization.md**, and **docs/standards/definition-of-done.md**, then confirm project mode.
2. Require one existing requirement ID and read its Spec plus current index entry.
3. Confirm that the current Spec satisfies the Ready criteria and has no unresolved decision that would materially change scope, behavior, API, data, permissions, or acceptance. If the content is complete but status or index metadata is stale, synchronize them to ready. Do not check or require **approved_at**.
4. If a blocking question exists, proactively present it with impact and recommendation, use **.agents/skills/requirement-change/SKILL.md** after the user's confirmation, synchronize the requirement, and then resume planning.
5. If the requirement is ready but not scheduled, read **.agents/skills/release-plan/SKILL.md** and schedule it after the target release is known or confirmed by the user.
6. Read and execute **.agents/skills/feature-plan/SKILL.md** for the current confirmed Spec version.
7. If planning reveals a requirement gap, run the same confirmation-and-writeback loop before completing affected design, tasks, or tests.
8. Verify that design, tasks, tests, repository IDs, component IDs, dependencies, rollout, and rollback all trace to FR/NFR and AC items.
9. Report confirmed decisions, implementation order, blockers, affected repositories, verification commands, synchronized files, and whether **/fs-implement** may start.

## Guardrails

- Do not write production code.
- Do not plan affected behavior against an ambiguous or unsynchronized Spec version.
- Do not block planning solely because approval metadata or a sign-off is absent.
- Do not invent product behavior, target releases, owners, or repository mappings.
- Do not create tasks without acceptance and test links.
