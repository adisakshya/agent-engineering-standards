# Engineering Quality

Directives for implementation discipline, testing, dependency management, and security.

## Implementation and Architecture Discipline

- Follow existing patterns and conventions in the codebase.
- Do not introduce new frameworks, libraries, or architectural patterns without clear justification communicated to the user.
- Match the existing code style (naming, structure, error handling) rather than importing a different personal style.

## Testing and Regression Coverage

- Add or update tests for any behavior change.
- Run the full relevant test suite before declaring completion — not just the tests you wrote or touched.
- A change without adequate test coverage for the affected behavior is not complete; flag the gap if you cannot close it.

## Formatting, Linting, Type-Checking, and Builds

- Run the repository's formatter, linter, type-checker, and build before declaring a task done.
- Fix violations introduced by your change; do not fix unrelated pre-existing violations unless asked.
- Report the actual result of each check you ran — do not assume or guess.

## Dependency Management

- Check for an existing equivalent (in the codebase or already-installed dependencies) before adding a new dependency.
- Respect the repository's existing version-pinning conventions (exact pins, ranges, lockfiles).
- Justify any new dependency briefly in the completion notes.

## Security, Credentials, and Sensitive Data

- Never commit secrets, API keys, tokens, or credentials.
- Never introduce common vulnerability classes: SQL injection, XSS, command injection, path traversal, insecure deserialization, etc.
- Flag insecure patterns you encounter even when unrelated to the current task — report, do not silently fix unless asked (see `scope-and-minimalism.md`).

## Compatibility, Reliability, Idempotency, and External Side Effects

- Changes must be safe to re-run without unintended duplication or corruption.
- Preserve backward compatibility unless a breaking change was explicitly requested.
- Call out any external side effects a change introduces or triggers (API calls, emails, notifications, data writes, third-party webhooks) so the user is not surprised.
