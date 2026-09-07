# Model Routing

Operator Framework is model-agnostic: it does not require a specific AI
vendor or model. This document is the home of **ROUTE** doctrine — deciding
who or what executes already-defined work. The file keeps its v0.1 name,
*Model Routing*, but a route is broader than model choice: it also covers
execution mechanism, the context the executor receives, the verification
method, and the conditions under which execution must stop. Model choice is
one dimension of a route, not the whole of it (see
[`adr/ADR-0005-routing-as-execution-allocation.md`](adr/ADR-0005-routing-as-execution-allocation.md)).

## What a route decides

ROUTE happens *after* work is understood and bounded (see
[`README.md`](../README.md#the-operate-method)). Routing is execution
allocation, not ambiguity resolution — that is ORIENT's job. Where it
matters, a route determines:

1. **Reasoning requirement** — how much judgment the work genuinely needs.
2. **Execution mechanism** — which class of executor (see
   [the hierarchy below](#execution-mechanism-hierarchy-and-deterministic-first)).
3. **Context requirement** — the minimum context the executor must receive
   ([context least privilege](#context-least-privilege)).
4. **Tool permissions / expectations** — what the executor may or should use.
5. **Verification method** — how success will be demonstrated.
6. **Escalation conditions** — when execution must stop rather than improvise.

A route is written onto the ticket where non-default (the ticket's **Route**
block, see [`templates/ticket.md`](../templates/ticket.md)) during
[`plan-tickets`](../skills/plan-tickets/skill.md), and honoured at execution
time by [`execute-ticket`](../skills/execute-ticket/skill.md). Routing stays
an optimization, not a required ceremony: a single general-purpose model can
perform every skill, and a ticket that omits its Route block simply falls
back to the defaults in this document.

## Route by task shape

Different skills stress different capabilities. Route by **task shape**, not
by brand loyalty or habit:

| Capability | Skills that need it most |
|---|---|
| Ambiguity resolution, clarifying questions | [`resolve`](../skills/resolve/skill.md) |
| Long-form structured writing | [`write-spec`](../skills/write-spec/skill.md), [`report`](../skills/report/skill.md) |
| Decomposition and dependency reasoning | [`plan-tickets`](../skills/plan-tickets/skill.md) |
| Mechanical, well-scoped execution | [`execute-ticket`](../skills/execute-ticket/skill.md) |
| Independent, skeptical review | [`verify`](../skills/verify/skill.md) |
| Careful policy/compliance checking | [`public-release`](../skills/public-release/skill.md) |

## Execution-mechanism hierarchy and deterministic-first

Use deterministic systems where correctness can be computed; spend
intelligence only where judgment changes the outcome. The broad routing
hierarchy favours:

```
deterministic tool
      ↓ if insufficient
bounded inexpensive execution
      ↓ if insufficient
stronger reasoning / execution
```

Execution-mechanism classes, roughly in rising cost:

| Class | When it fits |
|---|---|
| Deterministic tool | Correctness can be computed: comparison, validation, search, lint, type check, test run |
| Local / batch worker | A bounded transformation a script or local process does more cheaply and repeatably than a model |
| Inexpensive worker | Well-specified bounded work needing a little judgment |
| Coding agent | Bounded implementation inside a repository/toolchain |
| Capable general model | Moderate judgment, integration, or unfamiliar-but-bounded code |
| Strong reasoning model | Genuinely hard reasoning, architecture, or novel debugging |
| Human gate | Consequential sign-off — the framework's `verify` and `public-release` gates are mandatory human checks |

Do not use an LLM for work a deterministic tool performs more cheaply,
reliably, and repeatably:

| Task | Deterministic tool |
|---|---|
| Repository string lookup | `grep` / `ripgrep` |
| Structural search | repository search tooling |
| Dataset equality | comparator |
| JSON validity | parser / schema validator |
| Test correctness | test suite |
| Lint rules | linter |
| Type correctness | type checker |
| Repetitive transformation | script where appropriate |
| Architectural ambiguity | reasoning model / human |
| Novel debugging | capable reasoning model |

Risk, verification strength, and complexity influence how far up the
hierarchy a route needs to go — cheap is only safe when the lower rung
really is sufficient.

## Verification strength and risk influence the route

Strong verification can safely reduce the intelligence required during
execution: the more precisely success can be demonstrated, the cheaper the
executor that may safely perform the work. The table below is guidance, not
a decision procedure:

| Uncertainty | Blast radius | Verification | Likely route |
|---|---|---|---|
| Low | Low | Strong | Deterministic tool / cheapest reliable worker |
| Low | Medium | Strong | Bounded worker / coding agent |
| Medium | Low | Strong | Capable general model |
| Medium | Medium | Strong–Medium | Strong reasoning model |
| High | Any | Any | Return to ORIENT / PIN DOWN / ESTABLISH (see below) |
| Any | High | Weak | Stronger executor **plus** stronger review, or a human gate |

Blast radius and severity are defined in
[`TICKET_SYSTEM.md#severity`](TICKET_SYSTEM.md#severity). The important
consequence: where a ticket records a concrete verification method (see
[`templates/ticket.md`](../templates/ticket.md)), a cheaper executor becomes
safe because the verifier — not the executor — is the final judge.

## High uncertainty is a planning signal, not a model upgrade

```
HIGH UNCERTAINTY
      ↓
do not automatically buy a smarter executor
      ↓
return to ORIENT / PIN DOWN / ESTABLISH
```

A more capable model cannot reliably compensate for a missing decision, a
contradictory requirement, or an undefined acceptance condition. More
intelligence is not a replacement for specification. When execution
reveals high uncertainty, the route back to planning is the correct move —
not an upgrade in model price.

## Blockers and escalation

Execution workers must not silently improvise outside the ticket's
contract. When a worker stops, classify the blocker so the response is
proportional ([`execute-ticket`](../skills/execute-ticket/skill.md) carries
the full stop-condition list):

1. **Specification blocker** — requirements ambiguous, instructions
   contradictory, an edge case undecided, required architecture absent,
   acceptance criteria unclear, or scope undefined. Response: return the
   work to PIN DOWN / ESTABLISH, improve the durable specification, then
   re-route. This is an upstream planning problem, not an executor problem.
2. **Execution capability blocker** — the specification is clear but the
   current executor lacks the capability to do this section safely. Response:
   bounded local escalation to a stronger executor for the specific hard
   section, then return the remaining work to normal routing.
3. **Reality / discovery blocker** — the plan was reasonable but execution
   revealed new facts (undocumented behaviour, unexpected data, dependency
   incompatibility, corrupted state). Response: investigate, update the
   durable truth (ADR / spec / ticket / decision ledger) as required, then
   re-route. New information is part of engineering, not automatically
   evidence of poor planning.

**Escalate the blocker, not automatically the whole workload.** One hard
ticket must not move an entire project to an expensive model:

```
TCK-001…003 → low-cost executor
TCK-004     → genuine concurrency blocker
                  ↓
              escalate only that problem
                  ↓
              update durable truth
                  ↓
TCK-005     → return to normal low-cost routing
```

## Context least privilege

Give an executor exactly the context necessary to perform its bounded task —
planning should *reduce* execution context, not increase it. This extends the
same reasoning already used for
[`HANDOFF_PROTOCOL.md`](HANDOFF_PROTOCOL.md) (preserve the right context,
not every conversation turn) to the start of execution.

A well-prepared execution package typically contains only: the ticket, the
relevant specification section, the relevant ADR(s)/decisions, the
files/modules in scope, constraints, acceptance criteria, verification
instructions, and escalation/stop conditions. Avoid automatically including
every ADR, whole project history, old transcripts, unrelated documentation,
or archived reports. A ticket's **Context required** field (see
[`templates/ticket.md`](../templates/ticket.md)) records this explicitly when
it is non-obvious.

## Cost: the cheapest reliable path to verified completion

Routing is an optimization, not a rule, and no fixed savings are promised.
The economic principle is not "always use the cheapest model" — it is
**use the cheapest reliable path to verified completion**. Total execution
cost includes more than token price; consider, where relevant:

```
model/API cost          retries               failed attempts
supervision             rework                verification effort
elapsed time            blast radius          cost of incorrect implementation
```

A worker costing £0.10 that needs six attempts may be worse than a £0.40
worker that completes the task correctly once. Routing weighs expected total
cost, reliability, and risk. Whether cheaper routing actually worked can
only be answered where reports happen to record the route and evidence
actually used; v0.2 adds no mandatory telemetry for this — Operate should
be measurable where evidence is available, never faked where it is not.

## What this framework does not do

- It does not name or endorse specific models or vendors.
- It does not assume you have access to more than one model — every skill
  is usable with a single general-purpose model if that's all you have.
  Routing is an optimization, not a requirement.
- It does not build routing infrastructure: no model orchestration, API
  proxies, token-billing integration, or autonomous executor daemons.
  v0.2 makes the method and contracts correct; executable enforcement can
  follow once the methodology is validated manually.
- It does not store model API keys, configuration, or credentials anywhere
  in this repository. See [`README.md#security-and-privacy`](../README.md#security-and-privacy).

## Recording a routing decision

Routing choices are logged at two levels:

1. **Per ticket** — the ticket's **Route** block records the execution
   profile, verification method, context required, and escalation
   conditions when they differ from the defaults above. This is written at
   `plan-tickets` time so verification exists before execution where
   practical.
2. **Per project** — if a project deliberately routes specific skills to
   specific model classes (e.g. "always verify with a stronger reviewer"),
   record that choice in the project decision ledger using
   [`templates/decision.md`](../templates/decision.md) so future
   contributors understand why, and can revisit it as models change.
