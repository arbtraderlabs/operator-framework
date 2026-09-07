# Operator Framework

```text
   ____                        __
  / __ \____  ___  _________ _/ /_____  _____
 / / / / __ \/ _ \/ ___/ __ `/ __/ __ \/ ___/
/ /_/ / /_/ /  __/ /  / /_/ / /_/ /_/ / /
\____/ .___/\___/_/   \__,_/\__/\____/_/
    /_/

operator-framework
resolve -> spec -> route -> execute -> report -> verify
```

**Version:** v0.1 (initial public release)

> A spec-driven, cost-aware methodology for planning, routing, executing and
> validating work with AI agents.

## The problem

You ask AI to build **X**. It confidently builds **Y**.

Often the failure happens *before* implementation: your intent, vocabulary,
constraints, or assumptions were never made explicit, so the model inferred
its own. Operator Framework moves that failure earlier in the process, where
it is far cheaper to correct.

The framework is **documentation-first**: scope, decisions, and state live in
written artifacts — specs, tickets, a decision ledger, reports — not in a chat
transcript. Conversation is how work gets *done*; documentation is the record
of what was decided and what happened. It is also **model-agnostic**: it works
with *a* capable AI model, or several routed by task, with no dependency on any
specific vendor's API, branding, or tooling.

## How it works

```text
     idea / request
           |
           v
       resolve
           |
           v
        spec
           |
           v
    plan tickets
           |
           v
        route
           |
           v
       execute
           |
           v
        report
           |
           v
        verify
           |
           v
      accepted? -- no --> plan tickets
           |
           | yes
           v
         done
```

A request becomes an agreed problem, a written spec, bounded tickets, a routed
model assignment, executed work, a structured report, and independent
verification. Work that fails verification returns to ticket planning as a
corrective ticket — it is never accepted on the executor's say-so.

## Why it works

- **Resolve first** — align the user's intent with the model before building.
  Ambiguity is cheapest to fix before implementation, not after.
- **Write it down** — vocabulary, ADRs, and specs survive the session, so every
  new model starts from the same agreed context instead of re-deriving it.
- **Bound the work** — small tickets stop agents quietly expanding scope or
  "improving" unrelated areas.
- **Route intelligently** — use strong reasoning where ambiguity and risk
  justify it, and cheaper models for clear bounded execution.
- **Return evidence** — structured reports let a reviewer judge what happened
  without replaying an entire session.
- **Verify independently** — "done" is a claim until an independent check, with
  human sign-off, confirms it against the spec.

## Cost-aware model routing

Routing is an optimization, not a rule: it changes as models, costs, and
capabilities change, and no fixed savings are promised.

> Spend intelligence where intelligence changes the outcome.

```
  AMBIGUOUS / HIGH-RISK WORK
             |
             v
      STRONG REASONING
             |
             v
      SPEC + TICKETS
             |
             v
     BOUNDED EXECUTION
             |
             v
    STRUCTURED REPORT
             |
             v
      STRONG REVIEW
```

Cheaper execution is safe *because* the spec and ticket already fix the
contract. See [`docs/MODEL_ROUTING.md`](docs/MODEL_ROUTING.md) for the full
routing framework.

## Quick start

1. Read [`PRINCIPLES.md`](PRINCIPLES.md) — operating principles, including the
   Influence Note disclosure standard.
2. Read [`AGENTS.md`](AGENTS.md) — how an AI agent should behave inside the
   framework.
3. Read [`docs/METHODOLOGY.md`](docs/METHODOLOGY.md) — the end-to-end flow.
4. Start at [`skills/preflight/skill.md`](skills/preflight/skill.md) and walk
   through the skills in order.
5. Study [`examples/monitoring-dashboard/`](examples/monitoring-dashboard/) to
   see the framework applied to a full (synthetic) project.

## Skills

The short lifecycle above expands into nine sequential skills, each documented
independently in [`skills/`](skills/). `verify` and `public-release` are the
framework's two mandatory human sign-off gates.

| Skill | Purpose |
|---|---|
| `preflight` | Confirm environment, scope and safety |
| `resolve` | Remove ambiguity |
| `write-spec` | Create the implementation contract |
| `plan-tickets` | Break work into bounded units |
| `execute-ticket` | Perform one scoped change |
| `report` | Return structured evidence |
| `verify` | Independently test acceptance |
| `handoff` | Compress context for continuation |
| `public-release` | Apply the final publication gate |

The templates each skill reads and writes live in [`templates/`](templates/).
See [`docs/METHODOLOGY.md`](docs/METHODOLOGY.md) for how they fit together.

## Repository layout

| Path | Purpose |
|---|---|
| [`PRINCIPLES.md`](PRINCIPLES.md) | Core operating principles, including the Influence Note disclosure standard. |
| [`AGENTS.md`](AGENTS.md) | How any AI agent/model should behave when operating inside this framework. |
| [`docs/`](docs/) | Methodology, model routing, domain framing, decision ledger, reporting, ticket system, handoff, and verification guidance. |
| [`docs/adr/`](docs/adr/) | Architecture Decision Records explaining why the framework is built this way. |
| [`skills/`](skills/) | Nine discrete, sequential skills that operationalize the methodology. |
| [`templates/`](templates/) | Reusable templates referenced by the skills and docs. |
| [`tickets/`](tickets/) | Lifecycle directories (`backlog` → `in-progress` → `review` → `done`) for real work using this framework. |
| [`examples/monitoring-dashboard/`](examples/monitoring-dashboard/) | A complete worked example, end to end, using synthetic data only. |

## Handoff is context compression

> Preserve the right context, not every conversation turn.

Long projects accumulate stale context — obsolete plans, superseded decisions,
completed work, old logs. A handoff keeps the small working set that matters:
current state, decisions, active work, blockers, and the exact next step. A
fresh session or model can then continue cheaply and accurately instead of
replaying the whole project. See
[`docs/HANDOFF_PROTOCOL.md`](docs/HANDOFF_PROTOCOL.md).

## Security and privacy

- This repository, its examples, and its templates contain **synthetic data
  only**. No production systems, customer data, credentials, or proprietary
  material from any real project appear here or should ever be added.
- Do not paste real secrets, tokens, internal URLs, or private business
  logic into any ticket, spec, or report created from these templates.
- See [`docs/METHODOLOGY.md#security-and-privacy`](docs/METHODOLOGY.md#security-and-privacy)
  and [`skills/public-release/skill.md`](skills/public-release/skill.md) for the checks
  run before anything derived from this framework is made public.

## Status

v0.1 is a documentation-first release: the methodology, skills, templates,
and one worked example are complete and usable today. Tooling/automation
that enforces this structure programmatically is out of scope for v0.1 and
may follow in later versions.

## License

[MIT](LICENSE)
