---
name: requirement-change
description: Revise and conversationally reconfirm an existing requirement while preserving its permanent ID and propagating version impact. Use when scope, behavior, API, data, permissions, acceptance criteria, target release, tasks, tests, or requirement decisions change.
---

# Change Requirement

## Workflow

1. Read **docs/standards/conversation-and-synchronization.md**, **docs/standards/requirement-versioning.md**, **docs/standards/requirement-lifecycle.md**, **docs/standards/definition-of-done.md**, and **docs/standards/testing.md** completely.
2. Locate the requirement by ID in **docs/features/index.yaml**. Read its Spec, design, tasks, test plan, verification evidence, and all release records that reference it.
3. State the requested before-and-after behavior. Identify affected FR/NFR, AC, API, data, permissions, components, tasks, tests, risks, and releases.
4. Classify the Spec change:
   - Increment the minor version for compatible clarification or added coverage that does not change currently confirmed core behavior.
   - Increment the major version for core flow, main scope, API, database, permission, or key acceptance changes.
5. Preserve the requirement ID and existing sub-item numbers. Assign new numbers only to new items; mark removed items instead of renumbering them.
6. Before selecting among unresolved product choices, proactively present the change, open questions, impacts, and recommendation in the conversation. Do not make the user discover them in the change document.
7. After confirmation, update **spec.md**, updated_at, Change Log, and dependent documents immediately. For a major change, create **changes/<new-spec-version>.md** with a durable impact analysis, set status to review while confirmation is incomplete, and reset affected test results to not-run.
8. If target_release changes, update the old release deferral record, the new release scope when applicable, the Spec, and the feature index. Update the release index only when version-level metadata changes.
9. Update design_version, plan_version, or test_plan_version when their content changes. Align every document to the new spec_version.
10. Return to ready after all blocking decisions are confirmed, written back, and the Ready criteria are satisfied. Restore scheduled or in-progress only after the affected design, tasks, test plan, release scope, and lifecycle criteria are synchronized. Report the version decision, confirmed choices, impacted artifacts, invalidated evidence, remaining questions, and whether the interrupted fs phase can resume.

## Guardrails

- Never change the requirement ID because of a release move.
- Never preserve a passed result when its covered behavior changed without re-evaluation.
- Never continue affected implementation against an ambiguous or unsynchronized major change.
- Never require approval metadata to resume after the current Spec has been confirmed and synchronized.
- Never overwrite Change Log history.
