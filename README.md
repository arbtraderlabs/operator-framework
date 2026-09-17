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

**Version:** v0.3.0 (environment awareness + existing-project adoption)

> A spec-driven, cost-aware methodology for keeping AI-assisted work on course from intent to verified product delivery.

## The goal

The goal of Operator is not to make a project follow a process for the sake of process.

The goal is to deliver the **right product**, safely, with enough evidence that the work is actually complete and another human or model can understand the resulting state.

Operator should take the simplest safe path to verified delivery. Add ceremony only where it materially improves correctness, recoverability, clarity, safety, or reviewability.

```text
IDEA
  |
  v
understand -> define -> bound -> route -> build -> trace -> verify
                                                    |
                                                    v
                                             PRODUCT DELIVERED
```

If the road ahead is clear, keep moving. If something looks inconsistent, surface it. If there is a high-confidence consequential mismatch, stop before causing damage.

## The problem

You ask AI to build **X**. It confidently builds **Y**.

The failure pattern is consistent:

```text
user thinks X
model understands Y
model executes Y well
result is still wrong
```

The failure happened *before* implementation: intent, vocabulary, constraints, environment, and assumptions were never made explicit, so the model inferred its own.

Operator Framework makes **resolving ambiguity before building** the first act of the lifecycle and keeps the work aligned through execution, evidence, and verification.

The framework is **documentation-first**: scope, decisions, environment boundaries, and state live in durable artifacts rather than only in a chat transcript. Conversation is how work gets done; documentation is the record of what was decided and what happened.

It is also **model-agnostic**. The method works with one capable AI model, several models routed by task, deterministic tools, coding agents, or human execution.

## The OPERATE Method

OPERATE is the delivery lifecycle. The reusable skills implement it without coupling the method to a specific model or vendor.

```text
O  ORIENT      resolve ambiguity and understand the problem
P  PIN DOWN    vocabulary + decisions + specification
E  ESTABLISH   create bounded tickets and acceptance criteria
R  ROUTE       choose the right execution path
A  ACT         execute the scoped work
T  TRACE       return structured evidence and execution state
E  EVALUATE    independently verify the result against the agreed contract
```

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
understand problem + environment
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
choose execution path
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
structured report + evidence
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
   DONE   corrective ticket
             |
             v
          ESTABLISH
```

The corrective loop re-enters at ESTABLISH and runs ROUTE → ACT → TRACE → EVALUATE again until the work is accepted.

Each stage answers a question:

- **ORIENT** — *What are we actually trying to do?* Inspect the problem and environment, resolve ambiguity, surface assumptions, constraints and major unknowns (`preflight`, `resolve`).
- **PIN DOWN** — *What exactly have we agreed?* Turn the resolved understanding into durable artifacts: vocabulary, decisions, requirements, scope boundaries and specification.
- **ESTABLISH** — *How is the work bounded?* Break the spec into small tickets with acceptance criteria, dependencies and severity.
- **ROUTE** — *Who or what should perform this already-defined work?* Choose the execution mechanism, context, verification approach and escalation conditions.
- **ACT** — execute the scoped ticket within its boundaries.
- **TRACE** — return structured evidence: files changed, validation, deviations, failures, open questions and next state.
- **EVALUATE** — independently verify the result against the agreed contract.

## v0.3: environment awareness without unnecessary friction

A safe project does not need a dedicated DEV, SIM, STAGING and PROD stack simply because a framework says so.

It does need to know **where experimentation is safe** and what environments or repositories are consequential.

Operator distinguishes between:

- **repository/workspace responsibility** — what a repo or workspace is for, such as development, generated production output, public marketing or infrastructure;
- **runtime environment** — where software actually runs, such as local, DEV, SIM, staging or PROD.

See [`docs/ENVIRONMENT_GUARDRAILS.md`](docs/ENVIRONMENT_GUARDRAILS.md) and [`templates/environment-contract.md`](templates/environment-contract.md).

Environment awareness follows a proportional response:

```text
OBSERVE
   |
   v
COMPARE EXPECTED vs OBSERVED
   |
   v
DOES IT SMELL RIGHT?
   |
   +-- normal / low consequence ------> continue
   |
   +-- inconsistent / uncertain ------> flag + recommend a check
   |
   +-- clear high-consequence mismatch -> stop
```

This is intentionally **not** a blanket blocking system.

Examples:

- Work performed in SIM and output also targets SIM: continue.
- Tests pass in SIM but release output unexpectedly points at PROD: flag the inconsistency before promotion.
- A destructive operation targets PROD while the ticket explicitly targets SIM: stop.

The principle is simple:

> Guardrails should increase awareness before they increase friction.

## v0.3: adopting Operator into existing projects

Operator is not only for greenfield work.

If a team discovers the framework after a project is already mature, `/operate` can route to the supporting [`adopt`](skills/adopt/skill.md) skill.

The assessment maps existing practice onto OPERATE instead of forcing a rewrite.

It classifies each relevant area as:

- **Established** — the project already has a durable equivalent;
- **Partial** — the behaviour exists but is incomplete, implicit or inconsistent;
- **Missing** — a useful control or artifact is absent;
- **Not needed yet** — adding it now would create more ceremony than value.

The result should preserve what already works and recommend the **smallest useful migration path**.

Real projects can also expose reusable lessons for Operator itself. An adoption assessment may identify a framework feedback candidate and suggest an issue or pull request, but it does not silently modify Operator or publish project-specific material.

## Why it works

- **Resolve first** — align intent before building.
- **Write down durable truth** — important decisions and state survive the session.
- **Bound the work** — small tickets stop quiet scope expansion.
- **Route intelligently** — use the cheapest reliable execution path to verified completion.
- **Keep environment awareness proportional** — continue when things line up, flag suspicious mismatches, stop only for clear consequential risk.
- **Return evidence** — reviewers can judge what happened without replaying the entire session.
- **Verify independently** — "done" remains a claim until checked against the agreed contract.
- **Preserve existing good practice** — adoption improves mature projects instead of forcing them to start again.

## Cost-aware model routing

Routing is an optimization, not a rule. It changes as models, costs and capabilities change, and no fixed savings are promised.

> Spend intelligence where intelligence changes the outcome.

```text
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

Cheaper execution is safe when the work is well bounded and success can be verified. See [`docs/MODEL_ROUTING.md`](docs/MODEL_ROUTING.md).

## Quick start

Start or resume a project with:

    /operate

`/operate` inspects the repository, determines the current OPERATE state and routes to the appropriate workflow. It does not restart planning already captured in durable artifacts.

For an established project, it may recommend an adoption assessment rather than rebuilding the process from scratch.

To understand the framework from scratch:

1. Read [`PRINCIPLES.md`](PRINCIPLES.md).
2. Read [`AGENTS.md`](AGENTS.md).
3. Read [`docs/METHODOLOGY.md`](docs/METHODOLOGY.md).
4. Read [`docs/ENVIRONMENT_GUARDRAILS.md`](docs/ENVIRONMENT_GUARDRAILS.md).
5. Start at [`skills/preflight/skill.md`](skills/preflight/skill.md) and walk through the lifecycle as deeply as the project needs.
6. Study [`examples/monitoring-dashboard/`](examples/monitoring-dashboard/) for a complete synthetic example.

## Skills

The front door is [`skills/operate/skill.md`](skills/operate/skill.md). It inspects state and delegates into the lifecycle rather than adding another stage.

| Skill | Purpose |
|---|---|
| `operate` | State-aware front door and routing entry point |
| `preflight` | Confirm environment, scope, access and safety |
| `resolve` | Remove ambiguity |
| `write-spec` | Create the implementation contract |
| `plan-tickets` | Break work into bounded units |
| `execute-ticket` | Perform one scoped change |
| `report` | Return structured evidence |
| `verify` | Independently test acceptance |
| `handoff` | Compress context for continuation |
| `public-release` | Apply the final publication gate |
| `adopt` | Assess an existing project and map it onto OPERATE without unnecessary churn |

`adopt` is a supporting skill rather than an extra OPERATE stage.

## Repository layout

| Path | Purpose |
|---|---|
| [`VERSION`](VERSION) | Current framework version. |
| [`CHANGELOG.md`](CHANGELOG.md) | Versioned framework evolution. |
| [`PRINCIPLES.md`](PRINCIPLES.md) | Core operating principles. |
| [`AGENTS.md`](AGENTS.md) | Behaviour expected from an AI agent/model using the framework. |
| [`docs/`](docs/) | Methodology, environment guardrails, model routing, domain framing, decision ledger, reporting, ticket system, handoff and verification guidance. |
| [`docs/adr/`](docs/adr/) | Architecture Decision Records explaining significant framework choices. |
| [`skills/`](skills/) | `/operate`, supporting skills and lifecycle skills. |
| [`templates/`](templates/) | Reusable project artifacts including environment and adoption contracts. |
| [`tickets/`](tickets/) | Lifecycle directories (`backlog` → `in-progress` → `review` → `done`). |
| [`examples/monitoring-dashboard/`](examples/monitoring-dashboard/) | Complete worked synthetic example. |

## Handoff is context compression

> Preserve the right context, not every conversation turn.

Long projects accumulate stale context: obsolete plans, superseded decisions, completed work and old logs. A handoff keeps the small working set that matters — current state, decisions, active work, blockers and the exact next step.

See [`docs/HANDOFF_PROTOCOL.md`](docs/HANDOFF_PROTOCOL.md).

## Security and privacy

- This repository, its examples and templates contain **synthetic data only**.
- No production systems, customer data, credentials or proprietary material from a real project should be copied into the public framework repository.
- Do not put real secrets, tokens, internal URLs or private business logic into public framework artifacts.
- Real projects may use the method against private operational context; generalize any lesson before proposing it back to Operator.
- See [`skills/public-release/skill.md`](skills/public-release/skill.md) for the explicit publication gate.

## Status

v0.3 extends the v0.2 routing and verification foundation with two practical capabilities learned from applying Operator to real project structures:

1. **Environment and repository responsibility awareness** — identify where experimentation is safe, detect mismatches and respond proportionally rather than adding blanket gates.
2. **Existing-project adoption** — assess what a mature project already does well, identify evidence-backed gaps and migrate only what adds value.

The framework remains documentation-and-contract driven. Programmatic enforcement is intentionally out of scope until the methodology has earned it through repeated real-world use.

## License

[MIT](LICENSE)
