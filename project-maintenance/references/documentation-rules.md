# Documentation Rules

Use these rules when `$project-maintenance` creates, checks, or updates maintenance documentation.

## Bootstrap Documents

Create only files that can be supported by repository evidence.

- `docs/overview.md`: Describe the current system, entry points, runtime/build commands, major directories, core workflows, data model, APIs, external services, and test/lint/typecheck commands.
- `docs/decisions.md`: Record observable design decisions already present in the codebase. Link ADRs when they exist. Mark inferred decisions as inferred.
- `docs/specs/`: Create one spec per user-visible feature or independently testable capability discovered during bootstrap when there is enough evidence.
- `docs/adr/`: Create ADRs only for decisions with meaningful architecture, storage, API, dependency, deployment, security, or compatibility consequences.

## Evidence Labels

Use consistent labels:

- `Observed`: directly supported by code, tests, config, README, or existing docs.
- `Inferred`: likely from structure or naming but not directly stated.
- `Unverified`: plausible but not confirmed.
- `Conflict`: docs, tests, or code disagree.

## Conflict Handling

When code and documentation conflict:

1. Cite the conflicting files and the behavior each implies.
2. Do not silently rewrite the spec to match code if that changes intended behavior.
3. Ask for the intended source of truth when the conflict affects implementation, tests, data, or user-facing behavior.
4. If continuing is safe, isolate non-conflicting documentation changes and list the conflict as unresolved.

## Change Documentation Criteria

Update existing documentation when the request changes documented behavior, acceptance criteria, workflows, data, API contracts, or operational assumptions.

Create new documentation when the request introduces an independently explainable feature, a separate lifecycle, a new actor or permission boundary, a new data object, a new integration, or a decision that should be reusable later.

Do not update specs for a bug fix that only makes code conform to an existing spec, unless the spec is ambiguous and needs clarification.

Do not update specs for internal-only changes that preserve user-visible behavior, unless a technical decision or operational constraint must be recorded.

## Minimal Change Discipline

- Prefer narrowly scoped edits over sweeping cleanup.
- Avoid changing formatting in unrelated files.
- Avoid dependency changes unless required by the accepted spec.
- Preserve public interfaces unless the accepted spec says otherwise.
- Keep test additions focused on the changed behavior and nearby regression risk.

## Final Report Checklist

Include:

- Mode used.
- Change classification, when applicable.
- Docs created or updated.
- Code files changed.
- Acceptance criteria and the tests or checks that cover each item.
- Commands run and outcomes.
- Unresolved conflicts, assumptions, unverified facts, and remaining risks.
