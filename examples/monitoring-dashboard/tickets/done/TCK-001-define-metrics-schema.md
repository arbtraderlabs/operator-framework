## TCK-001: Define metrics schema

**Status:** done
**Spec reference:** [`../../SPEC.md`](../../SPEC.md#requirements) (Requirement 1)
**Depends on:** none

### Problem

Establish a single, agreed JSON-line metrics schema so ingestion, alerting,
and the dashboard UI all consume the same event shape.

### Acceptance criteria

- [x] Schema documented with field names, types, and allowed values.
- [x] Schema includes `service`, `timestamp`, `latency_ms`, `error_rate`,
      `status`.
- [x] At least 3 example events provided, using synthetic data only.

### Notes

Schema is documented in [`../../SPEC.md`](../../SPEC.md#requirements)
under Requirement 1. Example events:

```json
{"service": "checkout-api", "timestamp": "2026-01-10T09:00:00Z", "latency_ms": 120, "error_rate": 0.01, "status": "ok"}
{"service": "auth-api", "timestamp": "2026-01-10T09:00:05Z", "latency_ms": 950, "error_rate": 0.02, "status": "degraded"}
{"service": "notifications-worker", "timestamp": "2026-01-10T09:00:10Z", "latency_ms": 60, "error_rate": 0.00, "status": "ok"}
```

### Influence Note

> **Influence Note:** This artifact was produced under AI model assistance
> within the Operator Framework. It contains synthetic data only, reflects no
> proprietary or private project material, and remains subject to human
> review before execution or release.
