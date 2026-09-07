## TCK-005: Add synthetic data generator

**Status:** backlog
**Severity:** S3
**Spec reference:** [`../../SPEC.md`](../../SPEC.md#requirements) (Requirement 5)
**Depends on:** TCK-001

### Problem

Provide a way to generate realistic-looking but entirely synthetic metric
events for demos and testing, so development and demos never require real
traffic data (see D-003 in
[`../../DECISIONS.md`](../../DECISIONS.md#d-003-synthetic-data-generator-included-as-its-own-ticket)).

### Acceptance criteria

- [ ] Generator produces events conforming to the schema in TCK-001, for
      all three example services.
- [ ] Generator supports an "all healthy" mode and a "degraded scenario"
      mode (at least one service breaching thresholds) for demoing alerts.
- [ ] Generated output contains no real identifiers, timestamps tied to
      real events, or real infrastructure references — synthetic only.

### Route

**Execution profile:** inexpensive worker — clear, bounded, low-risk (S3)
work that does not need strong reasoning (see D-004 in
[`../../DECISIONS.md`](../../DECISIONS.md#d-004-severity-assigned-per-ticket-s3-backlog-routed-to-execution-tier)).
**Verification method:** generate events in both modes and confirm each
parses against the TCK-001 schema (deterministic schema check) and that the
"degraded scenario" output contains at least one service breaching the
thresholds from TCK-003.

### Notes

Not yet started. Scheduled after TCK-002 and TCK-003 land, since the
"degraded scenario" mode should exercise the real threshold logic once
finalized.

### Influence Note

> **Influence Note:** This artifact was produced under AI model assistance
> within the Operator Framework. It contains synthetic data only, reflects no
> proprietary or private project material, and remains subject to human
> review before execution or release.
