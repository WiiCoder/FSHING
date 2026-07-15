---
name: fs-test
description: Test and verify a FSHING requirement. Use when the user invokes /fs-test, $fs-test, supplies a requirement ID for acceptance coverage, regression execution, evidence collection, Spec-change retesting, or a release-readiness decision.
---

# FSHING Test

## Workflow

1. Read **AGENTS.md** and **docs/standards/conversation-and-synchronization.md**, then confirm project mode.
2. Require one existing requirement ID in in-progress, verifying, or release-ready review.
3. Read the current Spec, design, tasks, test plan, verification evidence, and actual child revisions.
4. Read and execute **.agents/skills/feature-test/SKILL.md**.
5. Verify every applicable AC and NFR maps to executed TC evidence.
6. If testing exposes an ambiguous or incorrect requirement, proactively present the discrepancy, impact, and recommendation; after confirmation, run requirement-change, synchronize the Spec and test artifacts, invalidate affected evidence, and resume the applicable tests.
7. Refresh affected workspace lock entries from actual Git state after test-related commits.
8. Report confirmed requirement changes, synchronized files, passed, failed, blocked, not-applicable, coverage gaps, invalidated evidence, and the release-readiness decision.

## Guardrails

- Do not treat build success or code review as acceptance evidence.
- Do not reuse stale evidence after changed behavior without assessment.
- Do not mark a requirement released.
- Do not expose secrets or unredacted customer data.
