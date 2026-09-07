# Domain Brief: Monitoring Dashboard

Produced via [`skills/resolve/skill.md`](../../skills/resolve/skill.md). Structure per
[`docs/DOMAIN.md`](../../docs/DOMAIN.md). All names, systems, and data
below are synthetic and invented for this example.

## Problem

Northwind Signal Co. (fictional) runs several small backend services. Right
now, the on-call engineer has to check three separate tools to understand
whether anything is degraded, which is slow and error-prone during an
incident. They need a single dashboard that shows service health at a
glance and alerts them when something needs attention.

## Actors

- **On-call engineer** — primary user; needs a fast, glanceable view during
  an incident.
- **SRE lead** — configures alert thresholds and reviews incident history.
- **Ingestion service** — a synthetic internal service that emits metrics
  (invented for this example; not a real system).

## Constraints

- Must work with metrics already emitted in a simple JSON line format
  (synthetic schema, defined in [`SPEC.md`](SPEC.md)).
- Initial version targets three example services only (`checkout-api`,
  `auth-api`, `notifications-worker` — all invented names).
- No real user or customer data may appear anywhere in metrics, dashboards,
  or examples — synthetic values only.
- Small team, limited time: v0.1 favors a simple, working dashboard over a
  feature-complete one.

## Out of scope

- Historical trend analysis beyond 24 hours.
- Multi-team / multi-tenant support.
- Mobile app or push notifications (alerts are dashboard + a synthetic
  webhook only).

## Success signal

The on-call engineer can determine, within 10 seconds of opening the
dashboard, whether any of the three services is degraded and why, without
checking any other tool.

## Open questions (resolved before write-spec)

- **Alert threshold source?** Resolved: SRE lead sets thresholds via a
  simple config file (see [`DECISIONS.md`](DECISIONS.md), D-001).
- **Data retention?** Resolved: 24 hours in-memory is sufficient for v0.1
  (see [`DECISIONS.md`](DECISIONS.md), D-002).
