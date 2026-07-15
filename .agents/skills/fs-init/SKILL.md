---
name: fs-init
description: Initialize or validate a FSHING project workspace. Use when the user invokes /fs-init, $fs-init, asks to create workspace.yaml, clone declared child repositories, generate workspace.lock.yaml, or diagnose template, overlay, initialization, and project modes.
---

# FSHING Initialize

## Workflow

1. Read **AGENTS.md**, **docs/standards/conversation-and-synchronization.md**, and **docs/standards/workspace-management.md** completely.
2. Determine the operating mode from workspace files and Git ignore state.
3. In FSHING template mode, do not write real project values into tracked template files. Instantiate a project only in a repository with its own project-control origin.
4. In initialization mode, copy **workspace.example.yaml** to **workspace.yaml** when needed, then fill only user-provided or discoverable project identity and repository data.
5. Validate every required repository declaration: ID, role, path, URL, default branch, required flag, and component IDs.
6. For each declared repository, inspect the actual path. Clone it only when the URL is known, the path is absent, and the user asked to initialize the project.
7. Verify each child origin, default branch, current branch, HEAD, and dirty state.
8. Create or refresh **workspace.lock.yaml** from actual Git state. Never invent a branch or commit.
9. Confirm parent Git ignores **repos/*/** and does not stage embedded repositories.
10. Proactively present missing project identity or repository choices with impact and recommendation. After confirmation, immediately write discoverable or user-provided values to the workspace files, revalidate them, and report the operating mode, initialized repositories, remaining inputs, lock status, and whether project workflows are allowed.

## Guardrails

- Do not push project data to the FSHING template origin.
- Do not store credentials in repository URLs or workspace files.
- Do not overwrite a dirty child repository.
- Do not enter project mode while required declarations, clones, or lock entries are incomplete.
