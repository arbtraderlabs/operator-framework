# ADR-0004: Mandatory Human Verification Gate Before Release

**Status:** Accepted

## Context

AI-executed work can look complete and well-reasoned while still containing
subtle errors, scope drift, or inadvertently included sensitive material.
Letting execution, verification, and release all be performed autonomously
by the same process removes the one check most likely to catch these
issues: independent human judgment at the point something becomes
consequential (marked "done", or made public).

## Decision

Two points in the framework require an explicit human sign-off and cannot be
fully automated away:

1. **Ticket verification** ([`skills/verify/skill.md`](../../skills/verify/skill.md)) —
   a ticket does not move to `tickets/done/` on a model's self-assessment
   alone; a human confirms the verification report's finding.
2. **Public release** ([`skills/public-release/skill.md`](../../skills/public-release/skill.md))
   — nothing produced under this framework is published without an explicit
   human go-ahead, following the pre-publish scan for proprietary or private
   material.

## Consequences

- **Positive:** Establishes a hard backstop against silently-declared
  "done" work and against accidental disclosure of sensitive material.
- **Positive:** Keeps humans accountable for consequential decisions, which
  matters for trust in the framework's output.
- **Negative:** Introduces latency versus a fully autonomous pipeline —
  work cannot be marked done or published without a human being available
  to confirm. Considered an acceptable and intentional tradeoff given the
  framework's goal of auditable, trustworthy operation over raw throughput.
- **Negative:** Requires that whoever adopts this framework actually staff
  and honor these gates; a team that rubber-stamps them defeats the point.
  This ADR does not eliminate that risk, but the framework requires the
  gate to exist so it *can* be honored.
