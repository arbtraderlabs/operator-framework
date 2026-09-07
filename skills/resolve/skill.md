# Skill: resolve

**Order:** 2 of 9
**Purpose:** Turn an ambiguous or underspecified request into a clear,
agreed problem statement — a domain brief — before any solution is
proposed.

## Why this matters

Models can competently build the wrong interpretation when they start from a
different mental model than the requester. What is obvious in the user's
head is not automatically present in the model's context. Resolve aligns
those interpretations before expensive execution begins — a few strong
reasoning turns up front are cheaper than rebuilding the wrong feature later.

## When to use

After [`skills/preflight/skill.md`](../preflight/skill.md), whenever the request is
ambiguous, open-ended, or could reasonably be interpreted several ways.

## Inputs

- The request, plus preflight's notes on scope/access/safety.
- Any existing domain material for the project.

## Procedure

1. **Restate the problem in plain language**, without proposing a solution
   yet. If you can't do this in one paragraph, the request likely needs to
   be split or clarified further.
2. **Identify actors, constraints, and out-of-scope items** — see
   [`docs/DOMAIN.md`](../../docs/DOMAIN.md) for the full structure of a domain
   brief.
3. **Surface assumptions explicitly.** List anything you're inferring
   rather than were told, and flag it for confirmation rather than silently
   proceeding on a guess.
4. **Ask clarifying questions where it matters.** Prioritize questions that
   would change the solution shape, not ones that are merely nice to know.
5. **Write the domain brief** using the structure in
   [`docs/DOMAIN.md`](../../docs/DOMAIN.md), keeping it generalized and
   synthetic — no real proprietary or private system details (see
   [`docs/METHODOLOGY.md#security-and-privacy`](../../docs/METHODOLOGY.md#security-and-privacy)).
6. **Log any material scoping decisions** in the project's decision ledger
   using [`templates/decision.md`](../../templates/decision.md).

## Outputs

- A domain brief (see [`docs/DOMAIN.md`](../../docs/DOMAIN.md) for structure;
  [`examples/monitoring-dashboard/DOMAIN.md`](../../examples/monitoring-dashboard/DOMAIN.md)
  for a worked example).
- Decision ledger entries for any scoping choices made along the way.

## Checkpoint

Confirm the domain brief with the requester before proceeding to
`write-spec` if there was any real ambiguity — a wrong shared understanding
here compounds through every later step.

## Next skill

[`skills/write-spec/skill.md`](../write-spec/skill.md)
