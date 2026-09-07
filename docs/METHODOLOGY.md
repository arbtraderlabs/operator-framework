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

## Model routing

Different skills have different model needs (for example, `resolve` benefits
from strong reasoning and clarifying-question ability; `execute-ticket` may
be well suited to a faster/cheaper model for mechanical steps). This
framework does not mandate a specific model per skill. See
[`docs/MODEL_ROUTING.md`](MODEL_ROUTING.md) for a routing framework you can
apply with whatever models you have available.

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
