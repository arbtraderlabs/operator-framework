# Specification Template

Copy this file to `SPEC.md` (or a per-feature spec file) at the root of the
project being specified. Produced by
[`skills/write-spec/skill.md`](../skills/write-spec/skill.md) from the domain brief
(see [`docs/DOMAIN.md`](../docs/DOMAIN.md)).

The spec is the implementation contract: it fixes intended behaviour before
execution so tickets, execution, and verification all work against the same
agreed definition — and so later model sessions implement what was agreed
rather than silently extending or reinterpreting it. Make it detailed enough
to constrain execution, but no more detailed than necessary.

---

# Specification: <Project/Feature Name>

**Status:** draft | approved | superseded
**Domain reference:** <relative link to DOMAIN.md or domain brief section>

## Summary

One paragraph: what this specifies and why, in plain language.

## Goals

- <Goal 1>
- <Goal 2>

## Non-goals

Explicitly out of scope for this spec — as important as the goals section.

- <Non-goal 1>

## Requirements

Numbered, specific, and each one testable. Group by area if useful.

1. <Requirement>
2. <Requirement>

## Design overview

Enough detail that [`skills/plan-tickets/skill.md`](../skills/plan-tickets/skill.md) can
decompose this into tickets without re-deriving the approach. Diagrams,
data shapes, and flows as needed — synthetic examples only.

## Risks and open questions

- <Risk or question, and how it will be resolved or who owns it>

## Influence Note

> **Influence Note:** This artifact was produced under AI model assistance
> within the Operator Framework. It contains synthetic data only, reflects no
> proprietary or private project material, and remains subject to human
> review before execution or release.
