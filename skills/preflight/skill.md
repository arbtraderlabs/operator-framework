# Skill: preflight

**Order:** 1 of 9
**Purpose:** Confirm scope, access, environment, and safety before any other workflow skill runs.

## Why this matters

A short environment and scope check can prevent work being performed against
the wrong repository, branch, machine, account, or stale project state — or
with missing access that only surfaces mid-execution. Recovery from the wrong
environment costs far more than the check that avoids it.

## When to use

At the very start of engaging with a new request, whenever scope or context
changes materially, and before consequential execution when the project's
environment boundary is unknown or stale.

## Inputs

- The raw request, however informal.
- Any existing project artifacts if this is ongoing work (spec, tickets,
  decision ledger — see [`docs/METHODOLOGY.md`](../../docs/METHODOLOGY.md)).
- `ENVIRONMENTS.md` when the project has one.

## Procedure

1. **Confirm you understand the ask at a high level** — not full resolution
   yet (that's [`skills/resolve/skill.md`](../resolve/skill.md)), just enough to
   know what kind of work this is.
2. **Check for existing state.** If a project directory, spec, backlog,
   runbook, CI/release process, or other durable workflow already exists,
   read it before proceeding. If this is an established non-Operator project,
   consider [`skills/adopt/skill.md`](../adopt/skill.md) rather than restarting
   its planning process.
3. **Identify the active environment.** Establish the repository, branch,
   host/account/namespace role where relevant, and whether it is local/dev,
   test/sim, staging/candidate, production/live, public/release, or another
   project-defined class. Prefer the project's own vocabulary.
4. **Find the safe experimentation boundary.** Determine where development,
   debugging, destructive testing, and production-like validation are allowed.
   Do **not** require a dedicated simulation environment when local isolation,
   tests, containers, branches, or another mechanism are sufficient for the
   project's actual risk.
5. **Read or establish the environment contract.** For operational or
   multi-environment projects, read `ENVIRONMENTS.md`. If consequential
   boundaries exist but are undocumented, establish a minimal contract using
   [`templates/environment-contract.md`](../../templates/environment-contract.md)
   before ACT. See
   [`docs/ENVIRONMENT_GUARDRAILS.md`](../../docs/ENVIRONMENT_GUARDRAILS.md).
6. **Check access and constraints.** Do you (or the model) have what's needed
   — repository access, required context, time constraints, permissions?
   Flag gaps now rather than discovering them mid-execution.
7. **Run the safety check.** Confirm the request does not require introducing
   real proprietary data, secrets, or private material into artifacts tracked
   under this framework. If it does, flag this explicitly — synthetic or
   generalized versions only belong in public framework artifacts.
8. **Check for environment mismatch.** If the requested work targets one
   environment but the observed environment does not permit those actions,
   stop. Do not improvise or assume equivalent safety.
9. **Decide the path.** Is this ambiguous enough to need
   [`skills/resolve/skill.md`](../resolve/skill.md), clear enough to go to
   [`skills/write-spec/skill.md`](../write-spec/skill.md), or trivial enough
   for a single bounded ticket (see
   [`docs/METHODOLOGY.md#when-to-deviate`](../../docs/METHODOLOGY.md#when-to-deviate))?

## Unknown environment rule

If the active environment cannot be classified with sufficient confidence,
treat it as **protected** for consequential actions.

Read-only discovery may continue where safe. Deployment, destructive
commands, database writes, service restarts, publication, credential changes,
and other consequential actions stop until the environment is classified.

## Outputs

- A short go/no-go decision, stated explicitly.
- The identified environment and safe experimentation boundary where relevant.
- Any blockers or missing access surfaced immediately.
- A minimal environment contract when the project needs one and none exists.

## Checkpoint

Environment mismatch, an unknown consequential environment, or a security /
privacy concern is a stop-and-confirm point before execution.

## Next skill

[`skills/adopt/skill.md`](../adopt/skill.md) for an existing project needing an
assessment; [`skills/resolve/skill.md`](../resolve/skill.md) for ambiguous
requests; or [`skills/write-spec/skill.md`](../write-spec/skill.md) if the
problem is already clear.
