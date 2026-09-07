# Skill: plan-tickets

**Order:** 4 of 9
**Purpose:** Decompose an approved specification into small, ordered,
independently executable tickets.

## Why this matters

Tickets create bounded execution units small enough for lower-cost agents
and human review. They are also searchable history: on a long-lived project,
"did we already add this, and why" is answered by the ticket trail — not by
memory or chat scrollback.

## When to use

After [`skills/write-spec/skill.md`](../write-spec/skill.md) has produced a spec ready for
execution.

## Inputs

- The specification (see [`templates/spec.md`](../../templates/spec.md)).
- Any existing tickets for the same project, to avoid duplication.

## Procedure

1. **Walk the spec's requirements** and group them into units of work small
   enough to execute and verify in one pass (see
   [`docs/TICKET_SYSTEM.md#what-makes-a-good-ticket`](../../docs/TICKET_SYSTEM.md#what-makes-a-good-ticket)).
2. **Write each ticket** using [`templates/ticket.md`](../../templates/ticket.md),
   with specific, checkable acceptance criteria — not vague descriptions —
   and assign each a severity (see
   [`docs/TICKET_SYSTEM.md#severity`](../../docs/TICKET_SYSTEM.md#severity)).
3. **Record non-default Route overrides only.** Where a concrete
   verification method is known, or execution differs from the default
   (mechanism, context, or escalation), capture it in the ticket's **Route**
   section (see [`templates/ticket.md`](../../templates/ticket.md#route));
   otherwise omit the section entirely. Do not over-engineer trivial
   tickets — where no override applies, the defaults in
   [`docs/MODEL_ROUTING.md`](../../docs/MODEL_ROUTING.md) govern.
4. **Declare real dependencies** between tickets so execution order is
   explicit, not assumed.
5. **Assign sequential ticket numbers** (`TCK-001`, `TCK-002`, ...) — see
   [`docs/TICKET_SYSTEM.md#numbering`](../../docs/TICKET_SYSTEM.md#numbering).
6. **Place each ticket file in `tickets/backlog/`** (or the project's
   equivalent lifecycle directory — see
   [`docs/TICKET_SYSTEM.md`](../../docs/TICKET_SYSTEM.md)).
7. **Log any decomposition decisions worth recording** — e.g. why a
   seemingly single requirement was split into multiple tickets, or
   deliberately kept together — in the decision ledger.

## Outputs

- A set of tickets in `tickets/backlog/`, each following
  [`templates/ticket.md`](../../templates/ticket.md).
- Decision ledger entries for non-obvious decomposition choices.

## Checkpoint

Review the full ticket list against the spec before execution begins —
confirm every requirement maps to at least one ticket, and no ticket
exceeds a reviewable size.

## Next skill

[`skills/execute-ticket/skill.md`](../execute-ticket/skill.md), run once per ticket in
dependency order.
