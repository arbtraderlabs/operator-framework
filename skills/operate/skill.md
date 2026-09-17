# Skill: operate

**Type:** entry skill — user-facing front door, not a workflow step
**Invoke:** `/operate`
**Purpose:** Inspect the repository, infer the current OPERATE state from
durable artifacts, and route into the appropriate workflow skill. One
obvious way to start, assess, or resume work without knowing the stage,
skill, or artifacts to use.

## Behaviour

1. **Inspect before asking.** Read git state, README/AGENTS, `ENVIRONMENTS.md`
   or equivalent environment/release documentation when present, `docs/adr/`,
   any specification and decision ledger, the ticket lifecycle dirs, and
   execution/verification reports or handoff notes. Never ask for facts the
   repository can answer.
2. **Recognise existing projects.** If the repository predates Operator or
   already has meaningful workflows that do not use Operator artifacts, offer
   the [`adopt`](../adopt/skill.md) assessment path rather than assuming the
   project must restart at ORIENT.
3. **Apply environment awareness in proportion to the work.** Determine where
   experimentation is safe when the request can affect a consequential
   environment, repository responsibility, deployment target, or real-world
   side effect. Reuse existing guards and runbooks rather than creating new
   ceremony. See
   [`docs/ENVIRONMENT_GUARDRAILS.md`](../../docs/ENVIRONMENT_GUARDRAILS.md).
4. **Route from the earliest incomplete stage** (table below) — don't restart
   planning that already has durable output.
5. **Resolve decisions one at a time.** When PIN DOWN is needed, ask only
   genuine human decisions (intent, trade-offs, priorities, acceptance), one
   at a time, with evidence and a recommendation; record each decision using
   the project's existing durable decision mechanism, and create an ADR only
   where justified.
6. **Separate decisions from specification.** Finish decisions before
   `write-spec`; if a new one surfaces mid-spec, stop, return to PIN DOWN,
   record it, then continue.
7. **Delegate.** Follow the routed skill. Route executable work per
   [`docs/MODEL_ROUTING.md`](../../docs/MODEL_ROUTING.md) — cheapest reliable
   path, deterministic tools first.
8. **Respect gates.** Never bypass verify/public-release sign-off, commit or
   push approval, explicit environment protections, or security/privacy rules.

## State routing

| Inspection result | OPERATE | Route to |
|---|---|---|
| Existing project with non-Operator process | assessment | [`adopt`](../adopt/skill.md) |
| Consequential work; environment boundary materially unclear | ORIENT / safety | [`preflight`](../preflight/skill.md) |
| No sufficient durable plan/specification | ORIENT → PIN DOWN | [`resolve`](../resolve/skill.md) |
| Spec exists; decisions unresolved | PIN DOWN | [`resolve`](../resolve/skill.md) |
| Spec agreed; work unplanned | ESTABLISH | [`plan-tickets`](../plan-tickets/skill.md) |
| Executable ticket ready | ROUTE → ACT | [`execute-ticket`](../execute-ticket/skill.md) |
| Ticket blocked | blocker | classify, then [`execute-ticket`](../execute-ticket/skill.md) |
| Done; ticket unverified (review) | TRACE → EVALUATE | [`report`](../report/skill.md) / [`verify`](../verify/skill.md) |
| Done or pausing / ready to publish | gates | [`handoff`](../handoff/skill.md) / [`public-release`](../public-release/skill.md) |

Blockers use the v0.2 taxonomy — specification → planning, capability → local
escalation, reality/discovery → update durable truth (see
[`docs/MODEL_ROUTING.md`](../../docs/MODEL_ROUTING.md#blockers-and-escalation)).

Environment observations use the v0.3 proportional response:

- **continue** when expected and observed state align or the deviation is low-risk and contained;
- **warn** when the state looks inconsistent and should be checked before the next consequential boundary;
- **stop** only for a clear high-consequence mismatch or an explicit protected-boundary violation.

The operator should be able to say "the implementation is complete, but the
release state does not smell right" without treating correct implementation
work as failed.

## Outputs

Inferred current state and recommended next skill; any decision entries
created while resolving. For an existing project, this may instead be a
recommendation to run the adoption assessment before changing anything.
Warnings should identify the observed inconsistency and the next useful check,
not create a blocker by default.

## Next skill

The workflow or assessment skill the state routing selects.
