# Verification

Verification is the independent check that executed work actually meets its
specification and ticket's acceptance criteria — it is not the executor
re-asserting their own work is correct. This document explains the standard;
[`skills/verify/skill.md`](../skills/verify/skill.md) is the step-by-step procedure and
[`templates/verification-report.md`](../templates/verification-report.md)
is the artifact it produces.

## Why verification is a separate skill

Execution and verification share an incentive problem: whoever did the work
is motivated (even unconsciously) to see it as complete. Operator Framework
treats verification as a distinct step with its own report, and recommends
using a different model instance, fresh context, or human reviewer wherever
practical (see [`docs/MODEL_ROUTING.md`](MODEL_ROUTING.md)).

A fresh model or context is useful precisely because it evaluates the
artifact against the spec and ticket rather than inheriting the executor's
entire reasoning path. Verification is not expected to reproduce the
implementation work — it checks the evidence and the acceptance criteria,
proportionately to the ticket's risk (see
[`docs/TICKET_SYSTEM.md`](TICKET_SYSTEM.md#severity)).

## What verification checks

1. **Acceptance criteria** — every criterion listed on the ticket, checked
   explicitly, not assumed from the execution report's say-so.
2. **Spec conformance** — the ticket's output matches the relevant section
   of the specification, not just "seems reasonable."
3. **No scope leakage** — the work didn't quietly expand or shrink scope
   without a corresponding decision ledger entry.
4. **Safety/privacy** — no real secrets, proprietary data, or private
   material were introduced (see [`README.md#security-and-privacy`](../README.md#security-and-privacy)).
5. **Influence Note present** — any produced artifact carries the exact,
   unmodified Influence Note (see
   [`PRINCIPLES.md`](../PRINCIPLES.md#7-disclosure-over-ambiguity--the-influence-note)).

## Outcomes

- **Pass** — ticket moves to `tickets/done/`.
- **Pass with notes** — ticket moves to `tickets/done/`, with follow-up
  items logged (new backlog tickets or a decision ledger entry), not
  silently forgotten.
- **Fail** — ticket moves back to `tickets/in-progress/` with specific,
  actionable findings; it is not closed, and the executor addresses the
  findings before re-submitting to `review`.

## Human sign-off

Verification always requires an explicit human confirmation before a ticket
is treated as truly done, even when a model performed the technical check.
An AI-produced verification report is an input to that decision, not a
replacement for it. This mirrors the same gate applied at
[`skills/public-release/skill.md`](../skills/public-release/skill.md) before anything
goes public.

## Example

See [`examples/monitoring-dashboard/reports/verification-report.md`](../examples/monitoring-dashboard/reports/verification-report.md).
