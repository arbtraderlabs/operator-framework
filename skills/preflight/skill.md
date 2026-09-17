# Skill: preflight

**Order:** 1 of 9
**Purpose:** Confirm scope, access, environment, and safety before any other workflow skill runs.

## Why this matters

A short environment and scope check can prevent work being performed against
the wrong repository, branch, machine, account, or stale project state — or
with missing access that only surfaces mid-execution. Recovery from the wrong
environment costs far more than the check that avoids it.

Preflight should remove avoidable mistakes without turning routine work into ceremony.

## When to use

At the very start of engaging with a new request, whenever scope or context
changes materially, and before consequential execution when the project's
environment boundary is unknown or stale.

## Inputs

- The raw request, however informal.
- Any existing project artifacts if this is ongoing work (spec, tickets,
  decision ledger — see [`docs/METHODOLOGY.md`](../../docs/METHODOLOGY.md)).
- `ENVIRONMENTS.md` or equivalent environment/release documentation when the project has it.

## Procedure

1. **Confirm you understand the ask at a high level** — not full resolution
   yet (that's [`skills/resolve/skill.md`](../resolve/skill.md)), just enough to
   know what kind of work this is.
2. **Check for existing state.** If a project directory, spec, backlog,
   runbook, CI/release process, or other durable workflow already exists,
   read it before proceeding. If this is an established non-Operator project,
   consider [`skills/adopt/skill.md`](../adopt/skill.md) rather than restarting
   its planning process.
3. **Identify the active environment where it matters.** Establish the repository,
   branch, host/account/namespace role where relevant, and whether it is local/dev,
   test/sim, staging/candidate, production/live, public/release, or another
   project-defined class. Do not demand details that do not affect the requested work.
4. **Find the safe experimentation boundary.** Determine where development,
   debugging, destructive testing, and production-like validation are allowed
   to the depth justified by the task. Do **not** require a dedicated simulation
   environment when local isolation, tests, containers, branches, or another
   mechanism are sufficient for the project's actual risk.
5. **Use existing environment documentation before creating new artifacts.**
   Read `ENVIRONMENTS.md` when present, but also recognise equivalent runbooks,
   repository guards, deployment maps, CI/CD rules, or operational documentation.
   Create a minimal environment contract from
   [`templates/environment-contract.md`](../../templates/environment-contract.md)
   only when a real visibility gap would otherwise make consequential execution
   ambiguous or unsafe. See
   [`docs/ENVIRONMENT_GUARDRAILS.md`](../../docs/ENVIRONMENT_GUARDRAILS.md).
6. **Check access and constraints.** Do you (or the model) have what's needed
   — repository access, required context, time constraints, permissions?
   Flag gaps now rather than discovering them mid-execution.
7. **Run the safety check.** Confirm the request does not require introducing
   real proprietary data, secrets, or private material into artifacts tracked
   under this framework. If it does, flag this explicitly — synthetic or
   generalized versions only belong in public framework artifacts.
8. **Run the environment smell test.** Compare the expected environment,
   workspace responsibility, output target, and observed state. Respond in
   proportion to the consequence:
   - **inform / continue** when the state is consistent or a deviation is low-risk and contained;
   - **warn** when something is unexpected or inconsistent but not itself proof that continuing is unsafe;
   - **stop** when there is a clear high-consequence mismatch, such as destructive
     work targeting PROD when the ticket targets SIM or an explicit protected
     repository rule would be violated.
9. **Decide the path.** Is this ambiguous enough to need
   [`skills/resolve/skill.md`](../resolve/skill.md), clear enough to go to
   [`skills/write-spec/skill.md`](../write-spec/skill.md), or trivial enough
   for a single bounded ticket (see
   [`docs/METHODOLOGY.md#when-to-deviate`](../../docs/METHODOLOGY.md#when-to-deviate))?

## Unknown environment rule

If the active environment cannot be classified with sufficient confidence,
protect **consequential actions whose impact cannot be bounded**.

Read-only discovery and low-risk contained work may continue where safe.
Deployment, destructive commands, database writes, service restarts,
publication, credential changes, and other real-world side effects should
pause when the operator cannot establish that the target is appropriate.

## Outputs

- A short go/no-go decision where one is useful; routine safe work need not be burdened with ceremony.
- The identified environment and safe experimentation boundary where relevant.
- Any warnings, blockers, or missing access surfaced early.
- A minimal environment contract only when the project genuinely needs one and no equivalent durable source exists.

## Checkpoint

A **clear high-consequence environment mismatch**, an unknown consequential
target, or a security/privacy concern is a stop-and-confirm point before
execution. Lower-confidence inconsistencies should be surfaced as warnings
with the next sensible check rather than treated as automatic blockers.

## Next skill

[`skills/adopt/skill.md`](../adopt/skill.md) for an existing project needing an
assessment; [`skills/resolve/skill.md`](../resolve/skill.md) for ambiguous
requests; or [`skills/write-spec/skill.md`](../write-spec/skill.md) if the
problem is already clear.
