# Handoff Note Template

Produced by [`skills/handoff/skill.md`](../skills/handoff/skill.md) whenever work
pauses or changes hands. See [`docs/HANDOFF_PROTOCOL.md`](../docs/HANDOFF_PROTOCOL.md) for
when to write one.

---

# Handoff: <Project/Spec name>

**Date:** YYYY-MM-DD
**From:** <human name / role, or model + human supervisor>
**To:** <next human/role, or "unassigned">

## Environment

- **Host / environment:** <hostname, dev/staging/prod, container, etc.>
- **Repository:** <path or remote>
- **Branch:** <branch, and whether it is pushed>
- **Working tree:** clean | dirty (summarize uncommitted changes)
- **Last known good commit:** <SHA or short description>

## Current state

- **Spec:** <relative link>, status: draft | approved
- **Active ticket(s):** <relative link(s)>, lifecycle stage: backlog |
  in-progress | review | done
- **Decision ledger:** <relative link>, latest entry: D-XXX

## What's done

Concrete summary — link to the execution/verification reports rather than
re-describing them in full.

## What's next

The specific next action for whoever picks this up. Not "continue the
work" — name the actual next step.

## Context to carry forward

- **Active spec:** <relative link>
- **Active ticket:** <relative link>
- **Relevant ADRs / decisions:** <links>

## Do not repeat

- Completed validation
- Rejected approaches
- Already-resolved ambiguity
- Work already committed

## Blockers

Anything the next person/model needs from someone else before they can
proceed (approval, access, information).

## Pointers

- <Relative link to spec section in play>
- <Relative link to ticket(s)>
- <Relative link to relevant decision ledger entries>
