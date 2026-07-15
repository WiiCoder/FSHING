---
name: release-plan
description: Create or update a semantic product release, its requirement scope, milestones, risks, deferrals, and gates. Use when planning a version, scheduling requirements, moving scope between versions, freezing scope, or maintaining docs/releases.
---

# Plan Release

## Workflow

1. Read **docs/standards/conversation-and-synchronization.md**, **docs/standards/workspace-management.md**, **docs/standards/release-versioning.md**, **docs/standards/requirement-lifecycle.md**, and **docs/standards/definition-of-done.md** completely.
2. Validate the requested version as semantic versioning and distinguish formal from prerelease versions.
3. Inspect **workspace.yaml**, **workspace.lock.yaml**, **docs/releases/index.yaml**, existing release directories, **docs/features/index.yaml**, and candidate Specs.
4. Create **docs/releases/<version>/** from **docs/releases/_template/** when the release does not exist.
5. Define the release goal, manager, planned dates, milestones, dependencies, risks, rollout, rollback, and gates without inventing unknown values.
6. Include only requirements whose current Spec is ready with no unresolved blocking decision. Set target_release to this version and status to scheduled after the release choice is known or confirmed; do not require approval metadata.
7. Keep **requirements.md**, affected Specs, feature index, and release index consistent in the same change.
8. For removed scope, record the original release, new release or cancellation, reason, and decision date. Preserve the requirement ID and history.
9. Initialize **repositories.yaml** from declared workspace repositories without claiming final commits before they are known. Check P0/P1 capacity, cross-component dependencies, migrations, security, compatibility, and verification needs.
10. Proactively present unresolved scope, date, dependency, deferral, or risk choices with impact and recommendation. After confirmation, immediately synchronize release documents and affected requirement Specs and indexes. Report included, deferred, blocked, and unresolved requirements plus the next release milestone.

## Guardrails

- Do not treat a documentation revision as a product version change.
- Do not schedule draft requirements or requirements with unresolved blocking decisions.
- Do not block scheduling solely because approval metadata is absent.
- Do not erase deferral history from an old release.
- Do not mark a release or requirement released during planning.
