# Methodology

This document describes the end-to-end flow of Operator Framework: how a
request becomes verified, reported work. It is the map; each
[`skills/`](../skills/) file is the detailed procedure for one step.

## The flow

```
request
  │
  ▼
preflight        (skills/preflight/skill.md)   — confirm scope, access, safety before doing anything
  │
  ▼
resolve          (skills/resolve/skill.md)     — turn an ambiguous ask into a clear, agreed problem statement
  │
  ▼
write-spec       (skills/write-spec/skill.md)  — produce a written specification of the solution
  │
  ▼
plan-tickets     (skills/plan-tickets/skill.md)— decompose the spec into small, orderable tickets
  │
  ▼
execute-ticket   (skills/execute-ticket/skill.md) — do the work for one ticket at a time
  │
  ▼
report           (skills/report/skill.md)      — summarize what was executed, against the ticket/spec
  │
  ▼
verify           (skills/verify/skill.md)      — independent check that the work meets the spec (human gate)
  │
  ▼
handoff          (skills/handoff/skill.md)     — persist state so work can pause/resume cleanly
  │
  ▼
public-release   (skills/public-release/skill.md) — final scan and sign-off before anything goes public
```

`execute-ticket` → `report` → `verify` repeats per ticket until the ticket
backlog for the spec is empty (see [`docs/TICKET_SYSTEM.md`](TICKET_SYSTEM.md)).
`handoff` can occur at any point work pauses, not only at the end.

The written spec is what makes this sequence more than a chat session: it is
the implementation contract that tickets are planned from and verification
checks against. It fixes intended behaviour before execution so later
sessions — including cheaper execution models — implement what was agreed
rather than re-deriving or silently extending it. Keep specs detailed enough
to constrain execution, and no more detailed than necessary.

## Core artifacts

| Artifact | Produced by | Template |
|---|---|---|
| Domain brief | `resolve` | referenced in [`docs/DOMAIN.md`](DOMAIN.md) |
| Specification | `write-spec` | [`templates/spec.md`](../templates/spec.md) |
| Tickets | `plan-tickets` | [`templates/ticket.md`](../templates/ticket.md) |
| Decision ledger entries | any skill, as decisions are made | [`templates/decision.md`](../templates/decision.md) |
| Execution report | `report` | [`templates/execution-report.md`](../templates/execution-report.md) |
| Verification report | `verify` | [`templates/verification-report.md`](../templates/verification-report.md) |
| Handoff note | `handoff` | [`templates/handoff.md`](../templates/handoff.md) |

## Routing (ROUTE)

ROUTE is the execution-allocation decision for already-defined work. There
is no dedicated `route` skill — routing is an optimization, not a required
stage ceremony, and [`docs/MODEL_ROUTING.md`](MODEL_ROUTING.md) owns the
routing doctrine. In practice:

- `plan-tickets` records non-default **Route** overrides on a ticket
  (execution profile, verification method, context, escalation) so
  verification can exist before execution;
- `execute-ticket` honours those overrides, prefers deterministic tooling
  where sufficient, and classifies blockers instead of improvising;
- different skills have different model needs, but the framework never
  mandates a specific model per skill.

See [`docs/MODEL_ROUTING.md`](MODEL_ROUTING.md) for the full routing
framework.

## Security and privacy

- Treat every artifact as potentially public until `public-release` says
  otherwise. Do not put real secrets, customer data, or proprietary logic
  into a spec, ticket, or report "temporarily" — it tends to stay.
- Domain briefs and specs should describe systems abstractly enough that
  they teach the pattern without exposing a real, private implementation.
- If you must reference real infrastructure while resolving a real problem,
  keep that material outside this repository and outside anything intended
  for `public-release`; only the synthetic, generalized version belongs here.
- See [`skills/public-release/skill.md`](../skills/public-release/skill.md) for the
  explicit pre-publish scan.

## When to deviate

The sequence above is the default, not a straitjacket. Trivial, low-risk
tickets may reasonably compress `resolve` and `write-spec` into a short
paragraph inside the ticket itself — but the decision to compress should
itself be logged in the decision ledger, not silently assumed.
