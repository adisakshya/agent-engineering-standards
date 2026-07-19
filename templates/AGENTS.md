<!-- Last synced: 2026-07-19 | Source: initial-scaffold -->

This file is the always-loaded entry point for Codex in this repository. It carries condensed, always-on rules and explicit pointers to the full guideline library in `agent-guidelines/`. Read the referenced file before performing the related action.

## 1. Agent Conduct

- Read existing files, patterns, and conventions before changing anything.
- Plan proportional to complexity: no upfront plan for trivial changes; a brief plan for multi-file or architecturally significant ones.
- Touch only what the task requires.
- Run relevant checks (build/test/lint/type-check) before declaring a task done. Never claim a check passed without having run it.
- Never push, force-push, delete branches, drop data, or touch shared/production infrastructure without explicit user confirmation for that specific action.
- Report outcomes concisely — do not narrate every step taken.

Full detail: agent-guidelines/agent-conduct.md

## 2. Scope and Minimalism

- Change only what the task explicitly requires.
- No unrequested refactors, no speculative abstractions, no "while I'm in here" additions.
- No style-only changes unless the task is specifically about style.
- Report unrelated issues you notice — do not fix them unasked.
- If scope appears to need to expand, stop and confirm with the user first.

Full detail: agent-guidelines/scope-and-minimalism.md

## 3. GitHub Workflow

- Branch naming: `<type>/<short-description>` (e.g., `feat/`, `fix/`, `chore/`, `docs/`, `refactor/`).
- Commits: one logical change per commit, imperative-mood subject line, no noise commits in final history.
- Issues: clear title, explicit problem statement, explicit acceptance criteria.
- PRs: one logical change per PR, description states what/why/how-to-validate, draft when work is in progress.
- Every PR must reference an issue (e.g., `Closes #N`). If no issue exists for the change, ask the user to create one before opening the PR. Never open a PR without a linked issue.

Before creating an issue: agent-guidelines/github/issues.md
Before branching or committing: agent-guidelines/github/branches.md, agent-guidelines/github/commits.md
Before opening or updating a PR: agent-guidelines/github/pull-requests.md

## 4. Engineering Quality

- Follow existing patterns and conventions; do not introduce new frameworks or architectural patterns without justification.
- Add or update tests for behavior changes; run the full relevant test suite, not just new tests.
- Run and pass formatting, linting, type-checking, and build before declaring completion.
- Check for existing equivalents before adding a dependency; respect existing version-pinning conventions.
- Never commit secrets or credentials; never introduce common vulnerability classes; flag insecure patterns even if unrelated to the current task.
- Preserve backward compatibility unless a breaking change was requested; call out external side effects.

Full detail: agent-guidelines/engineering-quality.md

## 5. PR Completion Comments

Use this exact format for every PR description or completion comment. Omit any section with nothing to say.

```
## Summary
<one paragraph, decision-oriented, no file list, no restating the task>

## Validation
<what was actually run and what it returned — only checks actually executed>

## Notes
<anything requiring developer action or awareness — omit if empty>
```

Never:
- Repeat the task description back to the user.
- Give a file-by-file walkthrough of the diff.
- Pad with unnecessary detail to appear thorough.
- Claim untested work is validated.

Full rules: agent-guidelines/pr-completion-comments.md

## 6. Code Review

- Every finding must name a specific location (`file:line`) and state the concrete impact or failure scenario.
- Every finding carries a severity: `blocking`, `suggestion`, or `nit`.
- A review with no findings is complete and correct — do not manufacture issues to appear thorough.
- No stylistic opinions unless an established linter/formatter rule is being violated.
- Address each reviewer comment explicitly: fix it, explain why not, or push back with reasoning — never silently ignore it.
- After addressing feedback, summarize what changed rather than asking the reviewer to re-read the whole diff.

Before reviewing a PR or code changes, apply: agent-guidelines/github/code-review.md

## 7. Documentation

- Update the README only when it documents something that actually changed (install, usage, configuration, commands).
- Keep documented commands accurate and runnable — verify before leaving them in place.
- Add a changelog entry when the repo maintains one and the change is user-facing.
- Write an ADR for significant architectural decisions only if the repo already has an ADR convention.
- Document observable behavior for users/developers, not internal implementation detail.

Full detail: agent-guidelines/documentation.md

## 8. [REPO-SPECIFIC]

<!-- Populate this section in each repository. Do not add content here in the central template. -->
<!-- See templates/LOCAL-ADDITIONS.md for a worked example. -->

## Response Format and Signature

- Use structured output: bullets, numbered lists, tables. No long prose paragraphs.
- Lead with the conclusion or outcome, not background or task restatement.
- Preserve information density — reduce words, not context. Do not omit information just to sound concise.
- End every response or comment you author with a signature footer:

  ---
  *— Codex*

  (Use `*— ChatGPT*` instead if that is the applicable agent name for this session.)
