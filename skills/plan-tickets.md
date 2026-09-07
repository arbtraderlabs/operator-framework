# Skill: plan-tickets

**Order:** 4 of 9
**Purpose:** Decompose an approved specification into small, ordered,
independently executable tickets.

## When to use

After [`skills/write-spec.md`](write-spec.md) has produced a spec ready for
execution.

## Inputs

- The specification (see [`templates/spec.md`](../templates/spec.md)).
- Any existing tickets for the same project, to avoid duplication.

## Procedure

1. **Walk the spec's requirements** and group them into units of work small
   enough to execute and verify in one pass (see
   [`docs/ticket-system.md#what-makes-a-good-ticket`](../docs/ticket-system.md#what-makes-a-good-ticket)).
2. **Write each ticket** using [`templates/ticket.md`](../templates/ticket.md),
   with specific, checkable acceptance criteria — not vague descriptions.
3. **Declare real dependencies** between tickets so execution order is
   explicit, not assumed.
4. **Assign sequential ticket numbers** (`TCK-001`, `TCK-002`, ...) — see
   [`docs/ticket-system.md#numbering`](../docs/ticket-system.md#numbering).
5. **Place each ticket file in `tickets/backlog/`** (or the project's
   equivalent lifecycle directory — see
   [`docs/ticket-system.md`](../docs/ticket-system.md)).
6. **Log any decomposition decisions worth recording** — e.g. why a
   seemingly single requirement was split into multiple tickets, or
   deliberately kept together — in the decision ledger.

## Outputs

- A set of tickets in `tickets/backlog/`, each following
  [`templates/ticket.md`](../templates/ticket.md).
- Decision ledger entries for non-obvious decomposition choices.

## Checkpoint

Review the full ticket list against the spec before execution begins —
confirm every requirement maps to at least one ticket, and no ticket
exceeds a reviewable size.

## Next skill

[`skills/execute-ticket.md`](execute-ticket.md), run once per ticket in
dependency order.
