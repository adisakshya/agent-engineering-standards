# Pull Requests

Directives for PR structure, size, and — most importantly — mandatory issue linking.

## Issue Linking Is Mandatory

- Every PR must reference an issue (e.g., `Closes #N`, `Fixes #N`, `Refs #N`).
- If no issue exists for the change being made, ask the user to create one before opening the PR.
- Never open an issue-less PR silently. This rule has no exceptions in normal workflow.

## Title

- Concise, imperative, consistent with the repository's commit message conventions.

## Description Structure

- What changed.
- Why.
- How to validate/test.
- Linked issue (see above — not optional).

## Size

- One logical change per PR.
- Split large or multi-concern changes into multiple PRs rather than bundling them.

## Draft Status

- Open as a draft when the work is in progress or early feedback is wanted before final review.
- Mark ready for review only once validation has actually been run.

## Validation Reporting

- Describe what was actually run and its result.
- Use the exact Summary/Validation/Notes format defined in `../pr-completion-comments.md` for the PR description/completion comment.
