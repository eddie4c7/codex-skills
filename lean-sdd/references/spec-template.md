# Slice Spec Template

Use this template for `docs/specs/<number>-<feature>.md`. Keep each spec focused on one vertical slice. Omit sections that do not apply.

```markdown
# [Slice Name]

## State

[Draft | Planned | In Progress | Implemented | Verified | Deferred]

## Purpose

[Why this slice matters to the user]

## User Story

As a [user], I want [capability], so that [value].

## Scope

- [Included behavior]

## Out Of Scope

- [Excluded behavior]

## User Flow

1. [User action]
2. [System response]
3. [User-visible result]

## Acceptance Criteria

- Given [context], when [action], then [observable result].
- Given [context], when [edge action], then [observable handling].

## Constraints

- [Product, technical, security, data, or UX constraint]

## Errors And Boundaries

- [Invalid input, empty state, loading state, failure state, permission boundary]

## Data, API, And UI Impact

- Data: [new or changed data shape]
- API: [new or changed endpoint/command/interface]
- UI: [new or changed screen/control/state]

## Test Strategy

- [Automated or manual verification mapped to acceptance criteria]

## Unresolved Questions

- [Question that does not block this slice or needs user decision]
```

Acceptance criteria must be observable and verifiable. Avoid vague completion criteria such as "works well", "is intuitive", or "handles errors properly" without concrete expected behavior.
