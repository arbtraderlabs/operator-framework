# Decision Ledger

The decision ledger is the running, append-only record of material choices
made on a project. It exists so that "why did we do it this way" always has
a written answer, independent of anyone's memory of a conversation.

## What counts as a decision

Log an entry whenever something changes:

- **Scope** — adding, dropping, or redefining what a spec or ticket covers.
- **Approach** — choosing one technical or process approach over a viable
  alternative.
- **Risk posture** — accepting a known risk, deferring a fix, or overriding
  a verification concern.
- **Routing** — which model or process handled a given skill, if that
  choice was deliberate (see [`docs/MODEL_ROUTING.md`](MODEL_ROUTING.md)).

Routine, reversible micro-choices (variable names, file layout inside a
single ticket) do not need a ledger entry. When in doubt, log it — the cost
of an unnecessary entry is far lower than the cost of an undocumented
material decision.

## Format

Each entry uses [`templates/decision.md`](../templates/decision.md)
and is appended to the project's `DECISIONS.md` file (see
[`examples/monitoring-dashboard/DECISIONS.md`](../examples/monitoring-dashboard/DECISIONS.md)
for a worked example). Entries are numbered sequentially and never edited
after the fact — if a decision is later reversed, add a *new* entry that
supersedes the old one and says so explicitly.

## Why append-only

An editable ledger stops being trustworthy: readers can no longer tell
whether an entry reflects contemporary reasoning or a later rewrite.
Append-only entries preserve the actual history of judgment calls, including
ones that were later reversed — which is often the most useful information
in the ledger.

## Relationship to ADRs

[Architecture Decision Records](adr/) capture durable, structural decisions
about the *framework itself* (see [`docs/adr/`](adr/)). The decision ledger
captures decisions made *while doing project work* under the framework.
A project's `DECISIONS.md` is not a place to re-litigate the framework's own
ADRs — if a project needs to deviate from an ADR, log that deviation and its
rationale as a decision, but treat it as an exception, not a silent override.

## Who writes entries

Any skill can and should write a decision ledger entry the moment it makes a
material choice — don't defer logging to the end of the session, and don't
let entries be reconstructed from memory afterward.
