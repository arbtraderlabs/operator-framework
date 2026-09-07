# Skill: write-spec

**Order:** 3 of 9
**Purpose:** Produce a written specification of the solution from the
domain brief, precise enough to be decomposed into tickets without
re-deriving the approach each time.

## When to use

After [`skills/resolve.md`](resolve.md) has produced an agreed domain
brief.

## Inputs

- The domain brief (see [`docs/domain.md`](../docs/domain.md)).
- Any relevant prior decision ledger entries.

## Procedure

1. **Restate goals and non-goals** from the domain brief in solution terms
   — what will and won't be built/changed.
2. **Write numbered, testable requirements.** Each one should be checkable
   later during [`skills/verify.md`](verify.md) — avoid requirements that
   can't be confirmed objectively.
3. **Describe the design** at the level of detail
   [`skills/plan-tickets.md`](plan-tickets.md) needs to decompose it —
   components, data shapes, flows. Use synthetic examples only.
4. **Call out risks and open questions** rather than silently resolving
   them with an unstated assumption.
5. **Log material design decisions** in the decision ledger using
   [`templates/decision-ledger-entry.md`](../templates/decision-ledger-entry.md) —
   especially anywhere you chose one approach over a plausible alternative.
6. **Include the Influence Note** verbatim (see
   [`PRINCIPLES.md`](../PRINCIPLES.md#7-disclosure-over-ambiguity--the-influence-note)).

## Outputs

- A specification document using [`templates/spec.md`](../templates/spec.md)
  (see [`examples/monitoring-dashboard/SPEC.md`](../examples/monitoring-dashboard/SPEC.md)
  for a worked example).
- Decision ledger entries for material design choices.

## Checkpoint

Have the spec reviewed (by a human, or a different model pass) before
moving to `plan-tickets` if the domain brief indicated any significant
ambiguity or risk.

## Next skill

[`skills/plan-tickets.md`](plan-tickets.md)
