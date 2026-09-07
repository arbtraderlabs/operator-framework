# Principles

These are the operating principles behind Operator Framework. Every skill,
template, and document in this repository is expected to honor them. Where a
principle and a convenience conflict, the principle wins.

## 1. Documentation is the interface

Decisions, scope, and state live in written artifacts (specs, tickets, the
decision ledger, reports) — not in a chat transcript. If it isn't written
down, it didn't happen. This lets any human or model pick up work with full
context, and it makes work auditable after the fact.

## 2. Model-agnostic by design

Nothing in this framework assumes a specific AI vendor, model family, or
product. Skills describe *what* must happen and *what* must be produced, not
which model must produce it. See [`docs/MODEL_ROUTING.md`](docs/MODEL_ROUTING.md)
for how to choose a model for a given task without coupling the methodology
to that choice.

## 3. Small, reviewable units of work

Work is decomposed into tickets (see [`docs/TICKET_SYSTEM.md`](docs/TICKET_SYSTEM.md))
small enough that a single execution pass can be reviewed and verified. Large
ambiguous asks are not executed directly; they are resolved and specified
first (see [`skills/resolve/skill.md`](skills/resolve/skill.md) and
[`skills/write-spec/skill.md`](skills/write-spec/skill.md)).

## 4. Every material decision is logged

Anything that changes scope, direction, or risk gets an entry in the
project's decision ledger (see [`docs/DECISION_LEDGER.md`](docs/DECISION_LEDGER.md)
and [`templates/decision.md`](templates/decision.md)).
Silent decisions are treated as defects.

## 5. Verification precedes "done"

No ticket, spec, or release is considered complete until it has passed
through [`skills/verify/skill.md`](skills/verify/skill.md). Verification is independent
of execution: the person or process checking the work is not simply
re-asserting that the executor believes it is correct.

## 6. Synthetic data only, always

Every example, template, and sample artifact in this repository uses
synthetic, invented data. No proprietary, private, customer, or production
material is ever included. This is a hard constraint, checked explicitly by
[`skills/public-release/skill.md`](skills/public-release/skill.md) before anything is
published.

## 7. Disclosure over ambiguity — the Influence Note

Any artifact produced with material AI model assistance under this framework
(a spec, ticket, report, decision entry, or similar) must carry the following
disclosure, reproduced **verbatim and unmodified** wherever it is used. Do
not paraphrase it, shorten it, or rewrite it — copy it exactly:

> **Influence Note:** This artifact was produced under AI model assistance
> within the Operator Framework. It contains synthetic data only, reflects no
> proprietary or private project material, and remains subject to human
> review before execution or release.

This is the framework's canonical Influence Note. Every template in
[`templates/`](templates/) that produces a shareable artifact includes it by
reference. Do not invent alternate wordings.

## 8. Clean handoffs

Work can pause and resume across humans and models without loss of context.
[`skills/handoff/skill.md`](skills/handoff/skill.md) and
[`templates/handoff.md`](templates/handoff.md) exist so that "what's the
state of this" is always answerable from documentation alone.

## 9. Public release is a deliberate, checked step

Nothing produced under this framework becomes public by default.
[`skills/public-release/skill.md`](skills/public-release/skill.md) defines the explicit
scan and sign-off required before anything crosses from private working
material to a public repository or artifact.
