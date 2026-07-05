# Lean SDD Workflow

Use Lean SDD to keep new app development fast while preventing ambiguous scope, ad hoc technology choices, missing tests, and drift between documents and code.

## Global Approach

1. Prefer user-visible vertical slices over technical-layer tasks.
2. Keep specifications short and acceptance-driven.
3. Make reasonable assumptions when unknowns do not block progress; record them.
4. Ask only when an unknown changes product scope, technology direction, data handling, security posture, or verification feasibility.
5. Update specs before code for `start`, `slice`, and `change`.
6. Verify each slice before moving to the next.

## Mode: shape

1. Organize the user's idea, constraints, and target users.
2. List unknowns.
3. Record reasonable assumptions for non-blocking unknowns.
4. Draft `docs/product.md`-equivalent content using `product-template.md`.
5. Define what the MVP excludes.
6. Split the MVP into 3-7 vertical slices with user value, dependencies, state, and spec links.
7. Do not modify code.

Report the product definition, assumptions, unresolved questions, MVP exclusions, and proposed roadmap.

## Mode: start

### Phase 1: Shape

- Define product purpose, target users, MVP scope, exclusions, main flows, unknowns, and assumptions.
- Create or update `docs/product.md` only if useful for the project.

### Phase 2: Decide

- Prefer user-specified technology constraints.
- Select the minimum stack needed for the first working slice.
- Avoid unnecessary dependencies and future-proof architecture.
- Record active decisions in `docs/decisions.md`.
- If selecting unspecified technology, state choice, reason, alternatives, and assumptions.

### Phase 3: Slice

- Split MVP into vertical slices in `docs/roadmap.md`.
- Choose the first slice that can be verified fastest while proving user-visible value.
- Create the first spec under `docs/specs/`.
- Make acceptance criteria observable and testable.

### Phase 4: Plan

Before code edits, present:

- Documents to create or update
- First slice to implement
- Acceptance criteria
- Technical structure
- Planned files
- Test strategy
- Key assumptions
- Risks

Continue after presenting the plan unless the user asked for approval before edits.

### Phase 5: Implement

- Build only the minimum project and code required for the first slice.
- Do not create empty future features, unused generic infrastructure, or speculative abstractions.
- Remove starter placeholders and sample content that are not part of the product.
- Do not hard-code secrets.
- Follow existing package manager and conventions when a project already has them.

### Phase 6: Verify

- Add tests that map to acceptance criteria.
- Run available lint, type checks, tests, and build commands.
- Confirm the app can start when practical.
- Record checks that could not run and why.

### Phase 7: Report

Report documents created, slice implemented, acceptance criteria-to-implementation mapping, acceptance criteria-to-test mapping, commands and results, assumptions, unresolved items, and the next recommended slice.

## Mode: slice

1. Read `AGENTS.md`, product docs, decisions, roadmap, and relevant specs.
2. Check whether a spec already exists for the target feature.
3. Create a new spec for an independent new feature.
4. Update an existing spec for an extension of existing behavior.
5. Confirm acceptance criteria before code changes.
6. Identify impact area and planned files.
7. Implement the smallest vertical slice.
8. Add tests that map to acceptance criteria.
9. Run lint, type checks, tests, and build where available.
10. Update spec state and roadmap state.
11. Report spec, implementation, tests, and verification mapping.

## Mode: change

1. Read the existing spec for the target feature.
2. Compare current acceptance criteria with the new request.
3. Update the spec first.
4. Check backward compatibility impact.
5. Change code with the smallest diff.
6. Update existing tests and add regression tests as needed.
7. Avoid unrelated refactoring.
8. Report spec diff, implementation diff, and test diff.

## Mode: check

Compare:

- `product.md` and roadmap
- Roadmap and specs
- Specs and implementation
- Acceptance criteria and tests
- `decisions.md` and actual technology configuration

Classify mismatches as:

- Spec is stale
- Implementation does not satisfy spec
- Tests are missing or stale
- Technical decision is unrecorded
- Intent is unclear

Do not automatically perform broad fixes. Present minimal correction options.

## Roadmap Guidance

Write roadmap slices as user outcomes, not technical layers.

Bad slices:

- Create database
- Build API
- Build UI

Good slices:

- User can create an account
- User can post an article
- User can search posts

Each slice should include name, user value, dependencies, state, and linked spec.

## ADR Guidance

Create ADRs only when a decision is expensive to change, has multiple credible choices, affects security or data integrity, or has long-term project-wide impact. Keep routine decisions in `docs/decisions.md`.
