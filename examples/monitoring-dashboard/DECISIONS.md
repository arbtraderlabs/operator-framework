# Decision Ledger: Monitoring Dashboard

Append-only record of material decisions for this example project. See
[`docs/decision-ledger.md`](../../docs/decision-ledger.md) for the rules
(entries are never edited after the fact; reversals get a new entry).

---

## D-001: Alert thresholds configured via a simple file, not an admin UI

**Date:** 2026-01-12
**Made during:** `resolve`
**Status:** active

### Decision

The SRE lead sets alert thresholds by editing a simple config file
(synthetic example: `thresholds.example.json`), not through an admin UI.

### Context

An admin UI would require additional auth/UI work not justified by v0.1's
small user base (one SRE lead, three services).

### Alternatives considered

- **Admin UI for thresholds** — rejected for v0.1: adds meaningful UI/auth
  surface for a single-user need. May revisit if the team grows.
- **Hard-coded thresholds** — rejected: too inflexible even for v0.1.

### Consequences

TCK-003 (alerting rules) reads thresholds from this config file rather than
from a database or UI-managed setting.

---

## D-002: 24-hour in-memory retention, no persistent storage

**Date:** 2026-01-12
**Made during:** `resolve`
**Status:** active

### Decision

The dashboard retains only 24 hours of metrics, held in memory, with no
database or persistent store in v0.1.

### Context

The success signal (see [`DOMAIN.md`](DOMAIN.md#success-signal)) only
requires current/near-term status, not historical trend analysis, which is
explicitly out of scope.

### Alternatives considered

- **Persistent time-series database** — rejected for v0.1: adds
  infrastructure and cost disproportionate to the stated need. Logged as a
  known limitation (data lost on restart) rather than silently accepted.

### Consequences

TCK-002 (ingestion pipeline) implements a simple in-memory ring buffer per
service rather than a database-backed store. A future version could
introduce persistence without changing the dashboard's contract.

---

## D-003: Synthetic data generator included as its own ticket

**Date:** 2026-01-13
**Made during:** `plan-tickets`
**Status:** active

### Decision

Add a dedicated ticket (TCK-005) for a synthetic data generator, rather than
treating demo data as an afterthought of the ingestion pipeline ticket.

### Context

Keeping demo/test data generation as a first-class, separate concern makes
it easier to guarantee no real traffic data is ever needed to develop or
demo the dashboard — directly supporting the framework's synthetic-data
principle (see [`PRINCIPLES.md`](../../PRINCIPLES.md#6-synthetic-data-only-always)).

### Alternatives considered

- **Fold into TCK-002** — rejected: would blur ingestion logic with data
  generation, making both harder to verify independently.

### Consequences

TCK-005 is currently in `tickets/backlog/`, scheduled after the core
pipeline and UI tickets.
