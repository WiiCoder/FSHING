---
name: fs-requirement
description: Create, discuss, confirm, or change a traceable FSHING requirement and immediately synchronize confirmed decisions. Use when the user invokes /fs-requirement, $fs-requirement, describes a new feature or bug, supplies an existing requirement ID to revise, changes scope or target release, or asks to maintain requirement metadata.
---

# FSHING Requirement

## Route

1. Read **AGENTS.md**, **docs/standards/conversation-and-synchronization.md**, and **docs/standards/definition-of-done.md**, then confirm project mode. Local overlay mode may be used only for non-durable validation.
2. Inspect the request for an existing requirement ID matching FEAT, BUG, TECH, SEC, or OPS.
3. If no existing ID is supplied and no matching requirement exists, read and execute **.agents/skills/requirement-create/SKILL.md**.
4. If an existing ID is supplied or a matching requirement already exists, read and execute **.agents/skills/requirement-change/SKILL.md**.
5. If identity is ambiguous, search **docs/features/index.yaml** and feature folders before allocating a new ID.
6. After drafting or changing the requirement, proactively present the current understanding, every material unresolved question, each question's impact, and a recommended answer in the conversation. Do not ask the user to inspect the files to discover these items.
7. Discuss blocking questions until confirmed. After every confirmation, immediately update **spec.md**, its Change Log, **docs/features/index.yaml**, and every affected design, task, test, verification, and release artifact.
8. Set the requirement to ready only when its current Spec satisfies **docs/standards/definition-of-done.md**, has no unresolved blocking decision, and all confirmation results are written back. Do not require **approved_at**, a signature, or a separate approval record.
9. When planning is included in the user's request or the user has explicitly authorized continued fs work, read and execute **.agents/skills/fs-plan/SKILL.md** without waiting for an approval gate. A requirement-only request does not authorize production implementation.

## Output

Report:

- requirement ID and Spec version;
- lifecycle status and target release;
- created or changed files;
- confirmed decisions, unresolved questions, and design, test, or release impacts;
- the next valid FSHING command.

## Guardrails

- Never create a duplicate requirement for the same requested change without explaining the distinction.
- Never change an existing requirement ID.
- Never hide a pending question only in a Markdown file or substitute an approval field for direct discussion.
- Never record an unresolved product choice as confirmed fact.
- Never implement code during this command.
