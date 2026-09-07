# ADR-0005: Routing as Execution Allocation, Not Only Model Choice

- **Status:** proposed
- **Date:** 2026-09-07
- **Deciders:** Operator Framework maintainers (under human review)
- **Related:** [`MODEL_ROUTING.md`](../MODEL_ROUTING.md), [`templates/ticket.md`](../../templates/ticket.md), [ADR-0002](ADR-0002-ticket-based-execution-lifecycle.md)

## Context

v0.1 described ROUTE mostly as *which model performs a given skill* and
correctly framed model routing as an optimization, not a requirement. But
the cost of work is not only model price: the framework repeatedly decides
*who or what* executes already-defined work, what context that executor
receives, how success will be demonstrated, and when execution must stop.
Treating routing as only "which model to buy" invites paying
reasoning-model cost for work a deterministic tool or a cheap executor could
do reliably — and, worse, "solving" a missing decision or vague acceptance
criterion by upgrading to a more expensive model when the real defect is
upstream in planning.

## Decision

Define ROUTE as the execution-allocation decision for already-defined
(bounded) work. A route may specify the execution mechanism, the minimum
context the executor needs, the verification method, and the escalation
conditions; model choice is one dimension of a route, not the whole of it.
Operational detail — the mechanism vocabulary, the uncertainty/risk/
verification relationship, the blocker taxonomy, and the adopted principles
(deterministic-first, cheapest reliable path to verified completion, context
least privilege, escalate the blocker not the workload) — lives canonically
in [`MODEL_ROUTING.md`](../MODEL_ROUTING.md); this ADR records only the
durable decision.

Where execution differs from the default, the route is captured on the
ticket in a Route section (see [`templates/ticket.md`](../../templates/ticket.md));
ordinary tickets carry no Route section and use the defaults. Routing
remains an optimization: a single general-purpose model can still perform
every skill.

## Alternatives considered

- **Add a tenth sequential `route` skill.** Rejected: routing is an
  optimization, not a required stage ceremony, and a mandatory skill would
  duplicate the ticket-authoring already done by `plan-tickets`.
- **Create a separate `docs/ROUTING.md`.** Rejected as duplication:
  [`MODEL_ROUTING.md`](../MODEL_ROUTING.md) is the existing routing home and
  is broadened in place.

## Consequences

### Positive

- ROUTE becomes operational: routes are written contracts on tickets where
  non-default, and the doctrine tells routers and executors what to
  consider.
- Cheap, reliable execution is safer because tickets can carry their
  verification method and escalation conditions up front.
- Blocker handling distinguishes planning defects, capability gaps, and new
  discovery, keeping escalation local.

### Negative or accepted trade-offs

- Adds a Route section to the ticket template; mitigated by making it
  optional and default-driven so ordinary tickets carry no routing metadata.
- Adds routing vocabulary; mitigated by keeping it model- and
  vendor-agnostic and by reusing existing concepts (severity, verification,
  handoff context compression).

