# Model Routing

Operator Framework is model-agnostic: it does not require a specific AI
vendor or model. This document describes how to choose a model for a given
skill without coupling the methodology itself to that choice.

## Principle

Route by **task shape**, not by brand loyalty or habit. Different skills
stress different capabilities:

| Capability | Skills that need it most |
|---|---|
| Ambiguity resolution, clarifying questions | [`resolve`](../skills/resolve/skill.md) |
| Long-form structured writing | [`write-spec`](../skills/write-spec/skill.md), [`report`](../skills/report/skill.md) |
| Decomposition and dependency reasoning | [`plan-tickets`](../skills/plan-tickets/skill.md) |
| Mechanical, well-scoped execution | [`execute-ticket`](../skills/execute-ticket/skill.md) |
| Independent, skeptical review | [`verify`](../skills/verify/skill.md) |
| Careful policy/compliance checking | [`public-release`](../skills/public-release/skill.md) |

## A simple routing framework

1. **Classify the task**: reasoning-heavy (ambiguous, high-stakes,
   multi-step) vs. mechanical (well-specified, repetitive, low ambiguity).
2. **Match capability to cost**: use a higher-capability model where
   ambiguity or stakes are high (`resolve`, `verify`, `public-release`); a
   faster/cheaper model is often sufficient for well-scoped
   `execute-ticket` work once the spec and ticket are precise.
3. **Keep verification independent**: where practical, don't let the same
   model instance that executed a ticket also be the sole verifier of it.
   A different model, a fresh context, or a human reviewer reduces the risk
   of the verifier inheriting the executor's blind spots.
4. **Re-evaluate per project, not once globally**: model capabilities and
   costs change quickly; treat routing choices as a living decision, logged
   like any other (see [`docs/DECISION_LEDGER.md`](DECISION_LEDGER.md)),
   not a permanent architectural commitment.

## What this framework does not do

- It does not name or endorse specific models or vendors.
- It does not assume you have access to more than one model — every skill
  is usable with a single general-purpose model if that's all you have.
  Routing is an optimization, not a requirement.
- It does not store model API keys, configuration, or credentials anywhere
  in this repository. See [`README.md#security-and-privacy`](../README.md#security-and-privacy).

## Recording a routing decision

If a project deliberately routes specific skills to specific model classes,
record that choice in the decision ledger using
[`templates/decision.md`](../templates/decision.md)
so future contributors understand why, and can revisit it as models change.
