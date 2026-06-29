---
name: git-commit-message
description: Generate Git commit messages from staged changes. Use when the user asks Codex to inspect files already added to the Git index, read `git diff --cached` or staged file metadata, and draft a concise commit message without modifying the repository.
---

# Git Commit Message

Use this skill to draft a commit message from staged Git changes.

## Workflow

1. Confirm the current directory is inside the target Git repository.
2. Inspect staged changes only:
   - Prefer `git status --short`
   - Read `git diff --cached --stat`
   - Read `git diff --cached --name-status`
   - Read `git diff --cached --find-renames --find-copies --no-ext-diff`
3. Ignore unstaged and untracked changes unless the user explicitly asks to consider them.
4. If there are no staged changes, say that no commit message can be generated from the index.
5. Identify:
   - primary intent of the staged change
   - affected area or scope
   - behavior change versus docs/tests/chore/refactor
   - any breaking change, migration, or user-visible impact
6. Draft the message in the style that best matches the repository's recent commits when practical. Check recent style with `git log -n 10 --pretty=format:%s` if available.
7. Prefer a concise subject line under 72 characters.
8. Add a body only when it clarifies multiple changes, risk, migration notes, or important rationale.
9. Do not run `git add`, `git commit`, amend, reset, checkout, or mutate files unless the user explicitly asks.

## Portable Commands

Use plain Git commands so the workflow works across operating systems and shells:

```text
git status --short
git diff --cached --name-status --find-renames --find-copies
git diff --cached --stat
git log -n 10 --pretty=format:%s
git diff --cached --find-renames --find-copies --no-ext-diff
```

For large diffs, inspect the staged file list and stat first, then read the most relevant staged file diffs with:

```text
git diff --cached -- <path>
```

## Message Format

Default to this shape unless the repository strongly suggests another style:

```text
<type>(<scope>): <summary>

<body, only if useful>
```

Common types:

- `feat`: user-facing capability
- `fix`: bug fix
- `docs`: documentation-only change
- `test`: test-only change
- `refactor`: internal restructuring without behavior change
- `chore`: maintenance, config, metadata, generated files
- `build`: build system or dependency change
- `ci`: CI configuration change

If the change does not fit Conventional Commits, use a plain imperative subject such as:

```text
Update maintenance docs for project workflow
```

## Output

Return one primary recommendation and, when useful, one or two alternatives.

Include a short note about the evidence used, such as staged files or diff highlights. Keep the final answer concise and do not paste the whole diff.
