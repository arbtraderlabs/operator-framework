# ADR Template

Copy this file to an ADR file (e.g. `ADR-00N-<kebab-title>.md`) for
durable architectural decisions. See
[`docs/adr/README.md`](../docs/adr/README.md) for when to use ADRs.

Create an ADR when the choice is architectural or structural, expensive or
risky to reverse, or likely to be questioned months later — not for every
decision. Routine, reversible choices belong in the project decision ledger
instead (see [`docs/DECISION_LEDGER.md`](../docs/DECISION_LEDGER.md)). Six
months later, seeing a component in the repository does not explain why it
was chosen; the ADR preserves that reasoning and the alternatives that were
rejected.

---

# ADR-[NUMBER]: [Decision title]

- **Status:** proposed | accepted | superseded | deprecated
- **Date:** YYYY-MM-DD
- **Deciders:** [people or roles]
- **Related:** [specs, tickets, reports, or other ADRs]

## Context

What problem or architectural pressure requires a decision? Include the
constraints and options that materially shaped the choice.

## Decision

State the decision clearly and specifically.

## Consequences

### Positive

- [benefit]

### Negative or accepted trade-offs

- [trade-off]

## Alternatives considered

- **[Alternative]:** [why it was not selected]

## Follow-up

- [ticket, validation, or review needed]
