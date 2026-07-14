---
name: requirement-create
description: Create a new versioned and traceable product, bug, technical, security, or operations requirement. Use when recording a new requirement, assigning a permanent requirement ID, creating a feature directory, or adding an entry to docs/features/index.yaml.
---

# Create Requirement

## Workflow

1. Read **docs/standards/requirement-versioning.md** and **docs/standards/requirement-lifecycle.md** completely.
2. Confirm the request is new rather than a change to an existing requirement. Use requirement-change for an existing ID.
3. Classify the requirement as FEAT, BUG, TECH, SEC, or OPS.
4. Inspect **docs/features/index.yaml** and existing feature folders. Allocate the next four-digit number for the current year and type. Never reuse an ID.
5. Choose a short lowercase hyphen-case slug. Create **docs/features/<ID>-<slug>/** from **docs/features/_template/**.
6. Fill every known Spec field. Leave unknown owner, date, approval, release, and evidence fields null; never invent them.
7. Write concrete goals, non-goals, FR/NFR, AC, affected components, dependencies, risks, and decisions. Keep the initial status at draft unless actual review evidence supports a later state.
8. Update **docs/features/index.yaml** in the same change with ID, title, type, priority, status, spec_version, target_release, introduced_in, released_in, owner, components, path, and updated_at.
9. Check that every AC references a valid FR or NFR and every cross-document reference uses the permanent requirement ID.
10. Report the assigned ID, created files, unresolved inputs, and the next lifecycle action.

## Guardrails

- Do not include a product version in the requirement ID.
- Do not create code changes in this workflow.
- Do not mark ready without current-version approval evidence.
- Do not silently merge separate product outcomes into one requirement; record explicit dependencies or create separate IDs.
