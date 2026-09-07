# Skill: public-release

**Order:** 9 of 9
**Purpose:** The final, deliberate step before anything produced under this
framework becomes public — a mandatory scan and human sign-off, never a
default outcome of finishing work.

## When to use

Whenever a project, or any artifact from it, is about to be published:
pushed to a public repository, shared externally, or otherwise made
visible outside the working team.

## Inputs

- All artifacts intended for release (spec, tickets, reports, decision
  ledger, code/content).
- The verification reports for any tickets included.

## Procedure

1. **Confirm every relevant ticket is in `tickets/done/`** with a Pass or
   Pass-with-notes verification report and human sign-off (see
   [`skills/verify.md`](verify.md)). Do not release work still in
   `in-progress` or `review`.
2. **Scan for real proprietary or private material.** Search every artifact
   for real customer names, internal URLs, production credentials, or
   business logic that wasn't meant to be generalized. Anything found must
   be removed or replaced with synthetic equivalents before release — see
   [`README.md#security-and-privacy`](../README.md#security-and-privacy).
3. **Scan for secrets.** Check for tokens, keys, connection strings, or
   credentials in any form, including inside examples or configuration
   snippets. None should ever be present, even placeholder-looking real
   ones.
4. **Confirm the Influence Note is present** verbatim on every artifact
   that requires it (see
   [`PRINCIPLES.md`](../PRINCIPLES.md#7-disclosure-over-ambiguity--the-influence-note)).
5. **Validate internal links and structure** — relative links between
   docs, skills, templates, and examples should resolve; the framework's
   own navigation is part of what's being released.
6. **Get explicit human sign-off to publish.** This is mandatory (see
   [`docs/adr/0004-human-verification-gate-before-release.md`](../docs/adr/0004-human-verification-gate-before-release.md))
   and is independent from the sign-off already obtained during `verify` —
   verification confirms the work is correct; this confirms it is safe and
   appropriate to make public.
7. **Publish**, then confirm the public artifact matches what was scanned
   (no last-minute unreviewed changes slipped in between scan and push).

## Outputs

- A published, public artifact (repository, document, or release).
- A record of the scan performed and the sign-off obtained (a decision
  ledger entry is appropriate here).

## Checkpoint

**Mandatory human sign-off**, distinct from the verification sign-off.
Nothing is published without it.

## Next skill

None — this is the final skill in the sequence for a given piece of work.
If new work arises, return to [`skills/preflight.md`](preflight.md).
