# Domain Framing

Before writing a specification, a project needs a **domain brief**: a short,
plain-language description of the problem space, the people/systems
involved, and the constraints that matter. This document explains what a
domain brief is for and what it should contain. It is produced by
[`skills/resolve/skill.md`](../skills/resolve/skill.md) and consumed by
[`skills/write-spec/skill.md`](../skills/write-spec/skill.md).

## Why a separate domain step

Jumping straight from a request to a specification tends to bake in
unstated assumptions about the domain — who the users are, what "correct"
means, what already exists. A short domain brief surfaces those assumptions
explicitly, before they get expensive to unwind.

## What belongs in a domain brief

1. **Problem in one paragraph** — plain language, no solution talk yet.
2. **Actors** — who or what interacts with this system (people, services,
   schedules). Use roles, not real names or org-specific identifiers.
3. **Constraints** — technical, time, budget, compliance, or organizational
   constraints that shape the solution space.
4. **Out of scope** — explicitly state what this effort will *not* cover, to
   prevent silent scope creep later.
5. **Success signal** — how you'll know, in domain terms (not implementation
   terms), that the problem is solved.
6. **Open questions** — anything still unresolved, to be closed out during
   `resolve` before `write-spec` begins.

## Example

See [`examples/monitoring-dashboard/DOMAIN.md`](../examples/monitoring-dashboard/DOMAIN.md)
for a complete, synthetic worked example of a domain brief.

## Security and privacy note

A domain brief should describe the *shape* of a problem, not expose the real
private system it may be modeled on. Use generic role names (e.g. "on-call
engineer", "billing service") and invented, synthetic identifiers rather
than real team, product, or customer names. See
[`docs/METHODOLOGY.md#security-and-privacy`](METHODOLOGY.md#security-and-privacy).

## Relationship to other artifacts

```
domain brief (this doc's output)
   → specification (docs handled in docs/METHODOLOGY.md, template in templates/spec.md)
      → tickets (docs/TICKET_SYSTEM.md, template in templates/ticket.md)
```
