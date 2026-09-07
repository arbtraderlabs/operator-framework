# Skills

Nine sequential skills operationalize the Operator Framework methodology
(see [`docs/methodology.md`](../docs/methodology.md) for how they fit
together). Each skill file below states its purpose, inputs, procedure,
outputs, and the human checkpoints it respects.

| Order | Skill | Purpose |
|---|---|---|
| 1 | [`preflight.md`](preflight.md) | Confirm scope, access, and safety before starting |
| 2 | [`resolve.md`](resolve.md) | Turn an ambiguous request into a clear, agreed problem statement |
| 3 | [`write-spec.md`](write-spec.md) | Produce a written specification |
| 4 | [`plan-tickets.md`](plan-tickets.md) | Decompose the spec into small, orderable tickets |
| 5 | [`execute-ticket.md`](execute-ticket.md) | Execute one ticket |
| 6 | [`report.md`](report.md) | Write an execution report |
| 7 | [`verify.md`](verify.md) | Independently verify the work (human gate) |
| 8 | [`handoff.md`](handoff.md) | Persist state for clean pause/resume |
| 9 | [`public-release.md`](public-release.md) | Final scan and sign-off before anything goes public (human gate) |

These skills are model-agnostic — see [`docs/model-routing.md`](../docs/model-routing.md)
for how to choose a model per skill, and [`AGENTS.md`](../AGENTS.md) for how
any AI agent should behave while running them.
