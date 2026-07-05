---

name: lean-sdd
description: Build new applications and MVPs using lightweight specification-driven development and small vertical slices. Use explicitly to shape a new app idea, create minimal product and feature specs, scaffold a new project, implement the next accepted slice, or check alignment between specs, code, and tests. Do not use for maintaining substantially completed existing projects, isolated bug fixes, or broad speculative architecture design.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# Lean SDD

Build new applications through lightweight specifications followed by focused AI implementation.

Do not design or implement the entire application at once.

## Modes

Interpret the first argument as one of:

* `shape`: define the product and MVP slices without changing code
* `start`: define the product, record initial decisions, create the first spec, and implement the first vertical slice
* `slice`: specify and implement one new vertical slice
* `change`: update an implemented feature by changing its spec before its code
* `check`: compare product documents, specs, code, and tests without making broad changes

When no mode is supplied, infer the safest mode. Prefer `shape` when the directory is empty and the request is exploratory. Prefer `check` when intent is unclear in a non-empty repository.

Use `project-maintenance` instead when the project is already substantially implemented and the main task is documenting or maintaining existing behavior.

## Principles

* Write only enough specification to implement and verify the next slice.
* Prefer observable acceptance criteria over lengthy prose.
* Build vertical user-value slices, not isolated technical layers.
* Keep the MVP scope and non-goals explicit.
* Record durable technical choices and their reasons.
* Implement only after the relevant spec is defined.
* Prefer the smallest end-to-end implementation that provides user value.
* Avoid speculative abstraction and unused infrastructure.
* Do not add features that were not requested.
* Keep documentation, code, and tests aligned.
* Clearly distinguish confirmed requirements, assumptions, and open questions.

## Project documents

Use these documents when relevant:

* `AGENTS.md`: repository-specific commands and constraints
* `docs/product.md`: problem, users, value, MVP scope, and non-goals
* `docs/roadmap.md`: ordered vertical slices and their states
* `docs/decisions.md`: currently active technical decisions
* `docs/specs/*.md`: intended behavior for individual slices
* `docs/adr/*.md`: durable, significant, difficult-to-reverse decisions

Do not create every document automatically. Use only what the project needs.

## Lightweight specification standard

A feature spec should normally contain:

* status
* purpose
* user story
* scope
* non-goals
* user flow
* acceptance criteria
* constraints
* important errors or edge cases
* data, API, and UI impact when applicable
* test approach
* assumptions or open questions

Omit irrelevant sections.

Acceptance criteria must be observable and verifiable.

Prefer:

* Given a signed-in user with no existing records
* When the user submits a valid maintenance record
* Then the record appears in the vehicle history
* And the persisted record contains the submitted date and mileage

Avoid:

* The feature should work correctly
* The UI should be user-friendly
* The system should be robust

## Vertical-slice rule

Divide work by user-visible capability.

Prefer:

* User can create an account
* User can register a vehicle
* User can save a maintenance record
* User can view maintenance history

Avoid roadmap items that only describe technical layers:

* Create database
* Create API
* Create frontend
* Add state management

A slice may include UI, API, persistence, and tests when all are required to deliver the behavior.

## Shape mode

1. Identify the problem, target users, and desired outcome.
2. Separate confirmed requirements from assumptions.
3. Define the smallest useful MVP.
4. Explicitly list non-goals.
5. Identify the primary user journeys.
6. Divide the MVP into approximately three to seven vertical slices.
7. Identify dependencies and major risks.
8. Produce or update `docs/product.md` and `docs/roadmap.md`.
9. Do not modify application code.

Do not block on minor ambiguity. Use a reasonable assumption and record it.

## Start mode

### Understand

1. Read applicable repository instructions.
2. Inspect the working directory and existing files.
3. Determine whether the directory is empty, partially scaffolded, or already an established application.
4. If it is already substantially implemented, recommend `project-maintenance` rather than silently applying a greenfield process.

### Shape

1. Define the product problem and target user.
2. Define MVP scope and non-goals.
3. Define the main user flow.
4. Divide the MVP into vertical slices.
5. Create or update:

   * `docs/product.md`
   * `docs/roadmap.md`

### Decide

1. Respect user-specified technologies and constraints.
2. Choose only technologies needed for the first slices.
3. Prefer simple, conventional project structures.
4. Record choices and short reasons in `docs/decisions.md`.
5. Mark inferred choices as assumptions.
6. Create an ADR only for a significant, durable, or difficult-to-reverse decision.

### Specify

1. Select the smallest first slice that proves the application can work end to end.
2. Create `docs/specs/<number>-<feature>.md`.
3. Define observable acceptance criteria.
4. Include meaningful failure and boundary cases.
5. Describe only the interfaces and data required for this slice.

### Plan

Before changing application code, report:

* product and MVP summary
* first vertical slice
* acceptance criteria
* proposed technology choices
* documents to create or update
* files expected to change
* test strategy
* assumptions
* risks

### Implement

1. Scaffold the minimum viable project.
2. Implement only the selected slice.
3. Do not create empty modules for future features.
4. Do not add generic infrastructure without a current use.
5. Do not leave demo code or irrelevant placeholders.
6. Keep secrets outside source control.
7. Follow established repository and package-manager conventions.
8. Make changes small enough to review.

### Verify

Run applicable:

* focused automated tests
* lint
* formatting checks
* type checks
* build checks
* application startup or smoke checks

Do not claim a check passed unless it was executed successfully.

Map each acceptance criterion to an automated test or an explicit manual verification.

### Complete

Update the slice and roadmap status only after verification.

Report:

* documents created or updated
* implementation completed
* acceptance-criterion-to-code mapping
* acceptance-criterion-to-test mapping
* commands executed and results
* assumptions made
* unresolved questions
* remaining risks
* recommended next slice

## Slice mode

1. Read `AGENTS.md`, product documents, roadmap, decisions, relevant specs, implementation, and tests.
2. Confirm that the requested work belongs to the current MVP.
3. Decide whether to create a new spec or update an existing one.
4. Define or update acceptance criteria before editing code.
5. Report the plan, affected files, risks, and tests.
6. Implement the smallest complete vertical slice.
7. Add or update focused tests.
8. Run applicable verification.
9. Update the spec and roadmap state.
10. Report documentation, code, and test alignment.

Create a new spec when the capability can be independently explained, tested, released, permissioned, or removed.

Update an existing spec when extending or changing the same user capability.

## Change mode

1. Read the current spec and implementation.
2. Identify the behavioral difference between the existing and requested states.
3. Update the spec before implementation.
4. Check compatibility, migration, and data implications.
5. Implement the smallest necessary code change.
6. Update existing tests and add regression coverage.
7. Avoid unrelated refactoring.
8. Report the spec, implementation, and test differences.

## Check mode

Compare:

* product against roadmap
* roadmap against specs
* specs against implementation
* acceptance criteria against tests
* decisions against actual configuration and dependencies

Classify discrepancies as:

* product or roadmap stale
* spec stale
* implementation incomplete or incorrect
* tests incomplete or stale
* technical decision unrecorded
* intended behavior unclear

Recommend the smallest corrective action. Do not automatically rewrite the whole project.

## ADR rule

Create an ADR only when a decision:

* is expensive to reverse
* has multiple credible alternatives
* affects security, privacy, or data integrity
* affects the architecture across multiple slices
* is likely to be questioned later

Do not create an ADR for routine implementation details.

## Prohibited behavior

* Do not implement the entire MVP in one pass.
* Do not produce a comprehensive detailed design for every future feature.
* Do not implement without acceptance criteria.
* Do not add hypothetical extensibility.
* Do not introduce microservices without a current requirement.
* Do not add dependencies merely for convenience.
* Do not switch the user’s chosen stack without explaining the conflict.
* Do not perform unrelated refactoring.
* Do not hide uncertainty behind confident language.
* Do not mark a slice complete without verification.

## Definition of done for a slice

A slice is complete only when:

* a current spec exists
* acceptance criteria are observable
* implementation satisfies the acceptance criteria
* each acceptance criterion has a test or explicit manual check
* applicable verification has passed
* documentation matches implementation
* assumptions and remaining risks are recorded

## References

Use:

* `references/product-template.md`
* `references/spec-template.md`
* `references/decision-template.md`
* `references/workflow.md`
