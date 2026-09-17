# Changelog

## v0.3.0 — in development

### Added

- Environment guardrail doctrine defining safe experimentation boundaries without forcing every project to create a dedicated simulation tier.
- Reusable `ENVIRONMENTS.md` contract template.
- Unknown-environment protection: consequential actions stop until the active environment is classified.
- Environment mismatch stop condition for execution.
- Optional target-environment block for operational tickets.
- Existing-project `adopt` assessment skill that maps current practice onto OPERATE rather than forcing a rewrite.
- Evidence-based adoption classifications: Established, Partial, Missing, Not needed yet.
- Adoption assessment template with environment review, preserve/gap analysis, pragmatic next steps, and framework feedback candidates.
- Human-governed framework feedback loop: real project learning may suggest an Operator issue or PR, but the framework never silently modifies itself.

### Changed

- `/operate` now recognises established non-Operator projects and can route them to adoption assessment.
- `preflight` now explicitly establishes environment identity and the safe experimentation boundary before consequential execution.
- `AGENTS.md` now requires environment identification before consequential actions.

### Versioning

This development line introduces a root `VERSION` file. Release history remains visible through Git commits and pull requests; future releases should update both `VERSION` and this changelog.
