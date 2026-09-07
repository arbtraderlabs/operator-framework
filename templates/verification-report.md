# Verification Report Template

Produced by [`skills/verify/skill.md`](../skills/verify/skill.md), independently of
whoever executed the ticket where practical. See
[`docs/VERIFY.md`](../docs/VERIFY.md) for the standard this report must
meet.

---

# Verification Report: <Ticket ID(s) covered>

**Ticket(s):** <relative link(s) to the ticket file(s)>
**Execution report reference:** <relative link>
**Verified by:** <human name / role, or model + human supervisor — ideally
distinct from the executor>
**Date:** YYYY-MM-DD

## Method

How verification was performed (re-derivation, spot check, test execution,
structured review, etc.).

## Findings

Checked against each acceptance criterion from the ticket:

- [x] <Criterion> — Pass: <specific evidence>
- [x] <Criterion> — Pass with notes: <what to follow up on>
- [ ] <Criterion> — Fail: <specific reason>

## Safety / privacy check

Confirm no real secrets, proprietary data, or private material were
introduced (see
[`README.md#security-and-privacy`](../README.md#security-and-privacy)).

- [ ] Confirmed synthetic data only
- [ ] Confirmed Influence Note present on produced artifacts

## Overall result

**Pass | Pass with notes | Fail**

## Human sign-off

**Signed off by:** <human name/role>
**Date:** YYYY-MM-DD

A verification report is not final until this section is completed by a
human, per [`docs/adr/ADR-004-git-native-ticketing.md`](../docs/adr/ADR-004-git-native-ticketing.md).

## Influence Note

> **Influence Note:** This artifact was produced under AI model assistance
> within the Operator Framework. It contains synthetic data only, reflects no
> proprietary or private project material, and remains subject to human
> review before execution or release.
