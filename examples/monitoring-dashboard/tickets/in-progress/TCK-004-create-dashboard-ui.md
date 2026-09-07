## TCK-004: Create dashboard UI

**Status:** in-progress
**Severity:** S2
**Spec reference:** [`../../SPEC.md`](../../SPEC.md#requirements) (Requirement 4)
**Depends on:** TCK-002, TCK-003

### Problem

Render one status card per service, color-coded by status, updating as new
events arrive, so the on-call engineer can assess health in under 10
seconds (see [`../../DOMAIN.md`](../../DOMAIN.md#success-signal)).

### Acceptance criteria

- [ ] One card per configured service (`checkout-api`, `auth-api`,
      `notifications-worker`), showing current status, latency, and error
      rate.
- [ ] Card color reflects status: green = `ok`, amber = `degraded`, red =
      `down`.
- [ ] Card updates within 5 seconds of a new event for that service.
- [ ] Dashboard renders correctly with zero events (no data yet) without
      erroring.

### Notes

Blocked on TCK-003 reaching `tickets/done/` for the final alert-state
contract the UI reads; UI layout work can proceed in parallel using the
schema from TCK-001 in the meantime.

### Influence Note

> **Influence Note:** This artifact was produced under AI model assistance
> within the Operator Framework. It contains synthetic data only, reflects no
> proprietary or private project material, and remains subject to human
> review before execution or release.
