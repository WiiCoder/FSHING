---
name: feature-plan
description: Turn a confirmed requirement Spec into a concrete technical design, implementation task graph, and traceable test plan. Use when a ready or scheduled requirement needs design, task decomposition, impact analysis, rollout planning, or test coverage before coding.
---

# Plan Feature

## Workflow

1. Read the requirement Spec and **docs/standards/conversation-and-synchronization.md**, **docs/standards/testing.md**, **docs/standards/requirement-lifecycle.md**, and **docs/standards/definition-of-done.md**.
2. Require status ready or scheduled and no unresolved blocking requirement decision for the current spec_version. Do not require **approved_at** or a sign-off.
3. Inspect the actual affected component code, tests, architecture guidance, and component-specific agent instructions.
4. Complete **design.md** with current state, target design, exact modules, API/data/permission impact, observability, rollout, rollback, and compatibility.
5. Complete **tasks.md** with small dependency-ordered TASK items. Map every task to FR/NFR, AC, a workspace repository ID, a logical component ID, and an objective completion condition.
6. Complete **test-plan.md**. Map every AC and NFR to one or more TC items, including regression, migration, security, concurrency, and failure cases when applicable.
7. Ensure design, task plan, and test plan all reference the exact current confirmed spec_version and target_release.
8. Identify unresolved DEC and RISK items. Proactively present material questions with impact and recommendation; after confirmation, update the Spec and dependent artifacts before continuing. Do not hide blocking decisions inside implementation tasks.
9. Update plan or design versions and timestamps only when their content changes.
10. Report the implementation order, parallelizable work, blockers, verification commands, and traceability coverage.

## Guardrails

- Do not write production code in this workflow.
- Do not invent product behavior missing from the Spec.
- Do not block planning solely because approval metadata is absent.
- Do not create tasks without acceptance or verification links.
- Do not consider file creation alone a completed plan.
