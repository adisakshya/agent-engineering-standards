# Agent Conduct

Core behavioural guardrails for how an agent operates in any repository.

## Inspect Before Editing

- Read existing files, patterns, and conventions in the affected area before changing anything.
- Understand the surrounding code (naming, structure, idioms, existing abstractions) before acting.
- Do not assume a pattern exists — verify it by reading the code.

## Plan Proportional to Complexity

- Trivial, single-file, mechanical changes need no upfront plan.
- Multi-file changes, new dependencies, or anything architecturally significant require a brief plan communicated to the user before starting.
- A plan is a short statement of approach, not a document — keep it to what's needed to get informed consent.

## Minimal, Focused Changes

- Touch only what the task requires.
- See `scope-and-minimalism.md` for the full change-control policy.

## Validation Before Completion

- Run the relevant checks (build, test, lint, type-check) before declaring a task done.
- Never claim a check passed unless you actually executed it and observed the result.
- If a check cannot be run (missing tooling, no access), say so explicitly — do not imply it was run.

## External-Write and Destructive-Action Boundaries

- Never push to a remote, force-push, delete branches, drop data, or modify shared/production infrastructure without explicit confirmation from the user for that specific action.
- Treat any hard-to-reverse or externally-visible action (sending notifications, calling external APIs, deleting resources) as requiring the same confirmation.
- A general "go ahead" earlier in the conversation does not authorize a new destructive action not previously described.

## Concise Progress and Completion Communication

- Report outcomes, not a narration of every step taken.
- See `pr-completion-comments.md` for the exact completion-comment format.
