# Skills

Nine sequential skills operationalize the Operator Framework methodology
(see [`docs/METHODOLOGY.md`](../docs/METHODOLOGY.md) for how they fit
together). Each skill file below states its purpose, inputs, procedure,
outputs, and the human checkpoints it respects.

| Order | Skill | Purpose |
|---|---|---|
| 1 | [`preflight.md`](preflight/skill.md) | Confirm scope, access, and safety before starting |
| 2 | [`resolve.md`](resolve/skill.md) | Turn an ambiguous request into a clear, agreed problem statement |
| 3 | [`write-spec.md`](write-spec/skill.md) | Produce a written specification |
| 4 | [`plan-tickets.md`](plan-tickets/skill.md) | Decompose the spec into small, orderable tickets |
| 5 | [`execute-ticket.md`](execute-ticket/skill.md) | Execute one ticket |
| 6 | [`report.md`](report/skill.md) | Write an execution report |
| 7 | [`verify.md`](verify/skill.md) | Independently verify the work (human gate) |
| 8 | [`handoff.md`](handoff/skill.md) | Persist state for clean pause/resume |
| 9 | [`public-release.md`](public-release/skill.md) | Final scan and sign-off before anything goes public (human gate) |

These skills are model-agnostic — see [`docs/MODEL_ROUTING.md`](../docs/MODEL_ROUTING.md)
for how to choose a model per skill, and [`AGENTS.md`](../AGENTS.md) for how
any AI agent should behave while running them.
