# Environment Contract: <Project Name>

**Status:** draft | approved | superseded
**Last reviewed:** <date>

Use this template only to the depth the project needs. A project is not required to create DEV, SIM, STAGING, and PROD tiers. It is required to make consequential boundaries explicit.

## Repository / workspace responsibilities

Repository responsibility and runtime environment are related but not identical. A project may use separate repositories for development, generated production output, marketing/public content, infrastructure, or release artefacts.

| Repository / workspace | Responsibility | Development allowed? | Manual edits allowed? | Canonical source / upstream |
|---|---|---|---|---|
| <repo or workspace role; use safe names in public artifacts> | <development / release candidate / generated output / marketing / other> | yes / controlled / no | yes / controlled / no | <source role or n/a> |

Record responsibility boundaries when confusing one repository for another could create operational risk. In particular, identify repositories that are generated/promotion targets rather than development sources.

## Environment map

| Environment | Purpose | How identified | Writes | Tests / experiments | Real-world side effects |
|---|---|---|---|---|---|
| <LOCAL / DEV / SIM / PROD / other> | <purpose> | <repo/branch/host role/account/namespace; no secrets> | allowed / controlled / blocked | allowed / controlled / blocked | none / synthetic / real |

## Safe experimentation boundary

- **Where development happens:** <environment / workspace>
- **Where destructive testing is allowed:** <environment or none>
- **Where production-like validation happens:** <environment or not required>
- **Why this level of isolation is sufficient:** <short risk-based explanation>

## Protected environments

For each protected environment:

### <Environment name>

**Purpose:** <what it serves>

**Permitted actions**
- <read-only diagnosis, controlled deployment, etc.>

**Forbidden actions**
- <experimental development, ad-hoc destructive commands, manual generated-file edits, etc.>

**Human gate**
- <what needs explicit approval>

## Promotion path

```text
<canonical source> -> <verification/gate> -> <candidate> -> <human gate> -> <protected target>
```

Describe how an accepted change moves between environments or repository responsibilities. State which source is canonical and whether a downstream target is generated or promotion-only. If the project has no production environment, state that explicitly.

## Rollback / recovery

- <expected recovery mechanism or why not applicable>

## Unknown-environment rule

If the operator cannot determine the active environment with sufficient confidence, consequential execution stops until it is classified. Read-only discovery may continue where safe.

## Influence Note

> **Influence Note:** This artifact was produced under AI model assistance
> within the Operator Framework. It contains synthetic data only, reflects no
> proprietary or private project material, and remains subject to human
> review before execution or release.
