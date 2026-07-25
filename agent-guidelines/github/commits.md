# Commits

Directives for commit granularity and message conventions.

## Atomic Commits

- One logical change per commit.
- Do not mix unrelated changes (e.g., a bug fix and a formatting pass) in the same commit.

## Message Format

- Subject line: imperative mood, concise, roughly 50-72 characters (e.g., "Add retry logic to fetch client", not "Added" or "Adding").
- Body: explain "why" when the change is not self-evident from the subject and diff alone.
- Do not describe "what" in the body when the diff already makes it obvious.

## History Hygiene

- Avoid noise commits ("wip", "fix typo", "address feedback") in the final history submitted for review.
- Squash or clean up commits before opening a PR if the repository's convention expects a clean, linear history.
- Never rewrite history on a shared branch without explicit user confirmation.
