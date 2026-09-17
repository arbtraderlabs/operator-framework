# Environment Guardrails

Operator Framework requires a project to know **where experimentation is safe** before consequential execution begins. It does not require every project to create a dedicated simulation server.

The required outcome is awareness and classification, not infrastructure or ceremony for its own sake.

## Core rule

> Identify enough about the environment, its purpose, permitted actions, and promotion path to keep delivery on course without adding unnecessary friction.

Environment awareness is proportional. A mismatch or oddity is not automatically a blocker.

```text
observe
  ↓
compare expected vs observed
  ↓
does it smell right?
  ├─ yes / low consequence ────────────────> continue
  ├─ uncertain / inconsistent ─────────────> flag + recommend a check
  └─ clear high-consequence mismatch ──────> stop
```

The operator should distinguish between:

- **inform** — useful context or a low-consequence deviation that does not threaten delivery;
- **warn** — something is inconsistent, unexpected, or insufficiently evidenced and should be checked before the next consequential boundary;
- **stop** — there is strong evidence that continuing could cause a material consequence, such as destructive work in the wrong environment or bypassing an explicit production boundary.

Guardrails should increase awareness before they increase friction.

## Unknown environments

If the environment cannot be identified with sufficient confidence, treat **consequential actions whose impact cannot be bounded** as protected until classification is good enough to proceed.

Protected does not mean "do nothing." Read-only inspection, evidence gathering, log review, local analysis, and other low-risk discovery may continue where access permits. Low-risk reversible work may also continue when its effects are clearly contained.

Deployment, destructive commands, database writes, service restarts, publication, credential changes, or other actions with real-world side effects should pause when the operator cannot establish that they are being performed in an appropriate environment.

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

The framework does not prescribe the label. It requires the boundary to be clear enough for the work being performed.

## Environment classes

Projects may use their own vocabulary. The common classes below are descriptive, not mandatory infrastructure tiers.

| Class | Typical purpose | Default posture |
|---|---|---|
| LOCAL / DEV | build, experiment, debug | writes and tests allowed within project constraints |
| TEST / SIM | production-like validation | controlled writes; no real customer side effects unless explicitly designed |
| STAGING / CANDIDATE | verify an accepted artefact before promotion | no experimental development; changes arrive through the defined flow |
| PROD / LIVE | serve real users or perform real-world actions | protected from experimentation; direct change follows the project's operational procedure |
| PUBLIC / RELEASE | customer-facing or public artefacts | controlled publication; no unrelated engineering work |

A project may have only one or two of these. Do not invent extra environments when the risk does not justify them.

## Repository responsibility is not the same as runtime environment

A project may separate responsibilities across repositories or workspaces even when those repositories do not map one-to-one to DEV, SIM, or PROD.

Examples include:

- an integration repository used for engineering;
- a release-candidate repository used only for accepted artefacts;
- a generated production-output repository that is not a development workspace;
- a public marketing repository with no application-development responsibility;
- an infrastructure repository whose changes affect several runtime environments.

The operator should understand both the **workspace responsibility** and the **runtime target** before drawing conclusions from either one alone.

## The environment contract

For operational or multi-environment projects, a durable `ENVIRONMENTS.md` can be created from [`templates/environment-contract.md`](../templates/environment-contract.md).

Do not duplicate a working runbook, deployment map, repository guard, or equivalent artifact merely to satisfy Operator. If existing documentation already answers the important questions, reference and use it. Create `ENVIRONMENTS.md` when it closes a real visibility gap.

A useful contract records, as needed:

1. environment or workspace name and purpose;
2. how it is identified (repository, branch, host role, account, namespace, or other non-secret locator);
3. permitted and forbidden actions where those boundaries matter;
4. data / side-effect boundary;
5. promotion source and target where applicable;
6. rollback or recovery expectation where consequential;
7. human gates required before crossing a consequential boundary.

Do not place secrets, customer data, private hostnames, credentials, or proprietary implementation details in a public Operator artefact. Real projects may keep sensitive topology in an appropriately private location and reference the safe abstraction from tracked framework artefacts.

## Preflight behaviour

Before consequential ACT, the operator should be able to answer enough of these questions for the risk involved:

```text
Where am I?
What is this environment or workspace for?
What am I allowed to change here?
What would be consequential here?
Where should this work actually be performed?
How does an accepted change reach its destination?
```

If the requested target and the observed environment differ, first assess the consequence rather than treating the difference itself as the failure.

Example — warning:

```text
Work verified in: SIM
Observed output target: PROD
Expected path: SIM -> candidate -> PROD

WARN — PROMOTION PATH LOOKS INCONSISTENT
The implementation may be complete, but the release state does not match the documented path.
Verify the intended target before promotion.
```

Example — stop:

```text
Ticket target: SIM
Observed environment: PROD
Requested action: destructive migration

STOP — HIGH-CONSEQUENCE ENVIRONMENT MISMATCH
Do not execute the destructive action here.
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

Existing projects often already have useful guardrails under different names. Do not demand that they rename or replace working mechanisms to match Operator.

Use the adoption assessment (`skills/adopt/skill.md`) to discover the project's actual workflow, map it onto OPERATE, identify missing protection, and recommend the smallest useful changes.

A valid conclusion may be that the project already has sufficient controls and needs no new environment artifact.

## Relationship to severity and routing

Environment is not the same as ticket severity. A small textual production change can still have a large blast radius; a complex local refactor may have no live impact.

ROUTE should consider both:

- ticket severity and reversibility;
- target environment and side effects;
- verification strength;
- permissions and human gates.

See [`docs/MODEL_ROUTING.md`](MODEL_ROUTING.md).
