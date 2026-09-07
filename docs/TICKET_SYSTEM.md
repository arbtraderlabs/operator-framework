# Ticket System

Tickets are the unit of executable work in Operator Framework. A
specification (see [`templates/spec.md`](../templates/spec.md)) is
decomposed into tickets by [`skills/plan-tickets/skill.md`](../skills/plan-tickets/skill.md);
each ticket is then executed independently by
[`skills/execute-ticket/skill.md`](../skills/execute-ticket/skill.md).

## Tickets are history too

Tickets are bounded execution units suited to lower-cost agents, but on a
long-lived project they are also the searchable record of what happened and
why. Human memory and chat scrollback are unreliable months later; the
ticket set is not. A future maintainer should be able to trace intent:

```
feature → ticket → spec → decision → report → verification
```

Write tickets so that trail stays intact: link to the spec section and the
decisions that shaped the work, and record the acceptance criteria that
define completion. Don't duplicate the full requirements into the ticket —
duplication is what lets the trail drift out of sync.

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

## Severity

Severity records a ticket's blast radius so work can be prioritised and
routed. It is a separate axis from **status** (which lifecycle directory the
ticket lives in) and from the **verification outcome** (pass |
pass-with-notes | fail, recorded on the verification report). Text labels
are the primary meaning; any colour coding is illustrative only.

| Severity | Label | Meaning |
|---|---|---|
| S0 | Critical | Immediate attention; severe production, security, or data-loss blast radius (or equivalent). |
| S1 | High | Priority work with meaningful operational, architectural, or delivery risk. |
| S2 | Medium | Normal engineering work requiring ordinary review (the default). |
| S3 | Low | Routine, low-risk, or cosmetic work. |

Most tickets default to S2; escalate only when the blast radius justifies
it. Severity influences — but does not alone determine — model routing and
review depth. Routing also weighs ambiguity, complexity, reversibility,
security/privacy exposure, and how clear the acceptance criteria are (see
[`docs/MODEL_ROUTING.md`](MODEL_ROUTING.md)).

## Route and verification contract

A ticket may carry a **Route** block recording, only where they differ from
the defaults, its execution profile, verification method, context required,
and escalation conditions (see [`templates/ticket.md`](../templates/ticket.md#route);
the defaults and mechanism vocabulary live in
[`docs/MODEL_ROUTING.md`](MODEL_ROUTING.md)). Recording a concrete
verification method at planning time lets verification exist before
execution. Ordinary tickets carry no Route block at all.

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
   [`docs/REPORTING_CONTRACT.md`](REPORTING_CONTRACT.md).
3. A verification report (`templates/verification-report.md`), written
   during `verify` — see [`docs/VERIFY.md`](VERIFY.md).

A ticket only moves to `tickets/done/` after its verification report records
a pass and a human has signed off.

## Example

See [`examples/monitoring-dashboard/tickets/`](../examples/monitoring-dashboard/tickets/)
for sample tickets at each lifecycle stage.
