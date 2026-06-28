---
name: project-maintenance
description: Explicitly-invoked workflow for maintaining existing, partly completed software projects without broad redesign. Use when the user calls $project-maintenance bootstrap, change, inspect, or docs-check to document current code as fact, reconcile docs/specs/tests, classify requested changes, update specs or ADRs before implementation, and make minimal tested changes.
---

# Project Maintenance

Use this skill only for explicit `$project-maintenance ...` requests unless the user clearly asks for this exact maintenance workflow.

## Core Rules

- Treat the current code as the primary observable fact.
- Do not decide that code or documentation is correct when they conflict. Report the contradiction, cite evidence, and ask how to treat it when the answer changes behavior or scope.
- Do not perform broad redesign, broad refactoring, unrelated cleanup, unnecessary renames, unnecessary abstraction, avoidable file splitting, or dependency additions/updates.
- Preserve currently working behavior unless the accepted change explicitly replaces it.
- Mark uncertain findings as assumptions, inferred, or unverified.
- Create an implementation plan before code edits.
- Add or update tests only around the changed behavior. Do not attempt whole-project test coverage in one pass.
- Run available tests, lint, and type checks when practical.
- Finish by mapping specs, implementation, tests, and verification results.

## Mode Selection

- `bootstrap`: Use for a project that lacks maintenance documentation. Analyze and create docs only.
- `change "<request>"`: Use for a requested implementation change in a project that already has docs or needs docs established around the change.
- `inspect`: Use for read-only assessment of structure, risks, documentation state, or likely next maintenance work.
- `docs-check`: Use to compare current docs/specs/ADRs against code and report gaps or contradictions.

Read `references/documentation-rules.md` before creating or updating docs. Read `references/spec-template.md` before writing specs. Read `references/adr-template.md` before writing ADRs.

## Bootstrap Mode

1. Read repository instruction files, README files, build/test configuration, dependency manifests, and existing docs.
2. Inspect directory structure, major features, data models, APIs, external services, entry points, and tests.
3. Identify unknowns, technical debt, and doc/code contradictions.
4. Present the documents to create or update and the evidence for each.
5. If explicit approval is not required by the user, create documentation only:
   - `docs/overview.md`
   - `docs/decisions.md`
   - `docs/specs/`
   - `docs/adr/`
6. Do not change production or test code.
7. Label anything not proven from code/config/docs as inferred or unverified.

## Change Mode

1. Read `AGENTS.md`, README files, `docs/overview.md`, `docs/decisions.md`, relevant specs, and relevant ADRs.
2. Inspect the target code and tests.
3. Classify the change as one or more of:
   - existing behavior change
   - independent new feature
   - bug where implementation violates an existing spec
   - internal-only implementation change
   - important technical decision
4. Before code edits, present:
   - classification and reason
   - docs to create or update
   - acceptance criteria
   - impact area
   - planned files
   - risks
   - test strategy
5. Update required specs, ADRs, overview, or decisions before implementation.
6. Implement the smallest change that satisfies the accepted spec.
7. Add or update focused tests.
8. Run relevant tests, lint, and type checks.
9. Report classification, documentation changes, code changes, acceptance criteria to test mapping, verification results, unresolved items, and remaining risk.

## Inspect And Docs-Check

- `inspect`: Stay read-only. Summarize architecture, documentation state, risk areas, likely missing specs, and recommended next steps.
- `docs-check`: Stay read-only unless the user asks to fix docs. Compare docs/specs/ADRs with code and tests, then report matches, gaps, contradictions, and confidence.

## Reference Loading

- Use `references/documentation-rules.md` for doc creation/update criteria and conflict handling.
- Use `references/spec-template.md` when deciding whether to update or create a spec and when drafting spec content.
- Use `references/adr-template.md` when an important technical decision is involved.
