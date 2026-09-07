# Architecture Decision Records

ADRs here capture durable, structural decisions about how Operator Framework
itself is built — distinct from the project-level
[decision ledger](../decision-ledger.md), which records decisions made
*while doing work* under the framework.

| ADR | Title |
|---|---|
| [0001](0001-documentation-first-workflow.md) | Documentation-first workflow over conversational execution |
| [0002](0002-ticket-based-execution-lifecycle.md) | Ticket-based execution lifecycle with explicit stages |
| [0003](0003-model-agnostic-skill-design.md) | Model-agnostic skill design |
| [0004](0004-human-verification-gate-before-release.md) | Mandatory human verification gate before release |

## Format

Each ADR follows a short, standard structure: Status, Context, Decision,
Consequences. New ADRs are numbered sequentially and, once accepted, are not
edited to reverse the decision — a later ADR may supersede an earlier one,
but the earlier one stays as a historical record (the same append-only
principle applied to the [decision ledger](../decision-ledger.md)).
