# Skill: handoff

**Order:** 8 of 9
**Purpose:** Persist enough state that work can pause and resume cleanly,
across humans, models, or time gaps, without relying on conversational
memory.

## Why this matters

A handoff is context compression. Long projects accumulate obsolete plans,
superseded decisions, and completed work; dragging all of it into every new
session costs tokens and buries what matters. A concise handoff keeps the
small working set — current state, environment, active spec/ticket, next
action, and what not to repeat — so a fresh session resumes cheaply and
accurately.

## When to use

At the end of a session, whenever responsibility changes hands, before a
long pause, or immediately if you must stop unexpectedly — see
[`docs/HANDOFF_PROTOCOL.md`](../../docs/HANDOFF_PROTOCOL.md) for the full list of triggers.

## Inputs

- Current state of the spec, tickets, and decision ledger.
- Whatever context the next person/model will need that isn't already
  captured in those artifacts.

## Procedure

1. **Confirm ticket locations are accurate.** Every ticket should already
   be in the lifecycle directory that reflects its true status (see
   [`docs/TICKET_SYSTEM.md`](../../docs/TICKET_SYSTEM.md)) — fix any drift
   before writing the handoff note, don't describe drift instead of fixing
   it.
2. **Confirm the decision ledger is current.** Any decision made this
   session should already be logged (see
   [`docs/DECISION_LEDGER.md`](../../docs/DECISION_LEDGER.md)) — don't defer
   logging into the handoff note itself.
3. **Write the handoff note** using
   [`templates/handoff.md`](../../templates/handoff.md): environment,
   current state, what's done, what's next (specifically), blockers, and
   pointers. Include the context to carry forward (active spec, active
   ticket, relevant decisions) and explicitly list what must *not* be
   repeated (completed validation, rejected approaches, resolved ambiguity,
   committed work).
4. **Name the actual next action.** "Continue the work" is not sufficient —
   state the concrete next step.

## Outputs

- A handoff note (see [`templates/handoff.md`](../../templates/handoff.md)).
- Tickets and decision ledger left in an accurate, current state.

## Checkpoint

None mandatory, but a handoff note that doesn't let the next person start
within a few minutes of reading it has failed its purpose — reread it as if
you were the one resuming.

## Next skill

Whichever skill the handoff note names as the next action — commonly
[`skills/execute-ticket/skill.md`](../execute-ticket/skill.md) or
[`skills/verify/skill.md`](../verify/skill.md), or
[`skills/public-release/skill.md`](../public-release/skill.md) if the project is ready to
publish.
