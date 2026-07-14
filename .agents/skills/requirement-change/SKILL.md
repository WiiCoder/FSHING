---
name: requirement-change
description: Revise an existing requirement while preserving its permanent ID and propagating version impact. Use when scope, behavior, API, data, permissions, acceptance criteria, target release, tasks, tests, or approval state changes.
---

# Change Requirement

## Workflow

1. Read **docs/standards/requirement-versioning.md**, **docs/standards/requirement-lifecycle.md**, and **docs/standards/testing.md** completely.
2. Locate the requirement by ID in **docs/features/index.yaml**. Read its Spec, design, tasks, test plan, verification evidence, and all release records that reference it.
3. State the requested before-and-after behavior. Identify affected FR/NFR, AC, API, data, permissions, components, tasks, tests, risks, and releases.
4. Classify the Spec change:
   - Increment the minor version for compatible clarification or added coverage that does not change approved core behavior.
   - Increment the major version for core flow, main scope, API, database, permission, or key acceptance changes.
5. Preserve the requirement ID and existing sub-item numbers. Assign new numbers only to new items; mark removed items instead of renumbering them.
6. Update **spec.md**, updated_at, Change Log, and dependent documents. For a major change, create **changes/<new-spec-version>.md** with a durable impact analysis.
7. For a major change, set status to review, clear approved_at, and require new product and technical approval. Reset affected test results to not-run.
8. If target_release changes, update the old release deferral record, the new release scope when applicable, the Spec, and the feature index. Update the release index only when version-level metadata changes.
9. Update design_version, plan_version, or test_plan_version when their content changes. Align every document to the new spec_version.
10. Report the version decision, impacted artifacts, invalidated evidence, required approvals, and remaining blockers.

## Guardrails

- Never change the requirement ID because of a release move.
- Never preserve a passed result when its covered behavior changed without re-evaluation.
- Never continue implementation against ambiguous or unapproved major changes.
- Never overwrite Change Log history.
