# FSHING Agent Guide

## Determine the Operating Mode

Check the workspace root before acting:

- **Template mode**: **workspace.yaml** is absent and **workspace.example.yaml** is present.
- **Local overlay mode**: **workspace.yaml** exists and is ignored by the current clone through **.git/info/exclude**.
- **Initialization mode**: **workspace.yaml** exists, but project identity, required repository declarations, required clones, or **workspace.lock.yaml** are incomplete.
- **Project mode**: **workspace.yaml** and **workspace.lock.yaml** exist, required fields are non-null, and every required child repository matches the declaration and lock.

Never infer project identity from ignored directories below **repos/**.

## Local Overlay Mode

Use a git-ignored workspace only to apply or validate FSHING locally against real child repositories:

1. Confirm **git check-ignore workspace.yaml workspace.lock.yaml** succeeds.
2. Keep all overlay identity, remotes, branches, and commits out of tracked files.
3. Never commit project requirements, releases, indexes, or evidence to the FSHING origin.
4. Move durable project artifacts to a separate project control repository before treating them as managed history.

Local overlay mode does not convert the FSHING template repository into a product control repository.

## Initialization Mode

Only initialize the project workspace:

1. Fill project ID, name, and control-repository URL.
2. Declare at least one required child repository with ID, role, path, URL, default branch, and component IDs.
3. Clone every required repository into its declared path.
4. Verify each origin, default branch, HEAD, and working-tree status.
5. Create workspace.lock.yaml from actual Git state.

Do not create requirements, plan releases, implement features, or claim verification until project mode validation passes.

## Template Mode

In the FSHING source repository:

1. Modify only reusable standards, skills, templates, schemas, and workflow documentation.
2. Keep **workspace.example.yaml** empty of real project values.
3. Do not create or commit **workspace.lock.yaml**.
4. Do not add product requirements or release records to the template indexes.
5. Do not reference local child repository URLs, branches, commits, technologies, or component names in reusable files.
6. Treat any local **repos/** contents as ignored development fixtures unless the user explicitly places them in scope.

## Project Mode

In a project control repository:

- **workspace.yaml** declares project identity, child repository IDs, paths, remotes, default branches, and component IDs.
- **workspace.lock.yaml** records a resolved workspace snapshot.
- **docs/features/index.yaml** is the machine-readable requirement catalog.
- **docs/features/<ID>-<slug>/spec.md** is the authoritative definition of one requirement.
- **docs/releases/index.yaml** is the machine-readable release catalog.
- **docs/releases/<version>/requirements.md** records release scope and deferrals.
- **docs/releases/<version>/repositories.yaml** records exact shipped child revisions.

Keep indexes and their source documents consistent in the same change. Do not create a second manually maintained Markdown requirement index.

## Git Boundaries

1. The parent repository tracks workflow and project-management artifacts.
2. Directories below **repos/** are ignored independent Git repositories.
3. Never add, force-add, or commit **repos/*/** in the parent repository.
4. Run parent Git operations from the workspace root.
5. Run child Git operations with an explicit path resolved from **workspace.yaml**.
6. Record code evidence with repository ID plus commit SHA or PR URL.
7. Preserve unrelated changes in every child repository.
8. Never store credentials in workspace declarations, locks, requirements, or evidence.

## Non-negotiable Requirement Rules

1. Keep requirement ID, product release, Spec version, Git evidence, and test evidence separate.
2. Never change or reuse an assigned requirement ID.
3. Never encode a product version in a requirement ID.
4. Treat a major Spec change as a new approval cycle before continuing implementation.
5. Maintain the traceability chain: Release → Spec → FR/NFR → AC → TASK → Commit/PR → TC → Evidence.
6. Do not mark a requirement released until an actual production or formal release is confirmed.
7. Do not invent approvals, test results, deployment evidence, commit SHAs, PR URLs, dates, owners, or release membership.
8. If implementation reveals a requirement gap, use the requirement-change workflow before guessing product behavior.
9. Update affected design, tasks, tests, release records, and indexes whenever their source requirement changes.
10. Treat workspace.lock.yaml as a reproducibility snapshot, not as release evidence.

## Requirement Directory

~~~text
docs/features/<REQUIREMENT-ID>-<short-slug>/
├── spec.md
├── design.md
├── tasks.md
├── test-plan.md
└── verification.md
~~~

Copy from **docs/features/_template/**. Create **changes/<spec-version>.md** only when a major change needs durable impact analysis.

## Release Directory

~~~text
docs/releases/<semver>/
├── release-plan.md
├── requirements.md
├── repositories.yaml
├── test-report.md
└── release-notes.md
~~~

Copy from **docs/releases/_template/**.

## Verification

In project mode:

1. Resolve every affected repository through **workspace.yaml**.
2. Read that child repository's agent guidance and manifests.
3. Derive the appropriate build, static analysis, and test commands from the child repository.
4. Run the relevant commands in every affected repository.
5. Record the exact commands, revisions, environment, and results in feature or release evidence.

Do not hardcode technology-specific verification commands in reusable FSHING files.

## Project Skills

Use the simplified FSHING entry skills for user-facing work:

- **fs-init**: initialize or validate a workspace.
- **fs-requirement**: route requirement creation or change.
- **fs-plan**: route release scheduling and feature planning.
- **fs-implement**: implement an approved requirement.
- **fs-test**: execute requirement-level verification.
- **fs-review**: audit implementation and traceability.
- **fs-release**: plan or verify a release.

If a client passes **/fs-init**, **/fs-requirement**, **/fs-plan**, **/fs-implement**, **/fs-test**, **/fs-review**, or **/fs-release** as ordinary prompt text, treat it as invocation of the matching **fs-*** skill.

The following skills are the internal execution layer and remain available for direct expert use:

- **requirement-create**
- **requirement-change**
- **release-plan**
- **feature-plan**
- **feature-implement**
- **feature-test**
- **feature-review**
- **release-verify**
