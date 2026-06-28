# ADR Guidance And Template

Use this file before creating or updating `docs/adr/*.md`.

## When To Create An ADR

Create an ADR for changes involving meaningful decisions about:

- architecture or module boundaries
- persistence, migrations, or data ownership
- public APIs or compatibility
- external services or dependencies
- security, privacy, permissions, or compliance
- deployment, operations, performance, reliability, or rollback

Do not create an ADR for routine bug fixes, small UI copy changes, mechanical test additions, or implementation details already covered by an accepted spec.

## File Naming

Use a sortable number and concise kebab-case title:

- `docs/adr/0001-record-current-auth-boundary.md`
- `docs/adr/0002-use-existing-search-query-model.md`

Continue the existing numbering scheme if one exists.

## Template

```markdown
# ADR <number>: <decision title>

## Status

Proposed | Accepted | Superseded

## Context

Describe the current facts, constraints, conflicts, and forces. Mark inferred or unverified facts.

## Decision

State the chosen decision clearly.

## Consequences

List expected benefits, tradeoffs, risks, migration needs, compatibility effects, and follow-up work.

## Alternatives Considered

- Option: <name>
  - Why not: <reason>

## Evidence

- Code/docs/tests/config that support the context.
```

## Writing Rules

- Record the decision, not a broad design essay.
- Keep alternatives short and real.
- Do not use ADRs to authorize unrelated refactoring.
- If the user has not approved the decision, keep status as `Proposed`.
