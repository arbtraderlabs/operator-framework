# Skill: preflight

**Order:** 1 of 9
**Purpose:** Confirm scope, access, and safety before any other skill runs.

## Why this matters

A thirty-second environment and scope check can prevent work being performed
against the wrong repository, branch, machine, account, or stale project
state — or with missing access that only surfaces mid-execution. Recovery
from the wrong environment costs far more than the check that avoids it.

## When to use

At the very start of engaging with a new request, and again whenever scope
or context changes materially (new stakeholders, new systems in play).

## Inputs

- The raw request, however informal.
- Any existing project artifacts if this is ongoing work (spec, tickets,
  decision ledger — see [`docs/METHODOLOGY.md`](../../docs/METHODOLOGY.md)).

## Procedure

1. **Confirm you understand the ask at a high level** — not full
   resolution yet (that's [`skills/resolve/skill.md`](../resolve/skill.md)), just enough
   to know what kind of work this is.
2. **Check for existing state.** If a project directory, spec, or ticket
   backlog already exists, read it before proceeding — don't restart work
   that's already in flight.
3. **Check access and constraints.** Do you (or the model) have what's
   needed — repository access, required context, time constraints? Flag
   gaps now rather than discovering them mid-execution.
4. **Run the safety check.** Confirm the request does not require
   introducing real proprietary data, secrets, or private material into
   artifacts that will be tracked under this framework (see
   [`README.md#security-and-privacy`](../README.md#security-and-privacy)).
   If it does, flag this explicitly — synthetic/generalized versions only
   belong in tracked artifacts.
5. **Decide the path.** Is this ambiguous enough to need
   [`skills/resolve/skill.md`](../resolve/skill.md), or clear enough to go straight to
   [`skills/write-spec/skill.md`](../write-spec/skill.md) or even directly to a single
   ticket for trivial work (see
   [`docs/METHODOLOGY.md#when-to-deviate`](../../docs/METHODOLOGY.md#when-to-deviate))?

## Outputs

- A short go/no-go decision, stated explicitly (not just proceeding
  silently).
- Any blockers or missing access, surfaced immediately rather than
  discovered later.

## Checkpoint

None mandatory here, but if the safety check in step 4 raises a concern,
treat that as a stop-and-confirm point before continuing.

## Next skill

[`skills/resolve/skill.md`](../resolve/skill.md) for ambiguous requests, or
[`skills/write-spec/skill.md`](../write-spec/skill.md) if the problem is already clear.
