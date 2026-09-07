# Specification: Monitoring Dashboard

**Status:** approved
**Domain reference:** [`DOMAIN.md`](DOMAIN.md)

Produced via [`skills/write-spec.md`](../../skills/write-spec.md) using
[`templates/spec.md`](../../templates/spec.md). All data, service names,
and identifiers below are synthetic.

## Summary

A single-page dashboard showing the health of three example backend
services (`checkout-api`, `auth-api`, `notifications-worker`), fed by a
simple JSON-line metrics format, with configurable alert thresholds and a
24-hour in-memory retention window.

## Goals

- Show current status (healthy / degraded / down) for each of the three
  services at a glance.
- Alert the on-call engineer when a service crosses a configured threshold.
- Keep the v0.1 implementation simple: in-memory storage, no database.

## Non-goals

- Historical analysis beyond 24 hours.
- Multi-team or multi-tenant support.
- Mobile notifications — dashboard view and a synthetic webhook only.

## Requirements

1. **Metrics schema.** Define a JSON-line event format: `{"service": string,
   "timestamp": ISO-8601 string, "latency_ms": number, "error_rate": number
   (0–1), "status": "ok" | "degraded" | "down"}`. Values in examples must be
   synthetic.
2. **Ingestion pipeline.** Accept a stream of metric events matching the
   schema, validate them, and retain the last 24 hours per service
   in-memory.
3. **Alerting rules.** Evaluate each incoming event against configurable
   thresholds (e.g. `error_rate > 0.05` or `latency_ms > 800` triggers
   "degraded"; explicit `"down"` status always triggers an alert). Alerts
   fire to a synthetic webhook endpoint.
4. **Dashboard UI.** Render one status card per service, color-coded
   (green/amber/red), showing current status, latency, and error rate, and
   updating as new events arrive.
5. **Synthetic data generator.** Provide a way to generate realistic-looking
   but entirely synthetic metric events for demos and testing, so no real
   traffic data is ever required.

## Design overview

```
[synthetic data generator] ──▶ [ingestion pipeline] ──▶ [in-memory 24h store]
                                        │                         │
                                        ▼                         ▼
                                 [alerting rules] ──▶ [dashboard UI]
                                        │
                                        ▼
                              [synthetic webhook]
```

Thresholds live in a simple config file (see D-001 in
[`DECISIONS.md`](DECISIONS.md)); retention is a fixed 24-hour in-memory
window (see D-002).

## Risks and open questions

- **Risk:** in-memory retention means data is lost on restart. Accepted for
  v0.1 (see D-002); revisit if durability becomes a requirement.
- **Open question:** none outstanding — all resolved during `resolve` (see
  [`DOMAIN.md`](DOMAIN.md#open-questions-resolved-before-write-spec)).

## Influence Note

> **Influence Note:** This artifact was produced under AI model assistance
> within the Operator Framework. It contains synthetic data only, reflects no
> proprietary or private project material, and remains subject to human
> review before execution or release.
