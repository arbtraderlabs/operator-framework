# Skill: adopt

**Type:** optional assessment skill — entry path for existing projects
**Purpose:** Inspect an existing project, map its current practice onto OPERATE, identify gaps, and recommend the smallest useful adoption path without demanding a rewrite.

## Why this matters

Most teams do not discover Operator Framework before starting work. They already have repositories, branches, runbooks, tickets, release habits, test environments, deployment rules, and informal guardrails. The framework should recognise useful practice that already exists rather than grading only whether files use Operator names.

`adopt` answers:

> "I just found Operator. Scan what I already have. How close am I, what am I missing, and what should I do next?"

## Inputs

- The existing repository or project material the operator can inspect.
- Relevant documentation, tickets/issues, pull requests, CI/CD configuration, environment notes, runbooks, tests, release rules, and handoff material.
- [`docs/ENVIRONMENT_GUARDRAILS.md`](../../docs/ENVIRONMENT_GUARDRAILS.md).

Do not require access to private production systems merely to complete the assessment. Assess only what can be evidenced safely.

## Procedure

1. **Inspect before asking.** Read existing project artifacts first. Do not ask the user to describe practices that are already documented.
2. **Discover the real workflow.** Identify how the project currently handles intent, decisions, specifications, bounded work, execution, evidence, verification, environments, release, and handoff — regardless of terminology.
3. **Map evidence onto OPERATE.** For each stage, record what already exists:
   - ORIENT — problem discovery, assumptions, constraints, preflight;
   - PIN DOWN — requirements, ADRs, decisions, specs;
   - ESTABLISH — tickets/issues, acceptance criteria, dependencies;
   - ROUTE — executor choice, permissions, verification planning, escalation;
   - ACT — bounded execution and change control;
   - TRACE — execution evidence, changed files, test/build results;
   - EVALUATE — independent review, CI, acceptance, human sign-off.
4. **Assess environment safety.** Identify where experimentation is safe, which environments are protected, and whether promotion boundaries are durable. Do not require a dedicated SIM tier if current isolation is sufficient for the project's risk.
5. **Classify each area by evidence**, not by naming convention:
   - **Established** — durable, repeatable evidence exists;
   - **Partial** — useful practice exists but is informal, inconsistent, or incomplete;
   - **Missing** — no durable evidence found;
   - **Not needed yet** — unnecessary for the project's current shape/risk.
6. **Recommend the smallest useful migration.** Preserve good existing mechanisms. Prefer adapters, references, or small durable files over replacing functioning systems just to match framework vocabulary.
7. **Separate project fixes from framework learning.** If the assessment reveals a pattern that could improve Operator Framework for many users, record it as a **framework feedback candidate**. Explain the reusable pattern without copying proprietary/project-specific material.
8. **Suggest contribution, never silently modify the framework.** If a feedback candidate is genuinely reusable and the user has an Operator Framework checkout/fork, propose an issue or PR. The human decides whether to contribute. Framework evolution must still pass normal review and verification.

## Assessment output

Use [`templates/adoption-assessment.md`](../../templates/adoption-assessment.md).

The report must contain:

- a short description of the project's observed operating model;
- an evidence-backed OPERATE mapping;
- environment / blast-radius observations;
- what is already strong and should be preserved;
- the highest-value gaps;
- a pragmatic next-step sequence;
- framework feedback candidates, if any;
- explicit unknowns where evidence was unavailable.

Do not generate a vanity score. A numeric percentage can imply precision the evidence does not support. Use the four evidence classifications above and a plain-language conclusion.

## Adoption path

A typical existing project should be able to move incrementally:

```text
inspect existing practice
        ↓
protect environment boundaries
        ↓
make key decisions/spec durable
        ↓
add bounded tickets + acceptance criteria
        ↓
standardise evidence + independent verification
        ↓
adopt more Operator structure only where it adds value
```

The result may legitimately be: "you already do most of this; document two missing boundaries and keep your current tools."

## Framework feedback loop

Operator should improve from real use without becoming self-modifying or autonomous.

```text
real project
    ↓
adoption assessment
    ↓
reusable gap discovered?
   / \
 no  yes
 |    |
keep  create framework feedback candidate
      ↓
      human chooses issue / PR
      ↓
      normal Operator review + verify
      ↓
      framework version advances
```

This is a human-governed learning loop, not automatic self-editing.

## Next skill

After assessment, route according to the highest-value unresolved gap. Commonly this is [`preflight`](../preflight/skill.md), [`resolve`](../resolve/skill.md), or [`plan-tickets`](../plan-tickets/skill.md). Do not restart stages already satisfied by durable existing evidence.
