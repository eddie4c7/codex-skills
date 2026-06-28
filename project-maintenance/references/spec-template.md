# Spec Guidance And Template

Use this file before creating or updating `docs/specs/*.md`.

## Split Criteria

Update an existing spec when:

- Existing feature behavior or acceptance criteria changes.
- The request is a small extension of an existing feature.
- The same user, permission model, data, and lifecycle remain in place.

Create a new spec when:

- The capability can be explained independently.
- The capability can be tested, released, deprecated, or removed independently.
- It has different users, permissions, data, lifecycle, API boundary, or external integration.

Do not update a spec when:

- The code is only being fixed to match an existing spec.
- The change is internal-only and preserves user-visible behavior.
- The user requested read-only inspection.

## File Naming

Use concise kebab-case names, for example:

- `docs/specs/search-filters.md`
- `docs/specs/user-invitations.md`
- `docs/specs/billing-webhooks.md`

## Template

```markdown
# Spec: <feature or capability name>

## Status

- State: Draft | Accepted | Implemented | Deprecated
- Last updated: <YYYY-MM-DD>
- Evidence: Observed | Inferred | Unverified | Mixed

## Scope

Describe what this feature covers.

## Non-Goals

List nearby behavior that is intentionally out of scope.

## Current Behavior

Describe observed behavior from code, tests, config, and docs. Mark inferred or unverified facts.

## Desired Behavior

Describe the behavior to preserve or implement.

## Users And Permissions

Identify users, roles, permissions, or access boundaries. Write `Unverified` if unknown.

## Data And Interfaces

List relevant data models, API routes, events, commands, files, or external services.

## Acceptance Criteria

- [ ] Each criterion must be testable.
- [ ] Include edge cases that define the requested behavior.
- [ ] Include compatibility expectations when existing behavior must remain.

## Test Plan

Map acceptance criteria to unit, integration, end-to-end, manual, lint, or type checks.

## Open Questions

List unresolved conflicts, assumptions, or user decisions needed before implementation.
```

## Writing Rules

- Prefer concrete behavior over intent.
- Keep acceptance criteria testable and scoped.
- Cite source files when a statement depends on current implementation.
- Do not use specs to justify unrelated refactors.
