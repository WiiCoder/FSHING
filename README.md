# FSHING

FSHING is a reusable GitHub template for managing multi-repository software projects with AI-assisted requirements, implementation, testing, review, and release workflows.

FSHING contains workflow standards, skills, and document templates. It must not contain the repository URLs, branches, commits, requirements, or releases of a specific product.

## Operating Modes

### Template Mode

The FSHING source repository is in template mode when **workspace.yaml** is absent and **workspace.example.yaml** is present.

Template mode contains:

- **workflow-version.yaml**: the FSHING workflow version;
- **workspace.example.yaml**: an empty project workspace schema;
- **.agents/skills/**: reusable workflow skills;
- **docs/standards/**: reusable governance rules;
- **docs/features/_template/**: requirement artifact templates;
- **docs/releases/_template/**: release artifact templates.

Local repositories may exist below **repos/** for FSHING development or validation, but they are ignored and are never part of the FSHING template.

### Initialization Mode

A generated project is in initialization mode when **workspace.yaml** exists but project identity, repository declarations, or **workspace.lock.yaml** are incomplete.

Only workspace setup is allowed in this mode. Requirement creation, implementation, testing, and release workflows must wait until required repositories have been cloned and verified.

### Local Overlay Mode

FSHING maintainers may create **workspace.yaml** and **workspace.lock.yaml** only for local validation against real repositories. In this mode both files must be ignored through the clone's local **.git/info/exclude**, not through the tracked **.gitignore**.

Local overlay data must never be committed or pushed to FSHING. A real product still needs its own project control repository before project requirements and releases are versioned.

### Project Mode

A repository created from FSHING enters project mode after it has:

- non-null project identity and control-repository URL in **workspace.yaml**;
- at least one complete required child-repository declaration;
- an existing clone for every required repository;
- **workspace.lock.yaml** matching the actual child branches, commits, and dirty state.

Each project control repository must have its own Git origin. Project data must never be pushed back to the FSHING template repository.

## Create a Project

1. Use the GitHub **Use this template** action to create a new project control repository.
2. Copy **workspace.example.yaml** to **workspace.yaml**.
3. Fill the project identity, control-repository URL, child repository IDs, paths, remotes, default branches, and component IDs.
4. Clone each child repository into its declared path below **repos/**.
5. Inspect the actual child Git state and create **workspace.lock.yaml**.
6. Commit workspace files to the project control repository.
7. Create requirements under **docs/features/** and releases under **docs/releases/**.

## Generated Project Shape

~~~text
project-control/
├── AGENTS.md
├── .agents/skills/
├── docs/
├── workflow-version.yaml
├── workspace.example.yaml
├── workspace.yaml
├── workspace.lock.yaml
└── repos/
    ├── service-a/   independent Git repository
    ├── web-app/     independent Git repository
    └── worker/      independent Git repository
~~~

The parent repository never tracks files below **repos/*/**. Cross-repository work is represented by repository-qualified commit SHAs or PR URLs in tasks, verification evidence, and release snapshots.

## Version Boundaries

- **workflow-version.yaml** identifies the installed FSHING workflow version.
- Product versions identify released software.
- Spec versions identify requirement document revisions.
- Child repository commits identify exact code.
- Release **repositories.yaml** files identify the exact code included in one product release.

These identifiers remain independent.

## Updating FSHING

Upgrade workflow standards, skills, and templates as a separate parent-repository change. Validate existing project data against the new compatibility schema before changing **workflow-version.yaml**.
