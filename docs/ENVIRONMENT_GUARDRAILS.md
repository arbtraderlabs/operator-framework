# Environment Guardrails

Operator Framework requires a project to know **where experimentation is safe** before consequential execution begins. It does not require every project to create a dedicated simulation server.

The required outcome is classification, not infrastructure for its own sake.

## Core rule

> Identify the environment, its purpose, permitted actions, forbidden actions, and promotion path before making consequential changes.

If the environment cannot be identified with sufficient confidence, treat it as **protected** until classified.

Protected does not mean "do nothing." Read-only inspection, evidence gathering, log review, and other non-destructive discovery may continue where access permits. Deployment, destructive commands, database writes, service restarts, publication, credential changes, and other consequential actions stop until the environment is known.

## Do I need a simulation environment?

Not necessarily.

A local script, static site, disposable prototype, or isolated development repository may need only a local development environment and tests. A live service with real users, data, money, external side effects, or meaningful operational blast radius needs a safe place to develop and validate changes before they reach production.

That safe place may be any appropriate isolation mechanism, including:

- a local clone or feature branch;
- a test suite with fixtures;
- a container;
- a virtual machine or WSL environment;
- a disposable cloud environment;
- a dedicated DEV, SIM, UAT, staging, or candidate system.

The framework does not prescribe the label. It requires the boundary to be explicit.

## Environment classes

Projects may use their own vocabulary. The common classes below are descriptive, not mandatory infrastructure tiers.

| Class | Typical purpose | Default posture |
|---|---|---|
| LOCAL / DEV | build, experiment, debug | writes and tests allowed within project constraints |
| TEST / SIM | production-like validation | controlled writes; no real customer side effects unless explicitly designed |
| STAGING / CANDIDATE | verify an accepted artefact before promotion | no experimental development; changes arrive through the defined flow |
| PROD / LIVE | serve real users or perform real-world actions | protected; no experimentation; direct change only through explicit operational procedure |
| PUBLIC / RELEASE | customer-facing or public artefacts | controlled publication; no unrelated engineering work |

A project may have only one or two of these. Do not invent extra environments when the risk does not justify them.

## The environment contract

For operational or multi-environment projects, keep a durable `ENVIRONMENTS.md` using [`templates/environment-contract.md`](../templates/environment-contract.md).

The contract records, at minimum:

1. environment name and purpose;
2. how it is identified (repository, branch, host role, account, namespace, or other non-secret locator);
3. permitted actions;
4. forbidden actions;
5. data / side-effect boundary;
6. promotion source and target where applicable;
7. rollback or recovery expectation;
8. human gates required before crossing a consequential boundary.

Do not place secrets, customer data, private hostnames, credentials, or proprietary implementation details in a public Operator artefact. Real projects may keep sensitive topology in an appropriately private location and reference the safe abstraction from tracked framework artefacts.

## Preflight behaviour

Before ACT, the operator should be able to answer:

```text
Where am I?
What is this environment for?
What am I allowed to change here?
What must never happen here?
Where should this work actually be performed?
How does an accepted change reach the next environment?
```

If the requested target and the observed environment disagree, stop and surface an **environment mismatch**.

Example:

```text
Ticket target: SIM
Observed environment: PROD

STOP — ENVIRONMENT MISMATCH
Do not execute the ticket here.
```

## Greenfield projects

For a new project, establish only the safety boundary the project currently needs. Examples:

```text
Environment: LOCAL DEVELOPMENT
Production: none
Safe experimentation: local working tree + tests
```

or:

```text
DEV: local/container — development and tests allowed
PROD: hosted service — experimentation prohibited
Promotion: DEV -> verify -> human approval -> PROD
```

Do not force a dedicated SIM environment just to satisfy the framework.

## Existing projects

Existing projects often already have useful guardrails under different names. Do not demand that they rename everything to match Operator.

Use the adoption assessment (`skills/adopt/skill.md`) to discover the project's actual workflow, map it onto OPERATE, identify missing protection, and recommend the smallest useful changes.

## Relationship to severity and routing

Environment is not the same as ticket severity. A small textual production change can still have a large blast radius; a complex local refactor may have no live impact.

ROUTE should consider both:

- ticket severity and reversibility;
- target environment and side effects;
- verification strength;
- permissions and human gates.

See [`docs/MODEL_ROUTING.md`](MODEL_ROUTING.md).
