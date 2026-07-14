---
name: fs-review
description: Review a FSHING requirement and its implementation. Use when the user invokes /fs-review, $fs-review, supplies a requirement ID for traceability audit, implementation conformance, status validation, evidence review, or pre-release quality assessment.
---

# FSHING Review

## Workflow

1. Read **AGENTS.md** and confirm project mode.
2. Require one existing requirement ID.
3. Read the requirement artifacts, referenced release records, workspace declarations, and actual child-repository changes.
4. Read and execute **.agents/skills/feature-review/SKILL.md**.
5. Classify findings as blocking, non-blocking, or advisory with exact evidence and affected IDs.
6. Report the verdict, unresolved findings, unsupported status claims, required fixes, and whether **/fs-release** may proceed.

## Guardrails

- Do not approve undocumented behavior.
- Do not accept self-reported evidence without checking available artifacts.
- Do not silently implement fixes unless the user also authorizes changes.
- Do not mark release-ready while blocking findings remain.
