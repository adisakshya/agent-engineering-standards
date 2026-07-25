# Branches

Directives for branch naming and lifecycle.

## Naming Convention

- Format: `<type>/<issue-number>-<short-description>`.
- Types: `feat/`, `fix/`, `chore/`, `docs/`, `refactor/` (match repository convention if it differs).
- Always include the GitHub issue number so the branch can be properly linked to its issue — not the description alone.
- Description: short, kebab-case, descriptive of the change.

## One Branch, One Logical Unit of Work

- Do not stack unrelated changes on a single branch.
- If a task turns out to require unrelated changes, split into separate branches. Confirm with the user before splitting a task's work across multiple branches.

## Base Branch

- Branch from the repository's default branch unless the task explicitly targets a release or maintenance branch.
- Always rebase or merge/pull the latest base branch into your branch before opening a PR.

## Cleanup

- Never delete any branch, merged or unmerged. Branch deletion is the user's responsibility, not the agent's (see `../agent-conduct.md` — destructive-action boundaries).
