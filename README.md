# Operator Framework

**Version:** v0.1 (initial public release)

Operator Framework is a documentation-first methodology for running AI-assisted
work as a disciplined, auditable operation rather than an ad hoc chat session.
It defines how a human operator and one or more AI models move a piece of work
from an unclear request to a verified, reportable outcome — through explicit
domain framing, written specifications, a ticket-based execution lifecycle,
and a decision ledger that keeps every material choice traceable.

The framework is **model-agnostic**: it assumes you are working with *a*
capable AI model (or several, routed by task), not any specific vendor or
product. Nothing here depends on a particular provider's API, branding, or
tooling.

## Why this exists

AI-assisted work fails in predictable ways: scope drifts, decisions are made
silently inside a chat transcript, "done" is declared without verification,
and handoffs lose context. Operator Framework addresses this by making the
**documentation the interface** between human intent and AI execution — every
skill in this framework reads and writes durable artifacts instead of relying
on conversational memory.

## Repository layout

| Path | Purpose |
|---|---|
| [`PRINCIPLES.md`](PRINCIPLES.md) | Core operating principles, including the Influence Note disclosure standard. |
| [`AGENTS.md`](AGENTS.md) | How any AI agent/model should behave when operating inside this framework. |
| [`docs/`](docs/) | Methodology, model routing, domain framing, decision ledger, reporting, ticket system, handoff, and verification guidance. |
| [`docs/adr/`](docs/adr/) | Architecture Decision Records explaining why the framework is built this way. |
| [`skills/`](skills/) | Nine discrete, sequential skills that operationalize the methodology. |
| [`templates/`](templates/) | Reusable templates referenced by the skills and docs. |
| [`tickets/`](tickets/) | Lifecycle directories (`backlog` → `in-progress` → `review` → `done`) for real work using this framework. |
| [`examples/monitoring-dashboard/`](examples/monitoring-dashboard/) | A complete worked example, end to end, using synthetic data only. |

## Quick start

1. Read [`PRINCIPLES.md`](PRINCIPLES.md) and [`AGENTS.md`](AGENTS.md).
2. Read [`docs/methodology.md`](docs/methodology.md) for the end-to-end flow.
3. Walk through the skills in order, starting at [`skills/preflight.md`](skills/preflight.md).
4. Study [`examples/monitoring-dashboard/`](examples/monitoring-dashboard/) to see the framework applied to a full (synthetic) project.

## The skill sequence

```
preflight → resolve → write-spec → plan-tickets → execute-ticket → report → verify → handoff → public-release
```

Each skill is documented independently in [`skills/`](skills/) and consumes or
produces artifacts described in [`docs/`](docs/) and [`templates/`](templates/).
See [`docs/methodology.md`](docs/methodology.md) for how they fit together.

## Security and privacy

- This repository, its examples, and its templates contain **synthetic data
  only**. No production systems, customer data, credentials, or proprietary
  material from any real project appear here or should ever be added.
- Do not paste real secrets, tokens, internal URLs, or private business
  logic into any ticket, spec, or report created from these templates.
- See [`docs/methodology.md#security-and-privacy`](docs/methodology.md#security-and-privacy)
  and [`skills/public-release.md`](skills/public-release.md) for the checks
  run before anything derived from this framework is made public.

## Status

v0.1 is a documentation-first release: the methodology, skills, templates,
and one worked example are complete and usable today. Tooling/automation
that enforces this structure programmatically is out of scope for v0.1 and
may follow in later versions.

## License

[MIT](LICENSE)
