# Changelog

## v0.3.0 — in development

### Added

- Environment guardrail doctrine defining safe experimentation boundaries without forcing every project to create a dedicated simulation tier.
- Reusable `ENVIRONMENTS.md` contract template.
- Proportional environment handling: continue when state is consistent or low-risk, warn when something does not fit the expected path, and stop only for clear consequential or explicitly forbidden mismatches.
- Unknown-environment protection for consequential actions whose impact cannot be safely bounded.
- Optional target-environment block for operational tickets.
- Existing-project `adopt` assessment skill that maps current practice onto OPERATE rather than forcing a rewrite.
- Evidence-based adoption classifications: Established, Partial, Missing, Not needed yet.
- Adoption assessment template with environment review, preserve/gap analysis, pragmatic next steps, and framework feedback candidates.
- Human-governed framework feedback loop: real project learning may suggest an Operator issue or PR, but the framework never silently modifies itself.

### Changed

- `/operate` now recognises established non-Operator projects and can route them to adoption assessment.
- `preflight` now applies environment awareness proportionally before consequential execution and reuses existing project controls where possible.
- `execute-ticket` now checks environment/workspace alignment when the ticket or side effects make it relevant.
- `AGENTS.md` now requires environment identification before consequential actions.
- Repository/workspace responsibility is treated separately from runtime environment so generated output, release, marketing, infrastructure, and development repositories are not assumed to be interchangeable.

### Versioning

This development line introduces a root `VERSION` file. Release history remains visible through Git commits and pull requests; future releases should update both `VERSION` and this changelog.
