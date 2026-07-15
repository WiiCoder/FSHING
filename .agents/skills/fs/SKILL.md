---
name: fs
description: Use one natural-language entry point to initialize, create or change requirements, plan, implement, test, review, resume, report status, or release a FSHING project. Use when the user invokes /fs or $fs, describes a feature or bug without choosing a phase, asks to continue or finish current FSHING work, asks for progress or the next action, or requests a product release.
---

# FSHING

## Role

Own the workflow orchestration so the user can state an outcome instead of selecting phase commands. Keep **fs-init**, **fs-requirement**, **fs-plan**, **fs-implement**, **fs-test**, **fs-review**, and **fs-release** as the execution layer.

Read **AGENTS.md** and **docs/standards/conversation-and-synchronization.md** first. Determine the operating mode, requested outcome, active requirement or release, and the furthest authorized checkpoint before routing.

## Intent and Authorization

Infer the checkpoint from the user's natural language:

| User intent | Authorized workflow |
|---|---|
| status, progress, what is next | Inspect and report only; do not mutate project or child repositories |
| initialize, configure, validate workspace | Run **fs-init** |
| discuss, record, define, or change a requirement | Run through **fs-requirement**, then stop when the requirement is synchronized |
| plan, design, schedule, or estimate | Ensure the requirement is synchronized, then run through **fs-plan** |
| implement, build, fix, complete, finish, or deliver | Drive the requirement through planning, implementation, testing, and review as far as evidence and user decisions allow |
| test or verify a requirement | Run **fs-test**; include **fs-review** when the user asks for conformance or release readiness |
| review or audit | Run **fs-review** |
| release a version | Run **fs-release** through planning, verification, or release-ready; do not record released state from this request alone |
| confirm a completed formal release | After independently presenting and verifying release evidence, run **fs-release** to record released state |
| continue or resume | Resume to the deterministic checkpoint defined by the active item's current state |

Treat the action verb as the authorization boundary. A request to discuss or plan does not authorize production code. A request to implement, fix, complete, finish, or deliver authorizes the recorded in-scope code and verification work, but not pushing, deploying, destructive migrations, or formal release. For **continue** or **resume**, derive authorization from the state mapping below instead of treating the phrase as unlimited implementation permission.

If the intent is genuinely ambiguous, default to requirement confirmation plus planning and state that boundary. Ask only when choosing the wrong path would materially change behavior, data, permissions, safety, or external state.

## Orchestration

1. Determine the operating mode from the workspace root without mutation. For status or progress requests, report the mode and missing initialization inputs without executing **fs-init**. For authorized mutating work in template or incomplete initialization mode, route to **fs-init** and do not start project workflows until project mode validation passes. If initialization completes and the original intent authorizes further work, resume it; otherwise report the missing inputs.
2. Resolve the work item. Prefer an explicit requirement ID or release version. Otherwise search the indexes and feature or release folders for a matching or active item before creating anything.
3. For **continue** or **resume**, prefer the most recently updated non-terminal requirement or active release. Include backlog, draft, review, ready, scheduled, in-progress, verifying, release-ready, blocked, deferred, and active release states in the search. If multiple items are equally plausible, present the concise choices and ask the user to select one.
4. Determine the authorized checkpoint from the intent table. Do not ask the user to choose an internal fs command.
5. Before each phase, read the matching **.agents/skills/fs-*/SKILL.md** completely and execute it. Continue directly into the next authorized phase when its prerequisites are satisfied.
6. When any phase exposes a requirement gap, proactively discuss it, run **fs-requirement**, synchronize the requirement and affected artifacts, then resume the interrupted phase without asking the user to invoke another command.
7. After each phase, verify that status, Spec version, target release, indexes, tasks, tests, evidence, and actual repository state remain consistent.
8. Stop only when the authorized checkpoint is reached, a material user decision is required, initialization is incomplete, verification fails in a way that needs direction, an external or destructive action needs authorization, or a real dependency is unavailable.

Do not stop merely to recommend another fs command. Either continue within the authorization boundary or explain the actual blocker.

## Resume Checkpoints

Map **continue** or **resume** to one deterministic checkpoint:

| Current state | Resume behavior |
|---|---|
| backlog, draft, or review | Complete requirement confirmation and stop at ready |
| ready | Complete scheduling and feature planning, then stop before production code |
| scheduled or in-progress | Continue implementation, testing, and review as far as evidence allows |
| verifying | Continue testing and review |
| release-ready requirement | Report readiness and wait for an explicit release-version request |
| planning, active, or code-freeze release | Continue release planning or verification, but stop no later than release-ready |
| release-ready release | Present the verified release evidence and wait for a separate explicit confirmation that the formal release actually occurred |
| blocked or deferred | Attempt only documented, authorized unblock or rescheduling work; otherwise present the blocker and required decision |

Never infer formal release confirmation from **continue**, **resume**, or an ordinary **release vX** request.

## Multiple Outcomes

When one request contains independent product outcomes, create or reuse separate requirement IDs and record their dependencies. Continue in dependency order when the user's implementation intent clearly covers all of them; ask only when priority or scope materially changes the result.

## Output

Keep the user-facing report compact:

- current confirmed requirement or release understanding;
- outcome reached and active work item;
- decisions still needed, with impact and recommendation;
- files and document versions written back;
- tasks, tests, or evidence invalidated or requiring rework;
- implementation and verification result when applicable;
- current lifecycle stage and the next action the skill will take or the real blocker.

Do not expose the internal command sequence unless the user asks. Do not require the user to inspect Markdown files to understand pending decisions.

## Guardrails

- Preserve project and child-repository boundaries from **AGENTS.md**.
- Never invent requirements, decisions, evidence, commits, releases, or deployment facts.
- Never use approval metadata as a workflow gate.
- Never push, deploy, mark formally released, or perform destructive operations without explicit authorization and required evidence. An ordinary **release vX** request is not the separate confirmation required to record a formal release.
- Preserve the seven phase skills as direct expert and compatibility entry points, but do not make ordinary users coordinate them.
