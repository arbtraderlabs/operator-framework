# Skill: resolve

**Order:** 2 of 9
**Purpose:** Turn an ambiguous or underspecified request into a clear,
agreed problem statement — a domain brief — before any solution is
proposed.

## When to use

After [`skills/preflight.md`](preflight.md), whenever the request is
ambiguous, open-ended, or could reasonably be interpreted several ways.

## Inputs

- The request, plus preflight's notes on scope/access/safety.
- Any existing domain material for the project.

## Procedure

1. **Restate the problem in plain language**, without proposing a solution
   yet. If you can't do this in one paragraph, the request likely needs to
   be split or clarified further.
2. **Identify actors, constraints, and out-of-scope items** — see
   [`docs/domain.md`](../docs/domain.md) for the full structure of a domain
   brief.
3. **Surface assumptions explicitly.** List anything you're inferring
   rather than were told, and flag it for confirmation rather than silently
   proceeding on a guess.
4. **Ask clarifying questions where it matters.** Prioritize questions that
   would change the solution shape, not ones that are merely nice to know.
5. **Write the domain brief** using the structure in
   [`docs/domain.md`](../docs/domain.md), keeping it generalized and
   synthetic — no real proprietary or private system details (see
   [`docs/methodology.md#security-and-privacy`](../docs/methodology.md#security-and-privacy)).
6. **Log any material scoping decisions** in the project's decision ledger
   using [`templates/decision-ledger-entry.md`](../templates/decision-ledger-entry.md).

## Outputs

- A domain brief (see [`docs/domain.md`](../docs/domain.md) for structure;
  [`examples/monitoring-dashboard/DOMAIN.md`](../examples/monitoring-dashboard/DOMAIN.md)
  for a worked example).
- Decision ledger entries for any scoping choices made along the way.

## Checkpoint

Confirm the domain brief with the requester before proceeding to
`write-spec` if there was any real ambiguity — a wrong shared understanding
here compounds through every later step.

## Next skill

[`skills/write-spec.md`](write-spec.md)
