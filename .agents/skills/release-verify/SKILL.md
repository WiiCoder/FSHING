---
name: release-verify
description: Verify a planned product version against release scope, requirement states, test evidence, defects, migrations, rollback, and publication records. Use for release readiness, go/no-go review, final release reporting, or marking requirements released after a confirmed formal release.
---

# Verify Release

## Workflow

1. Read **docs/standards/conversation-and-synchronization.md**, **docs/standards/workspace-management.md**, **docs/standards/release-versioning.md**, **docs/standards/testing.md**, and **docs/standards/definition-of-done.md** completely.
2. Read **workspace.yaml**, the release plan, requirements, repositories snapshot, test report, release notes, release index entry, and every included requirement's Spec and verification evidence.
3. Confirm scope consistency and repository identity: target_release, Spec version, feature status, deferrals, removals, components, priorities, repository IDs, and paths.
4. Verify every included P0/P1 requirement is release-ready and every applicable AC has passed evidence. Check lower-priority exceptions are explicitly accepted.
5. Verify every repositories.yaml revision against the actual child repository and deployed evidence, then verify release-level migration, rollback, smoke, security, compatibility, and operational checks.
6. Check blocking defects, waivers, dependencies, code-freeze exceptions, known issues, and any operational decision records required by the release plan.
7. Update **test-report.md** with evidence-backed results and a go, no-go, or conditional-go recommendation.
8. Move the release to release-ready only when all gates pass. Do not infer actual release from readiness.
9. Proactively present every unresolved release decision or requirement discrepancy with impact and recommendation. After confirmation, synchronize the release records and affected requirements, but never replace missing test, deployment, or repository evidence with conversation alone.
10. After explicit evidence confirms formal release, set the release status to released, fill released_at, update each actually shipped requirement to released, fill released_in, and synchronize both indexes. Report unmet gates, exceptions, confirmed decisions, synchronized files, final recommendation, and every state change made.

## Guardrails

- Do not mark released from a planned date, merged PR, successful build, or deployment command alone.
- Do not use workspace.lock.yaml as final release evidence without verifying the actual shipped revisions.
- Do not release a requirement omitted from the final release scope.
- Do not hide failed or blocked tests behind an aggregate pass result.
- Do not invent release decisions or operational evidence.
