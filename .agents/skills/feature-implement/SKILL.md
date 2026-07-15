---
name: feature-implement
description: Implement a confirmed and scheduled requirement against a fixed Spec version while maintaining task-to-code traceability. Use only when explicitly invoked as $feature-implement for expert control or when delegated by fs-implement or fs.
---

# Implement Feature

## Workflow

1. Read **AGENTS.md**, **docs/standards/conversation-and-synchronization.md**, **docs/standards/workspace-management.md**, the current confirmed Spec, design, tasks, test plan, and component-specific instructions.
2. Confirm status scheduled or in-progress, the Spec has no unresolved blocking decision, and every implementation task references the active spec_version. Do not require approval metadata.
3. Resolve affected repository IDs through **workspace.yaml**, inspect their actual **repos/** paths, verify the intended remotes, and preserve unrelated working-tree changes.
4. Set the requirement to in-progress when implementation actually begins and synchronize **docs/features/index.yaml**.
5. Implement in task dependency order. Keep behavior within the current confirmed FR/NFR and AC boundaries.
6. Run focused tests while iterating. Add or update automated tests mapped to the relevant TC and AC.
7. Record code evidence in **tasks.md** and **verification.md** using component repository plus commit SHA or PR URL. If no commit or PR exists yet, record the changed files and leave the evidence state explicit.
8. Update design and task documents when implementation reveals factual technical differences that do not change product behavior.
9. If product behavior, API contract, data requirements, permissions, or key acceptance must change, proactively present the gap, impact, and recommendation; stop affected work, use requirement-change after confirmation, synchronize the artifacts, and then resume.
10. Run final relevant component checks. Move to verifying only when the implementation is testable; never move directly to released.

## Guardrails

- Do not implement an ambiguous, stale, or unsynchronized Spec version.
- Do not block implementation solely because approval metadata is absent.
- Do not fabricate commit, PR, test, review, or deployment evidence.
- Do not mark a TC passed only because an automated test file exists.
- Do not mark release-ready before requirement-level verification is complete.
