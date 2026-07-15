---
name: feature-test
description: Build, execute, and record requirement-level testing against an exact Spec and target release. Use when creating test cases, checking acceptance coverage, running validation, recording evidence, retesting after a Spec change, or deciding whether a feature is release-ready.
---

# Test Feature

## Workflow

1. Read the current Spec, design, tasks, test plan, verification evidence, **docs/standards/conversation-and-synchronization.md**, **docs/standards/testing.md**, and **docs/standards/definition-of-done.md**.
2. Confirm test-plan spec_version and target_release match the requirement. Treat stale plans or prior results as invalid until assessed.
3. Build a coverage matrix for every FR/NFR and AC. Add missing TC items before claiming completeness.
4. Inspect actual implementation and code evidence in each affected component repository.
5. Execute the documented unit, API, UI, integration, E2E, security, performance, migration, rollback, or manual tests that apply.
6. Record environment, exact command or procedure, date, result, artifact, and verifier in **verification.md**. Redact secrets and personal data.
7. Mark failed, blocked, and not-applicable cases explicitly. Require a reason and impact assessment for not-applicable; proactively confirm it with the user when it materially reduces acceptance coverage.
8. If observed behavior or testability conflicts with the Spec, proactively present the discrepancy and recommendation, confirm the intended requirement, update the Spec and dependent test artifacts, and invalidate affected prior results before continuing.
9. Set status verifying while work remains. Set release-ready only when every applicable AC passes, blocking defects are absent, and evidence is complete.
10. Synchronize **spec.md**, **test-plan.md**, **verification.md**, and **docs/features/index.yaml** status and versions. Report confirmed changes, coverage gaps, failures, invalidated prior evidence, and the release-readiness decision.

## Guardrails

- Do not infer passed from code review, build success, or task completion.
- Do not reuse evidence from a changed behavior without re-evaluation.
- Do not mark released; formal release confirmation belongs to release verification.
- Do not expose credentials, tokens, customer content, or unredacted production data.
