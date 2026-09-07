# Handoff

Work under Operator Framework must be resumable by a different human, a
different model, or the same participant after a long gap — without needing
to reconstruct context from memory or scrollback. This document describes
when and how to hand work off; the mechanics of writing the note are in
[`skills/handoff/skill.md`](../skills/handoff/skill.md) and
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
   lifecycle stage (see [`docs/TICKET_SYSTEM.md`](TICKET_SYSTEM.md)).
2. **What's done** — concretely, not "mostly finished."
3. **What's next** — the specific next action, not a vague area of work.
4. **Blockers** — anything the next person/model needs from someone else
   before they can proceed.
5. **Environment** — where this work lives: repository, branch, machine /
   environment, working-tree state, last known good commit.
6. **Pointers** — relative links to the exact files involved (spec section,
   ticket, decision ledger entries).

## Why handoff is context compression

Large context capacity is valuable, but focused engineering tasks still
benefit from focused, relevant context. Long-running projects accumulate far
more context than any single task needs — obsolete plans, completed work,
old logs, superseded decisions, repeated explanations, unrelated
conversations. The goal is to preserve the *right* context, not all of it.

A concise handoff reduces token cost: a fresh session starts from a small,
current working set instead of replaying a large history. It also makes
resumption robust to the interruptions that actually happen — an agent or
model crash, switching models, switching machines, or returning after a long
gap. In each case the handoff note, not the conversation, is what lets the
next session continue without re-doing completed work or re-deriving
decisions that are already made.

## What to capture, what to leave behind

Carry forward only what the next session needs to resume:

- **Environment** — host/environment, repository, branch, working-tree
  state, last known good commit.
- **Context to carry forward** — the active spec, the active ticket, and
  the relevant ADRs/decisions.
- **The exact next action** — named, not "continue the work."

Leave behind what is already resolved or committed: completed validation,
rejected approaches, already-resolved ambiguity, and work already committed.
Repeating it in a handoff spends the next session's context on decisions
that are already settled.

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
