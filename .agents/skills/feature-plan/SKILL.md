---
name: feature-plan
description: Turn an approved requirement Spec into a concrete technical design, implementation task graph, and traceable test plan. Use when a ready or scheduled requirement needs design, task decomposition, impact analysis, rollout planning, or test coverage before coding.
---

# Plan Feature

## Workflow

1. Read the requirement Spec and **docs/standards/testing.md**, **docs/standards/requirement-lifecycle.md**, and **docs/standards/definition-of-done.md**.
2. Require status ready or scheduled and a non-null approved_at for the current spec_version. If not approved, stop planning implementation details and report the missing gate.
3. Inspect the actual affected component code, tests, architecture guidance, and component-specific agent instructions.
4. Complete **design.md** with current state, target design, exact modules, API/data/permission impact, observability, rollout, rollback, and compatibility.
5. Complete **tasks.md** with small dependency-ordered TASK items. Map every task to FR/NFR, AC, a workspace repository ID, a logical component ID, and an objective completion condition.
6. Complete **test-plan.md**. Map every AC and NFR to one or more TC items, including regression, migration, security, concurrency, and failure cases when applicable.
7. Ensure design, task plan, and test plan all reference the exact approved spec_version and target_release.
8. Identify unresolved DEC and RISK items. Do not hide blocking decisions inside implementation tasks.
9. Update plan or design versions and timestamps only when their content changes.
10. Report the implementation order, parallelizable work, blockers, verification commands, and traceability coverage.

## Guardrails

- Do not write production code in this workflow.
- Do not invent product behavior missing from the Spec.
- Do not create tasks without acceptance or verification links.
- Do not consider file creation alone a completed plan.
