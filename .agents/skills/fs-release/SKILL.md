---
name: fs-release
description: Plan or verify a FSHING product release. Use when the user invokes /fs-release, $fs-release, supplies a semantic version for release scoping, deferral management, code freeze, repository snapshots, go/no-go review, formal release confirmation, or released-state updates.
---

# FSHING Release

## Route

1. Read **AGENTS.md** and **docs/standards/conversation-and-synchronization.md**, then confirm project mode.
2. Require one semantic product version.
3. Inspect **docs/releases/index.yaml** and the version directory.
4. If the version does not exist, or the user asks to define scope, dates, milestones, or deferrals, read and execute **.agents/skills/release-plan/SKILL.md**.
5. If the version exists and the user asks for readiness, code-freeze validation, go/no-go, deployment confirmation, or final state changes, read and execute **.agents/skills/release-verify/SKILL.md**.
6. If intent is not explicit, route planning/active releases to release-plan and code-freeze/release-ready releases to release-verify.
7. Proactively present unresolved scope, deferral, waiver, migration, rollback, or release-fact questions with impact and recommendation. After confirmation, synchronize the release records and any affected requirements before continuing.
8. Report confirmed decisions, synchronized files, scope, deferred requirements, unmet gates, repository revisions, recommendation, and every state change.

## Guardrails

- Do not infer formal release from a planned date, merge, build, or deployment command.
- Do not hide failed tests or missing repository revisions.
- Do not erase deferral history.
- Do not mix the FSHING workflow version with the product release version.
