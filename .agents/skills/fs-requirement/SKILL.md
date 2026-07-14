---
name: fs-requirement
description: Create or change a traceable FSHING requirement. Use when the user invokes /fs-requirement, $fs-requirement, describes a new feature or bug, supplies an existing requirement ID to revise, changes scope or target release, or asks to maintain requirement metadata.
---

# FSHING Requirement

## Route

1. Read **AGENTS.md** and confirm project mode. Local overlay mode may be used only for non-durable validation.
2. Inspect the request for an existing requirement ID matching FEAT, BUG, TECH, SEC, or OPS.
3. If no existing ID is supplied and no matching requirement exists, read and execute **.agents/skills/requirement-create/SKILL.md**.
4. If an existing ID is supplied or a matching requirement already exists, read and execute **.agents/skills/requirement-change/SKILL.md**.
5. If identity is ambiguous, search **docs/features/index.yaml** and feature folders before allocating a new ID.

## Output

Report:

- requirement ID and Spec version;
- lifecycle status and target release;
- created or changed files;
- approval, design, test, or release impacts;
- the next valid FSHING command.

## Guardrails

- Never create a duplicate requirement for the same requested change without explaining the distinction.
- Never change an existing requirement ID.
- Never infer approval.
- Never implement code during this command.
