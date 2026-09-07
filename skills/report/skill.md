# Skill: report

**Order:** 6 of 9
**Purpose:** Produce an honest, checkable account of what was executed for
a ticket, as input to independent verification.

## When to use

Immediately after [`skills/execute-ticket/skill.md`](../execute-ticket/skill.md) completes
its work on a ticket.

## Inputs

- The ticket and its acceptance criteria.
- The work actually produced during execution.

## Procedure

1. **Move the ticket to `tickets/review/`** — execution is complete and it
   is now awaiting verification (see
   [`docs/TICKET_SYSTEM.md`](../../docs/TICKET_SYSTEM.md)).
2. **Write the execution report** using
   [`templates/execution-report.md`](../../templates/execution-report.md),
   checking off each acceptance criterion explicitly rather than asserting
   overall completion.
3. **Report deviations honestly.** If something wasn't done, was done
   differently than specified, or is uncertain, say so — a report that
   only lists successes undermines the verification step that follows (see
   [`docs/REPORTING_CONTRACT.md`](../../docs/REPORTING_CONTRACT.md)).
4. **Include the Influence Note** verbatim (see
   [`PRINCIPLES.md`](../../PRINCIPLES.md#7-disclosure-over-ambiguity--the-influence-note)).

## Outputs

- An execution report (see
  [`examples/monitoring-dashboard/reports/execution-report.md`](../../examples/monitoring-dashboard/reports/execution-report.md)
  for a worked example).

## Checkpoint

None mandatory here — the checkpoint that matters comes next, in
`verify`, but a report with unchecked or vague criteria should be
considered incomplete and revised before moving on.

## Next skill

[`skills/verify/skill.md`](../verify/skill.md)
