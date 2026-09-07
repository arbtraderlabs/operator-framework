# ADR-0002: Ticket-Based Execution Lifecycle With Explicit Stages

**Status:** Accepted

## Context

Once a specification exists, work still needs to be broken into pieces
small enough to execute and verify reliably, with a status model that
doesn't rely on memory or informal notes ("I think that one's basically
done"). Without an explicit lifecycle, tickets accumulate ambiguous,
untracked state.

## Decision

Work is decomposed into tickets (see
[`docs/TICKET_SYSTEM.md`](../TICKET_SYSTEM.md) and
[`templates/ticket.md`](../../templates/ticket.md)), and each ticket's
status is represented by which lifecycle directory it physically lives in:
`tickets/backlog/` → `tickets/in-progress/` → `tickets/review/` →
`tickets/done/`, with an explicit rejection path back from `review` to
`in-progress` on a failed verification (see
[`docs/VERIFY.md`](../VERIFY.md)).

## Consequences

- **Positive:** Status is unambiguous and machine-checkable — a ticket's
  directory *is* its status, so there is no separate status field that can
  drift out of sync.
- **Positive:** Reviewers can see the whole board state (what's queued,
  active, awaiting review, done) just by listing directories.
- **Negative:** Requires physically moving files between directories as
  part of every skill's completion step, which is an extra action compared
  to editing an in-place status field. Accepted as a worthwhile tradeoff for
  the consistency guarantee.
- **Negative:** Doesn't by itself prevent large tickets; ticket size is a
  discipline enforced during `plan-tickets` (see
  [`skills/plan-tickets/skill.md`](../../skills/plan-tickets/skill.md)), not by the
  directory structure.
