---
name: branch-commit-pr-standards
description: "Standards for branch naming, commit messages, and pull request structure. Use this skill before creating a branch, making commits, or opening/updating a pull request. Triggers on: \"create a branch\", \"commit my changes\", \"open a PR\", \"create a pull request\", \"push my changes\", \"name this branch\", \"write a commit message\", \"PR description\"."
---

# Branch, Commit, and PR Standards

## Branches

### Naming

Format: `<type>/<issue-number>-<short-description>`

Types: `feat/`, `fix/`, `chore/`, `docs/`, `refactor/` — match repository convention if it differs.

Always include the GitHub issue number. The description should be short, kebab-case, descriptive.

Good: `feat/42-add-retry-logic`
Bad: `add-retry-logic`, `feature-branch`, `my-changes`

### Lifecycle Rules

- One branch = one logical unit of work. Do not stack unrelated changes.
- Branch from the repository's default branch unless the task explicitly targets a release or maintenance branch.
- Rebase or merge the latest base branch into your branch before opening a PR.
- Never delete branches — that is the user's responsibility.

If a task requires unrelated changes, split into separate branches and confirm with the user first.

## Commits

### Atomic Commits

One logical change per commit. A bug fix and a formatting pass are separate concerns — they belong in separate commits. Mixed commits make history hard to read and `git bisect` unreliable.

### Message Format

- **Subject line**: imperative mood, ≤72 characters (e.g., "Add retry logic to fetch client" — not "Added" or "Adding")
- **Body** (when needed): explain *why* — not *what* the diff already shows

Good subject lines:
- `Fix race condition in session token refresh`
- `Add pagination support to /api/users endpoint`
- `Remove deprecated v1 authentication middleware`

### History Hygiene

- No noise commits ("wip", "fix typo", "address feedback") in the final submitted history.
- Squash or clean up before opening a PR if the repository expects a clean, linear history.
- Never rewrite history on a shared branch without explicit user confirmation.

## Pull Requests

### Issue Linking Is Mandatory

Every PR must reference an issue. No exceptions.

- `Closes #N` — this PR fully resolves the issue
- `Fixes #N` — synonymous with Closes, typically for bugs
- `Refs #N` — one of multiple PRs working toward the same issue

If no issue exists, ask the user to create one before opening the PR. Never open a PR silently without a linked issue.

### Title

Concise, imperative, consistent with commit conventions. One line, no trailing period.

### Description

Use this exact structure for every PR description and completion comment:
Summary
<What changed and why — decision-oriented. No file list. No restating the task. Reference the closing issue: "Closes #N".>

Test Plan
<What was tested and how. State what was actually run (commands, test names, manual steps) and what it returned. Only list checks you actually executed.>

Review Notes
<Anything requiring developer action or awareness: follow-up work, known limitations, manual steps, risk areas, design tradeoffs. Omit entirely if nothing to note.>

Never:
- Repeat the task description back to the reader
- Walk through the diff file-by-file
- Claim a check passed without having run it
- Include session/conversation links or internal Slack links
### Size and Scope
- One logical change per PR. Split multi-concern changes — confirm with the user before splitting.
- Open as draft when work is in progress or early feedback is wanted.
- Mark ready for review only after validation has actually been run.