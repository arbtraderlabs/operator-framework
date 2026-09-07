# Ticket Template

Copy this file to `TCK-<number>-<kebab-title>.md` inside the appropriate
[lifecycle directory](../docs/TICKET_SYSTEM.md) (`tickets/backlog/` when
first created). See [`docs/TICKET_SYSTEM.md`](../docs/TICKET_SYSTEM.md) for
the full lifecycle and conventions.

---

## TCK-XXX: <Short, specific title>

**Status:** backlog | in-progress | review | done
**Severity:** S0 | S1 | S2 | S3 (see
[`docs/TICKET_SYSTEM.md#severity`](../docs/TICKET_SYSTEM.md#severity);
default S2)
**Spec reference:** <relative link to the spec section this implements>
**Depends on:** <ticket IDs this requires, or "none">

### Problem

One or two sentences: what needs to be true after this ticket that isn't
true now.

### Acceptance criteria

- [ ] <Specific, checkable criterion 1>
- [ ] <Specific, checkable criterion 2>
- [ ] <Add as many as needed — vague criteria are not acceptable>

### Route

_Include only when execution differs from the defaults in
[`docs/MODEL_ROUTING.md`](../docs/MODEL_ROUTING.md); delete this section when
all defaults apply. Record only what materially differs or adds value._

- **Execution profile:** <mechanism class, if different from the default>
- **Verification method:** <concrete check and pass condition, if known>
- **Context required:** <minimal files / spec sections / ADRs, if not the
  default>
- **Escalation conditions:** <only if different from the standard stop list>

### Notes

Anything an executor needs that isn't obvious from the spec: constraints,
things explicitly out of scope for this ticket, links to related decisions
in the [decision ledger](../docs/DECISION_LEDGER.md).

### Influence Note

> **Influence Note:** This artifact was produced under AI model assistance
> within the Operator Framework. It contains synthetic data only, reflects no
> proprietary or private project material, and remains subject to human
> review before execution or release.
