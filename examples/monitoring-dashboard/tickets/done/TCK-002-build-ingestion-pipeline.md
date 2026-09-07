## TCK-002: Build ingestion pipeline

**Status:** done
**Severity:** S2
**Spec reference:** [`../../SPEC.md`](../../SPEC.md#requirements) (Requirement 2)
**Depends on:** TCK-001

### Problem

Accept a stream of metric events matching the agreed schema, validate
them, and retain the last 24 hours per service in memory.

### Acceptance criteria

- [x] Invalid events (missing fields, out-of-range `error_rate`) are
      rejected rather than stored.
- [x] Valid events are retained per-service for 24 hours, oldest events
      dropped after that window.
- [x] Retention uses an in-memory structure — no external database, per
      D-002 in [`../../DECISIONS.md`](../../DECISIONS.md#d-002-24-hour-in-memory-retention-no-persistent-storage).

### Notes

Implemented as a per-service ring buffer keyed by `service`, storing up to
24 hours of events; oldest entries evicted on insert once the window is
exceeded. See D-002 for why no persistent store is used in v0.1.

### Influence Note

> **Influence Note:** This artifact was produced under AI model assistance
> within the Operator Framework. It contains synthetic data only, reflects no
> proprietary or private project material, and remains subject to human
> review before execution or release.
