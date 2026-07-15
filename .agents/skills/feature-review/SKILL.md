---
name: feature-review
description: Audit a requirement across Spec, design, tasks, implementation, tests, and evidence for standards and traceability. Use when reviewing a feature before verification or release, checking implementation against requirements, or finding missing links and unsupported status claims.
---

# Review Feature

## Workflow

1. Read **docs/standards/conversation-and-synchronization.md**, **docs/standards/workspace-management.md**, and all other standards that apply, then read the requirement Spec, design, tasks, test plan, verification evidence, and referenced release record.
2. Resolve repositories through **workspace.yaml** and inspect actual code changes and tests in every referenced child repository. Identify the relevant comparison point rather than reviewing unrelated history.
3. Verify metadata consistency: ID, spec_version, target_release, status, confirmed decisions, components, and index entries.
4. Verify the traceability chain for every item: FR/NFR → AC → TASK → component code evidence → TC → verification evidence.
5. Compare actual behavior with the current confirmed requirements, API/data/permission design, migration plan, compatibility rules, rollout, and rollback.
6. Check that status claims satisfy **docs/standards/definition-of-done.md**.
7. Record findings in **verification.md** or the user-requested review artifact with severity, evidence, affected IDs, and a concrete remediation.
8. Separate blocking correctness or traceability gaps from non-blocking improvements.
9. Proactively present requirement-versus-implementation ambiguities with impact and recommendation. After the user confirms intended behavior, synchronize the requirement through requirement-change; do not change production behavior unless the user also authorizes code fixes.
10. Report confirmed requirement corrections, synchronized artifacts, the review verdict, blocking findings, unverified claims, and exact next actions.

## Guardrails

- Do not accept self-reported evidence without checking available artifacts.
- Do not mark release-ready while blocking findings remain.
- Do not treat undocumented behavior as confirmed scope.
- Do not review only code when the request requires requirement conformance.
