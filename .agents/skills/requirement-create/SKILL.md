---
name: requirement-create
description: Create and conversationally confirm a new versioned and traceable product, bug, technical, security, or operations requirement. Use only when explicitly invoked as $requirement-create for expert control or when delegated by fs-requirement or fs.
---

# Create Requirement

## Workflow

1. Read **docs/standards/conversation-and-synchronization.md**, **docs/standards/requirement-versioning.md**, **docs/standards/requirement-lifecycle.md**, and **docs/standards/definition-of-done.md** completely.
2. Confirm the request is new rather than a change to an existing requirement. Use requirement-change for an existing ID.
3. Classify the requirement as FEAT, BUG, TECH, SEC, or OPS.
4. Inspect **docs/features/index.yaml** and existing feature folders. Allocate the next four-digit number for the current year and type. Never reuse an ID.
5. Choose a short lowercase hyphen-case slug. Create **docs/features/<ID>-<slug>/** from **docs/features/_template/**.
6. Fill every known Spec field. Leave unknown owner, date, release, and evidence fields null; never invent them. Do not add approval metadata.
7. Write concrete goals, non-goals, FR/NFR, AC, affected components, dependencies, risks, and decisions. Mark unresolved decisions as open instead of guessing.
8. Update **docs/features/index.yaml** in the same change with ID, title, type, priority, status, spec_version, target_release, introduced_in, released_in, owner, components, path, and updated_at.
9. Check that every AC references a valid FR or NFR and every cross-document reference uses the permanent requirement ID.
10. Proactively present unresolved product questions with impact and a recommendation. After the user confirms them, immediately update the Spec and index; set status to ready only when no blocking decision remains and all Ready criteria in **docs/standards/definition-of-done.md** are satisfied. Report the assigned ID, confirmed understanding, changed files, remaining non-blocking issues, and the next lifecycle action.

## Guardrails

- Do not include a product version in the requirement ID.
- Do not create code changes in this workflow.
- Do not mark ready while a material behavior, scope, API, data, permission, or acceptance decision remains unresolved.
- Do not require approval metadata after the requirement has been confirmed and synchronized.
- Do not silently merge separate product outcomes into one requirement; record explicit dependencies or create separate IDs.
