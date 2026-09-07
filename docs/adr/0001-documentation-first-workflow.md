# ADR-0001: Documentation-First Workflow Over Conversational Execution

**Status:** Accepted

## Context

AI-assisted work is often driven entirely through chat: a human asks, a
model answers or acts, and the record of *why* lives only in a scrollback
transcript. This makes work hard to audit, hard to hand off, and easy to
silently scope-creep, because decisions are never forced into a durable,
reviewable form.

## Decision

Operator Framework requires that scope, decisions, execution, and
verification be captured in written artifacts (domain briefs, specs,
tickets, decision ledger entries, reports) rather than left implicit in a
conversation. See [`docs/methodology.md`](../methodology.md) for the full
artifact flow. Conversation is how work gets *done*; documentation is the
record of *what was decided and what happened*.

## Consequences

- **Positive:** Any human or model can pick up a project from its artifacts
  alone. Work is auditable after the fact. Handoffs (
  [`docs/handoff.md`](../handoff.md)) become tractable.
- **Positive:** Verification ([`docs/verify.md`](../verify.md)) has
  something concrete to check against, rather than "does this look right."
- **Negative:** Adds overhead versus pure chat-driven execution, especially
  for very small tasks. Mitigated by allowing lightweight compression of
  `resolve`/`write-spec` for trivial, low-risk tickets (see
  [`docs/methodology.md#when-to-deviate`](../methodology.md#when-to-deviate)),
  provided that compression itself is logged.
- **Negative:** Requires discipline to keep artifacts in sync with actual
  work; a stale spec or ticket is worse than none. Mitigated by treating
  the ticket's directory location as its single source of truth for status
  (see [`docs/ticket-system.md`](../ticket-system.md)).
