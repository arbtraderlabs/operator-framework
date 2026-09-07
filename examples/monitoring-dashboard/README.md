# Example: Monitoring Dashboard

A complete, worked example of Operator Framework applied end to end, using
entirely synthetic data. This example follows the full flow described in
[`docs/methodology.md`](../../docs/methodology.md): domain brief →
specification → tickets → execution → reporting → verification.

**Influence Note:** This artifact was produced under AI model assistance
within the Operator Framework. It contains synthetic data only, reflects no
proprietary or private project material, and remains subject to human
review before execution or release.

## Scenario

A fictional small engineering team ("Northwind Signal Co.", entirely
invented for this example) needs a monitoring dashboard so their on-call
engineer can see service health at a glance instead of checking several
disconnected tools. No real company, product, or system is represented.

## Contents

| File | Role |
|---|---|
| [`DOMAIN.md`](DOMAIN.md) | Domain brief — problem, actors, constraints, produced by [`skills/resolve.md`](../../skills/resolve.md) |
| [`SPEC.md`](SPEC.md) | Specification — produced by [`skills/write-spec.md`](../../skills/write-spec.md) |
| [`DECISIONS.md`](DECISIONS.md) | Decision ledger — see [`docs/decision-ledger.md`](../../docs/decision-ledger.md) |
| [`tickets/`](tickets/) | Sample tickets across all four lifecycle stages — see [`docs/ticket-system.md`](../../docs/ticket-system.md) |
| [`reports/execution-report.md`](reports/execution-report.md) | Execution report for the completed tickets |
| [`reports/verification-report.md`](reports/verification-report.md) | Verification report for the completed tickets |

## How to read this example

Read in this order to see the methodology applied naturally:
`DOMAIN.md` → `SPEC.md` → `tickets/done/` → `reports/execution-report.md` →
`reports/verification-report.md` → `DECISIONS.md` (which threads through
all of the above) → `tickets/review/`, `tickets/in-progress/`,
`tickets/backlog/` (to see work at earlier lifecycle stages).

## Status

This example itself is v0.1: it demonstrates the pattern with a small,
plausible feature set, not a production-ready monitoring system.
