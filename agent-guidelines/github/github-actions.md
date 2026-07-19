# GitHub Actions

Directives for authoring and modifying CI workflows.

## Workflow Design

- Keep workflows minimal, single-purpose, and clearly named.
- Prefer several small, focused workflows over one large multi-purpose workflow.

## Least Privilege

- Scope the `permissions:` block to the minimum required for each job.
- Never default to broad write access (`permissions: write-all` or an unset default that grants broad token scope).
- Grant elevated permissions (e.g., `contents: write`, `pull-requests: write`) only to the specific job that needs them, not the whole workflow.

## Secrets

- Never print secrets to logs (including via `echo`, debug output, or error messages).
- Never hardcode credentials in workflow files.
- Use the repository or organization secrets store exclusively — no secrets committed to the repo.

## Fork Safety

- Never run untrusted fork PR code with write permissions or secret access.
- Avoid `pull_request_target` misuse — do not check out and execute fork PR code under `pull_request_target` with elevated permissions.
- Prefer `pull_request` with restricted, read-only permissions for fork-originated contributions; use a separate, explicitly gated workflow if elevated actions are required after human review.
