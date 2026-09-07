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

**Version:** v0.2 (operational routing + verification contracts)

> A spec-driven, cost-aware methodology for planning, routing, executing and
> validating work with AI agents.

## The problem

You ask AI to build **X**. It confidently builds **Y**.

The failure pattern is consistent:

```text
user thinks X
model understands Y
model executes Y well
result is still wrong
```

The failure happened *before* implementation: your intent, vocabulary,
constraints, and assumptions were never made explicit, so the model inferred
its own. What is clear in your head is not automatically available in the
model's context. Operator Framework makes **resolving ambiguity before
building** the first act of the lifecycle — the ORIENT stage.

The framework is **documentation-first**: scope, decisions, and state live in
written artifacts — specs, tickets, a decision ledger, reports — not in a chat
transcript. Conversation is how work gets *done*; documentation is the record
of what was decided and what happened. It is also **model-agnostic**: it works
with *a* capable AI model, or several routed by task, with no dependency on any
specific vendor's API, branding, or tooling.

A request moves from ambiguity to an agreed problem, a written specification,
bounded execution, structured evidence, and independent verification. Work
that fails verification returns as a corrective ticket — it is never accepted
on the executor's say-so.

Operator Framework standardises that lifecycle through the **OPERATE Method**.

## The OPERATE Method

This lifecycle has a human-facing name: **the OPERATE Method**. OPERATE is
the methodology; the existing skills are the reusable operational steps that
implement it, and they keep their own names. The canonical stages:

```text
O  ORIENT      resolve ambiguity and understand the problem
P  PIN DOWN    vocabulary + decisions + specification
E  ESTABLISH   create bounded tickets and acceptance criteria
R  ROUTE       choose the right model or execution path for the task
A  ACT         execute the scoped work
T  TRACE       return structured evidence and execution state
E  EVALUATE    independently verify the result against the agreed contract
```

Mapped to the plain-English workflow, each OPERATE stage sits above the real
actions that realise it:

```text
┌───────────────┐
│    ORIENT     │
└──────┬────────┘
       │
       ▼
 idea / request
       │
       ▼
resolve ambiguity
       │
       ▼
understand the problem
       │
       ▼
┌───────────────┐
│   PIN DOWN    │
└──────┬────────┘
       │
       ▼
shared vocabulary
       │
       ▼
decisions / ADRs
       │
       ▼
      spec
       │
       ▼
┌───────────────┐
│   ESTABLISH   │
└──────┬────────┘
       │
       ▼
  plan tickets
       │
       ▼
acceptance criteria
       │
       ▼
  bounded scope
       │
       ▼
┌───────────────┐
│     ROUTE     │
└──────┬────────┘
       │
       ▼
choose execution
      path
       │
       ▼
┌───────────────┐
│      ACT      │
└──────┬────────┘
       │
       ▼
    execute
       │
       ▼
┌───────────────┐
│     TRACE     │
└──────┬────────┘
       │
       ▼
structured report
       │
       ▼
    evidence
       │
       ▼
┌───────────────┐
│   EVALUATE    │
└──────┬────────┘
       │
       ▼
     verify
       │
       ▼
   accepted?
     /    \
   yes     no
    |       |
    v       v
   DONE   corrective
           ticket
             |
             v
      ┌───────────────┐
      │   ESTABLISH   │
      └──────┬────────┘
             |
             v
        plan tickets
             |
             v
      ┌───────────────┐
      │     ROUTE     │
      └──────┬────────┘
             |
             v
       execution path
             |
             v
            ACT
```

The corrective loop re-enters at ESTABLISH and runs ROUTE → ACT → TRACE →
EVALUATE again until the work is accepted.

Each stage answers a question:

- **ORIENT** — *"What are we actually trying to do?"* Inspect the problem
  and environment, resolve ambiguity, surface assumptions, identify
  constraints and major unknowns before building (`preflight`, `resolve`).
- **PIN DOWN** — *"What exactly have we agreed?"* Turn the resolved
  understanding into durable artefacts: shared vocabulary, decisions (ADRs
  where appropriate), requirements, scope boundaries, and the specification
  (`DOMAIN.md`, decision ledger, `write-spec`).
- **ESTABLISH** — *"How is the work bounded?"* Break the spec into small
  tickets with acceptance criteria, dependencies, and severity
  (`plan-tickets`, ticket lifecycle).
- **ROUTE** — *"Who or what should perform this already-defined work?"*
  Routing happens *after* the problem is understood and bounded; it is
  execution allocation, weighing how clearly bounded the ticket is,
  technical complexity, severity / blast radius, reversibility,
  security/privacy exposure, cost, remaining uncertainty, and verification
  strength ([`docs/MODEL_ROUTING.md`](docs/MODEL_ROUTING.md)). A route is
  broader than model choice: it covers execution mechanism, context,
  verification, and escalation, and is captured — where non-default — in
  the ticket's **Route** block
  ([`templates/ticket.md`](templates/ticket.md#route)). Doctrine favours
  deterministic tools where correctness can be computed, and treats high
  uncertainty as a planning signal rather than a model upgrade. ROUTE is not
  "resolve ambiguity" — that is ORIENT's job.
- **ACT** — execute the scoped ticket within its boundaries; stop on
  blockers instead of inventing scope (`execute-ticket`).
- **TRACE** — return structured evidence and execution state: files changed,
  validation, evidence, deviations, failed checks, open questions, next
  action. Within OPERATE, TRACE means *execution traceability* — not packet,
  distributed, or telemetry tracing. The report is the portable interface
  between the executor and the reviewer (`report`).
- **EVALUATE** — independently verify the result against the agreed
  contract (`verify`).

Routing contrasts:

| Stage | README-only link change | Core architecture change |
|---|---|---|
| ORIENT | request understood | problem understood |
| PIN DOWN | README only, exact URL, no redesign | architecture / spec agreed |
| ESTABLISH | one bounded ticket | bounded architectural ticket |
| ROUTE | lower-cost execution agent suffices | stronger reasoning model (risk remains high) |

EVALUATE is an independent review model: the implementation agent does not
judge its own work complete. A typical workflow is a lower-cost execution
agent that performs ACT and TRACE (report + evidence), followed by a strong
reasoning reviewer who performs EVALUATE:

```text
evaluate -- pass --> accept
     |
     +-- fail --> corrective ticket -> route -> act -> trace -> evaluate
```

The stronger reviewer is not redoing the implementation; it asks "did the
work actually satisfy what we agreed?" The evaluator may be a stronger
reasoning model, a fresh session, a different capable model, or a human.

Two lifecycle controls sit alongside OPERATE rather than inside the acronym:

- **Handoff** — context compression for pausing and resuming work across
  chats, models, machines, or long gaps.
- **Public release** — the final publication, security, and privacy gate
  before anything becomes public.

## Why it works

- **Resolve first** — align the user's intent with the model before building.
  Ambiguity is cheapest to fix before implementation, not after.
- **Write it down** — vocabulary, ADRs, and specs survive the session, so every
  new model starts from the same agreed context instead of re-deriving it.
- **Bound the work** — small tickets stop agents quietly expanding scope or
  "improving" unrelated areas.
- **Route intelligently** — use strong reasoning where ambiguity and risk
  justify it, and cheaper executors for clear bounded work once the ticket
  fixes the contract.
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

Start or resume a project with the entry skill:

    /operate

It inspects the repository, determines the current OPERATE stage, and
routes into the workflow skills below — it does not restart planning that
is already captured. To understand the framework from scratch instead:

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

The front door is the `/operate` entry skill
([`skills/operate/skill.md`](skills/operate/skill.md)): it inspects the
repository, infers the current state, and routes into the workflow skills
below. The lifecycle expands into nine sequential workflow skills, each
documented independently in [`skills/`](skills/). `verify` and
`public-release` are the framework's two mandatory human sign-off gates.

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
| [`skills/`](skills/) | The `/operate` entry skill plus nine sequential workflow skills that operationalize the methodology. |
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

v0.2 is a documentation-and-contracts release building on v0.1: ROUTE now
covers execution mechanism, context, verification, and escalation, and
tickets may carry non-default **Route** overrides so verification can be
planned before execution. The methodology, skills, templates, and one
worked example remain complete and usable today; programmatic enforcement
remains out of scope.

## License

[MIT](LICENSE)
