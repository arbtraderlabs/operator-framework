# Skill: execute-ticket

**Order:** 5 of 9
**Purpose:** Perform the work described by a single ticket, and only that
ticket's scope.

## When to use

For each ticket in `tickets/backlog/`, once its dependencies (declared on
the ticket) are in `tickets/done/`.

## Inputs

- The ticket (see [`templates/ticket.md`](../../templates/ticket.md)).
- The relevant section(s) of the specification it links to.
- Any decision ledger entries the ticket references.

## Procedure

1. **Move the ticket to `tickets/in-progress/`** before starting — the
   ticket's location is its status (see
   [`docs/TICKET_SYSTEM.md`](../../docs/TICKET_SYSTEM.md)).
2. **Re-read the ticket's acceptance criteria** before starting work, and
   keep them visible throughout — they define "done" for this ticket, not
   a general sense of completeness.
3. **Do the work described**, staying inside the ticket's stated scope. If
   you discover the ticket is actually larger or smaller than planned, stop
   and flag it — log a decision ledger entry and, if needed, split or merge
   tickets rather than silently expanding scope.
4. **Do not introduce real proprietary, private, or secret data** at any
   point, even temporarily (see
   [`README.md#security-and-privacy`](../README.md#security-and-privacy)).
5. **Log any decisions made during execution** (approach choices,
   trade-offs) in the decision ledger as they happen, not from memory
   afterward.

## Outputs

- The completed work itself (code, configuration, content — whatever the
  ticket specifies).
- Decision ledger entries for any material choices made during execution.

## Checkpoint

None mandatory mid-execution, but do not mark the ticket complete yourself
— that determination belongs to [`skills/report/skill.md`](../report/skill.md) followed by
independent [`skills/verify/skill.md`](../verify/skill.md).

## Next skill

[`skills/report/skill.md`](../report/skill.md)
