# Handoff

Work under Operator Framework must be resumable by a different human, a
different model, or the same participant after a long gap — without needing
to reconstruct context from memory or scrollback. This document describes
when and how to hand work off; the mechanics of writing the note are in
[`skills/handoff.md`](../skills/handoff.md) and
[`templates/handoff.md`](../templates/handoff.md).

## When to hand off

- At the natural end of a session, whether or not the task is complete.
- Whenever responsibility moves from one person/model to another.
- Before any long pause (e.g. waiting on an external dependency, approval,
  or input).
- Immediately if you must stop unexpectedly mid-ticket.

A handoff is cheap; a lost afternoon reconstructing "what was I doing" is
not. When uncertain whether a handoff note is warranted, write one.

## What a handoff note must answer

1. **State** — which ticket(s)/spec are in play, and their current
   lifecycle stage (see [`docs/ticket-system.md`](ticket-system.md)).
2. **What's done** — concretely, not "mostly finished."
3. **What's next** — the specific next action, not a vague area of work.
4. **Blockers** — anything the next person/model needs from someone else
   before they can proceed.
5. **Pointers** — relative links to the exact files involved (spec section,
   ticket, decision ledger entries).

## Where it lives

A handoff note is a short markdown file following
[`templates/handoff.md`](../templates/handoff.md), stored alongside the
project's other artifacts (e.g. next to its `DECISIONS.md`) or attached to
the specific ticket it concerns. It is not a substitute for updating the
decision ledger or moving a ticket to its correct lifecycle directory —
it's a supplement that makes resuming fast.

## Anti-patterns

- Relying on chat history as the handoff mechanism — chat history is not
  guaranteed to be visible to whoever picks up the work next.
- Writing "continue where I left off" without saying where that is.
- Leaving a ticket's directory location (backlog/in-progress/review/done)
  out of sync with reality at handoff time.
