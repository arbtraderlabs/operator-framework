# Reporting

Reporting turns finished work into a written account that a verifier (and
later readers) can trust without re-doing the work themselves. Operator
Framework distinguishes two report types, produced by two different skills:

| Report | Produced by | Answers |
|---|---|---|
| Execution report | [`skills/report/skill.md`](../skills/report/skill.md) | "What did I do, and does it match the ticket?" |
| Verification report | [`skills/verify/skill.md`](../skills/verify/skill.md) | "Did an independent check confirm it actually meets the spec?" |

## Execution reports

An execution report is written by (or immediately after) whoever executed a
ticket. It should be honest about partial completion, deviations from the
ticket, and anything left undone — a report that only lists successes is
incomplete by definition. Use
[`templates/execution-report.md`](../templates/execution-report.md).

Minimum contents:
1. Which ticket(s) this covers, and their final status.
2. What was actually done, in enough detail to be checked against the spec.
3. Deviations from the ticket/spec, and why.
4. Known gaps, risks, or follow-ups.
5. The Influence Note (see [`PRINCIPLES.md`](../PRINCIPLES.md#7-disclosure-over-ambiguity--the-influence-note)).

## Verification reports

A verification report is written by whoever ran [`skills/verify/skill.md`](../skills/verify/skill.md)
— ideally someone (or some model instance) other than the executor. It
records what was checked, how, and the outcome. Use
[`templates/verification-report.md`](../templates/verification-report.md).

Minimum contents:
1. What was verified and against which spec/ticket.
2. Method used (re-derivation, spot check, test run, review, etc.).
3. Findings — pass, pass-with-notes, or fail, with specifics either way.
4. Sign-off status: whether a human has explicitly confirmed the result.
5. The Influence Note.

## Principles for good reporting

- **Specific over vague.** "Handled the edge cases" is not a finding;
  "confirmed empty-input and duplicate-ID cases return the documented
  error" is.
- **Traceable.** A reader should be able to go from the report back to the
  exact ticket, spec section, or decision it refers to via relative links.
- **No silent success.** If something could not be verified (e.g. no access
  to a real environment), say so explicitly rather than omitting it.

## Example

See [`examples/monitoring-dashboard/reports/execution-report.md`](../examples/monitoring-dashboard/reports/execution-report.md)
and [`examples/monitoring-dashboard/reports/verification-report.md`](../examples/monitoring-dashboard/reports/verification-report.md).
