# Skill: verify

**Order:** 7 of 9
**Purpose:** Independently confirm that executed work actually meets its
ticket's acceptance criteria and the specification — the framework's first
mandatory human checkpoint.

## Why this matters

An executor is the wrong person to declare their own work done: they are
motivated to see it as complete and can inherit their own blind spots.
Verification from a fresh context, a different model, or a human evaluates
the work against the spec and ticket rather than the executor's reasoning
path — giving the framework an independent acceptance boundary.

## When to use

For each ticket in `tickets/review/`, after its execution report exists.

## Inputs

- The ticket, its acceptance criteria, and the relevant spec section.
- The execution report (see
  [`templates/execution-report.md`](../../templates/execution-report.md)).

## Procedure

1. **Use a different vantage point than the executor where practical** — a
   different model instance, fresh context, or a human reviewer (see
   [`docs/MODEL_ROUTING.md`](../../docs/MODEL_ROUTING.md)). Do not simply
   re-read the execution report and agree with it.
2. **Check every acceptance criterion explicitly**, with specific evidence
   — not "looks fine." See [`docs/VERIFY.md`](../../docs/VERIFY.md) for the
   full standard.
3. **Check spec conformance and scope** — confirm the work matches the
   spec and didn't quietly expand or shrink scope without a logged
   decision.
4. **Run the safety/privacy check** — confirm no real secrets or
   proprietary/private data were introduced, and that the Influence Note is
   present on produced artifacts.
5. **Write the verification report** using
   [`templates/verification-report.md`](../../templates/verification-report.md),
   recording Pass, Pass with notes, or Fail with specifics.
6. **Get explicit human sign-off** — this is mandatory (see
   [`docs/adr/ADR-0004-mandatory-human-verification-gate.md`](../../docs/adr/ADR-0004-mandatory-human-verification-gate.md)).
   An AI-produced finding is an input to this decision, not a substitute
   for it.
7. **Move the ticket** to `tickets/done/` on Pass or Pass-with-notes, or
   back to `tickets/in-progress/` on Fail, with the findings attached.

## Outputs

- A verification report (see
  [`examples/monitoring-dashboard/reports/verification-report.md`](../../examples/monitoring-dashboard/reports/verification-report.md)).
- The ticket moved to its correct next lifecycle stage.

## Checkpoint

**Mandatory human sign-off** before the ticket is treated as done. Do not
proceed past this step without it.

## Next skill

[`skills/handoff/skill.md`](../handoff/skill.md) if work is pausing, otherwise return to
[`skills/execute-ticket/skill.md`](../execute-ticket/skill.md) for the next ticket, or
[`skills/public-release/skill.md`](../public-release/skill.md) once all relevant tickets
are done and the project is ready to publish.
