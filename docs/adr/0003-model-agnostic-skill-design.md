# ADR-0003: Model-Agnostic Skill Design

**Status:** Accepted

## Context

AI model capabilities, pricing, and vendors change quickly. A methodology
that names or depends on a specific model or provider would need constant
rewriting and would lock adopters into a particular vendor relationship,
which is not the goal of a general operating framework.

## Decision

Every skill in [`skills/`](../../skills/) is written in terms of inputs,
outputs, and procedure — never in terms of a specific model, vendor API, or
product feature. Guidance on *choosing* a model for a given skill is kept
separate, in [`docs/model-routing.md`](../model-routing.md), and is
explicitly framed as optional optimization rather than a requirement. The
framework must remain fully usable with a single, unnamed, general-purpose
model.

## Consequences

- **Positive:** The framework doesn't need to be rewritten as models and
  vendors change; only [`docs/model-routing.md`](../model-routing.md)
  guidance might evolve.
- **Positive:** Teams using different models, or mixing several, can adopt
  the same methodology without translation.
- **Negative:** Skill descriptions are necessarily more abstract than a
  vendor-specific tutorial would be, which requires readers to translate
  procedure into concrete prompts/tool calls themselves.
- **Negative:** Some genuinely model-specific capabilities (e.g. a
  particular tool-calling feature) may need per-adopter adaptation that this
  framework does not prescribe; this is treated as intentionally out of
  scope for v0.1.
