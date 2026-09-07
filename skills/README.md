# Skills

Operator Framework has one **entry skill** — [`operate/skill.md`](operate/skill.md),
invoked as `/operate` — which inspects the repository, infers the current
OPERATE state, and routes into the workflow skills below. It is a front
door into the lifecycle, not a workflow step.

## Entry skill

| Skill | Purpose |
|---|---|
| [`operate/skill.md`](operate/skill.md) | Inspect the repository, infer the current OPERATE state, and route into the workflow skills below. Invoke `/operate`. |

## Workflow skills

Nine sequential workflow skills operationalize the Operator Framework
methodology (see [`docs/METHODOLOGY.md`](../docs/METHODOLOGY.md) for how
they fit together). Each skill file below states its purpose, inputs,
procedure, outputs, and the human checkpoints it respects.

| Order | Skill | Purpose |
|---|---|---|
| 1 | [`preflight/skill.md`](preflight/skill.md) | Confirm scope, access, and safety before starting |
| 2 | [`resolve/skill.md`](resolve/skill.md) | Turn an ambiguous request into a clear, agreed problem statement |
| 3 | [`write-spec/skill.md`](write-spec/skill.md) | Produce a written specification |
| 4 | [`plan-tickets/skill.md`](plan-tickets/skill.md) | Decompose the spec into small, orderable tickets |
| 5 | [`execute-ticket/skill.md`](execute-ticket/skill.md) | Execute one ticket |
| 6 | [`report/skill.md`](report/skill.md) | Write an execution report |
| 7 | [`verify/skill.md`](verify/skill.md) | Independently verify the work (human gate) |
| 8 | [`handoff/skill.md`](handoff/skill.md) | Persist state for clean pause/resume |
| 9 | [`public-release/skill.md`](public-release/skill.md) | Final scan and sign-off before anything goes public (human gate) |

These skills are model-agnostic — see [`docs/MODEL_ROUTING.md`](../docs/MODEL_ROUTING.md)
for how to choose a model per skill, and [`AGENTS.md`](../AGENTS.md) for how
any AI agent should behave while running them.
