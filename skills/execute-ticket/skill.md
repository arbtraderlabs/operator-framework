# Skill: execute-ticket

**Order:** 5 of 9
**Purpose:** Perform the work described by a single ticket, and only that
ticket's scope.

## Why this matters

A ticket's boundaries are what keep a small request small. Without them,
opportunistic refactoring and unrelated "improvements" quietly turn low-risk
work into a large, hard-to-review change. Staying inside scope also makes
the ticket a fair unit for independent verification.

## When to use

For each ticket in `tickets/backlog/`, once its dependencies (declared on
the ticket) are in `tickets/done/`.

## Inputs

- The ticket (see [`templates/ticket.md`](../../templates/ticket.md)) and any
  **Route** overrides it records.
- The relevant section(s) of the specification it links to, and any decision
  ledger entries it references.
- Only the context the ticket actually needs — not a whole-project dump (see
  [`docs/MODEL_ROUTING.md`](../../docs/MODEL_ROUTING.md#context-least-privilege)).

## Procedure

1. **Move the ticket to `tickets/in-progress/`** before starting — the
   ticket's location is its status (see
   [`docs/TICKET_SYSTEM.md`](../../docs/TICKET_SYSTEM.md)).
2. **Re-read the ticket's acceptance criteria** — they define "done" for
   this ticket, not a general sense of completeness.
3. **Execute within scope**, honouring any **Route** overrides on the ticket
   (execution profile, verification method, context, escalation). Prefer a
   deterministic tool where correctness can be computed, and run a recorded
   verification method as you go where one is present.
4. **Stop rather than silently expanding scope or improvising.** If the
   ticket is materially larger or smaller than planned, stop and propose a
   split or merge. When you stop, classify the blocker — **specification**
   (contract deficient: return to planning, don't upgrade the executor),
   **capability** (contract clear but this executor can't do the section:
   escalate that section locally), or **reality/discovery** (new facts:
   update the durable truth and re-route) — and log a decision ledger entry.
   See [`docs/MODEL_ROUTING.md`](../../docs/MODEL_ROUTING.md#blockers-and-escalation)
   for the full doctrine. Never mark the ticket complete yourself.
5. **Do not introduce real proprietary, private, or secret data** at any
   point, even temporarily (see
   [`README.md#security-and-privacy`](../../README.md#security-and-privacy)).
6. **Log any material decisions** (approach choices, trade-offs) in the
   decision ledger as they happen.

## Outputs

- The completed work itself (code, configuration, content — whatever the
  ticket specifies), or a blocker classification and decision ledger entry
  if you stopped.
- Decision ledger entries for any material choices made during execution.

## Checkpoint

None mandatory mid-execution, but do not mark the ticket complete yourself —
that belongs to [`skills/report/skill.md`](../report/skill.md) followed by
independent [`skills/verify/skill.md`](../verify/skill.md). A stop condition
(step 4) is a stop-and-classify checkpoint before doing anything further.

## Next skill

[`skills/report/skill.md`](../report/skill.md)
