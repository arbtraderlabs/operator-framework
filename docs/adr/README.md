# Architecture Decision Records

ADRs here capture durable, structural decisions about how Operator Framework
itself is built. They are distinct from the project-level
[decision ledger](../DECISION_LEDGER.md), which records decisions made
*while doing work* under the framework.

A project using Operator Framework may also keep its own ADR records for
major project architecture decisions (e.g. a `docs/adr/` folder inside that
project), using the same test: create an ADR when the choice is
architectural/structural, expensive or risky to reverse, or likely to be
questioned later — not for every decision. The decision ledger stays the
running record of everyday judgment calls; the ADR preserves the reasoning
behind durable choices.

| ADR | Title |
|---|---|
| [0001](ADR-0001-documentation-first-workflow.md) | Documentation-first workflow over conversational execution |
| [0002](ADR-0002-ticket-based-execution-lifecycle.md) | Ticket-based execution lifecycle with explicit stages |
| [0003](ADR-0003-model-agnostic-skill-design.md) | Model-agnostic skill design |
| [0004](ADR-0004-mandatory-human-verification-gate.md) | Mandatory human verification gate before release |
| [0005](ADR-0005-routing-as-execution-allocation.md) | Routing as execution allocation, not only model choice |

## Format

Each ADR follows a short, standard structure: Status, Context, Decision,
Consequences. New ADRs are numbered sequentially and, once accepted, are not
edited to reverse the decision — a later ADR may supersede an earlier one,
but the earlier one stays as a historical record (the same append-only
principle applied to the [decision ledger](../DECISION_LEDGER.md)).
