# Branches

Directives for branch naming and lifecycle.

## Naming Convention

- Format: `<type>/<short-description>`.
- Types: `feat/`, `fix/`, `chore/`, `docs/`, `refactor/` (match repository convention if it differs).
- Description: short, kebab-case, descriptive of the change — not the ticket number alone.

## One Branch, One Logical Unit of Work

- Do not stack unrelated changes on a single branch.
- If a task turns out to require unrelated changes, split into separate branches.

## Base Branch

- Branch from the repository's default branch unless the task explicitly targets a release or maintenance branch.
- Rebase or merge from the base before opening a PR if the branch has drifted significantly.

## Cleanup

- Delete branches after merge when the repository's convention calls for it.
- Never delete a branch that has not been merged without explicit user confirmation (see `agent-conduct.md` — destructive-action boundaries).
