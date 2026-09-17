# Skill: operate

**Type:** entry skill — user-facing front door, not a workflow step
**Invoke:** `/operate`
**Purpose:** Inspect the repository, infer the current OPERATE state from
durable artifacts, and route into the appropriate workflow skill. One
obvious way to start, assess, or resume work without knowing the stage,
skill, or artifacts to use.

## Behaviour

1. **Inspect before asking.** Read git state, README/AGENTS, `ENVIRONMENTS.md`
   when present, `docs/adr/`, any specification and decision ledger, the
   ticket lifecycle dirs, and execution/verification reports or handoff notes.
   Never ask for facts the repository can answer.
2. **Recognise existing projects.** If the repository predates Operator or
   already has meaningful workflows that do not use Operator artifacts, offer
   the [`adopt`](../adopt/skill.md) assessment path rather than assuming the
   project must restart at ORIENT.
3. **Establish environment safety before consequential execution.** Determine
   where experimentation is safe and whether any live/protected environment
   exists. If the project has operational boundaries but no durable environment
   contract, route through [`preflight`](../preflight/skill.md) before ACT. See
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
   push approval, environment protections, or security/privacy rules.

## State routing

| Inspection result | OPERATE | Route to |
|---|---|---|
| Existing project with non-Operator process | assessment | [`adopt`](../adopt/skill.md) |
| Operational project; environment boundary unclear | ORIENT / safety | [`preflight`](../preflight/skill.md) |
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
Environment mismatch is an additional v0.3 stop condition: do not execute a
ticket in an environment where its requested actions are not permitted.

## Outputs

Inferred current state and recommended next skill; any decision entries
created while resolving. For an existing project, this may instead be a
recommendation to run the adoption assessment before changing anything.

## Next skill

The workflow or assessment skill the state routing selects.
