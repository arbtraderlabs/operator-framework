# Ticket System

Tickets are the unit of executable work in Operator Framework. A
specification (see [`templates/spec.md`](../templates/spec.md)) is
decomposed into tickets by [`skills/plan-tickets.md`](../skills/plan-tickets.md);
each ticket is then executed independently by
[`skills/execute-ticket.md`](../skills/execute-ticket.md).

## Lifecycle

Tickets move through four stages, represented as directories:

```
tickets/backlog/      → not yet started
tickets/in-progress/  → actively being executed
tickets/review/       → execution complete, awaiting/undergoing verification
tickets/done/         → verified and closed
```

Move the ticket file itself between directories as its status changes
(a ticket's location *is* its status — avoid letting a status field in the
file drift out of sync with its directory). See the `README.md` in each
[`tickets/`](../tickets/) subdirectory for stage-specific notes.

```
backlog ──▶ in-progress ──▶ review ──▶ done
                 ▲              │
                 └── rejected ──┘   (verification fails → back to in-progress)
```

## What makes a good ticket

- **Small.** Completable and reviewable in one execution pass. If it isn't,
  split it during `plan-tickets`.
- **Self-contained.** Links back to the relevant spec section and domain
  brief rather than restating them, but includes enough acceptance criteria
  to be executed without re-reading the whole spec.
- **Testable.** Has explicit, checkable acceptance criteria — "works
  correctly" is not a criterion; "returns HTTP 429 after the sixth request
  in 60 seconds" is.
- **Ordered honestly.** Declares its real dependencies on other tickets so
  `plan-tickets` output reflects an executable order, not just a list.

## Format

Use [`templates/ticket.md`](../templates/ticket.md) for every ticket.
Naming convention: `TCK-<3-digit-number>-<kebab-case-title>.md`
(e.g. `TCK-001-define-metrics-schema.md`).

## Numbering

Ticket numbers are assigned sequentially per project and are never reused,
even if a ticket is later dropped — this keeps references in the decision
ledger and reports unambiguous over time.

## Relationship to reporting and verification

Each ticket accumulates, over its life:
1. The ticket itself (`templates/ticket.md`), written during `plan-tickets`.
2. An execution report (`templates/execution-report.md`), written during
   `report`, once `execute-ticket` is complete — see
   [`docs/reporting.md`](reporting.md).
3. A verification report (`templates/verification-report.md`), written
   during `verify` — see [`docs/verify.md`](verify.md).

A ticket only moves to `tickets/done/` after its verification report records
a pass and a human has signed off.

## Example

See [`examples/monitoring-dashboard/tickets/`](../examples/monitoring-dashboard/tickets/)
for sample tickets at each lifecycle stage.
