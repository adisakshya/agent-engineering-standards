---
name: github-actions-standards
description: "Standards for authoring, modifying, and debugging GitHub Actions CI/CD workflows. Use this skill whenever you are creating a new workflow, editing an existing one, debugging CI failures, or reviewing workflow security. Triggers on: \"create a workflow\", \"add CI\", \"GitHub Actions\", \"write a workflow file\", \"fix the CI\", \"debug this workflow\", \"workflow permissions\", \"secrets in CI\", \"fork PR workflow\", \"pull_request_target\"."
---

# GitHub Actions Standards

## Workflow Design

Keep workflows minimal, single-purpose, and clearly named. A workflow that runs lint, test, build, and deploy is four workflows in a trench coat.

Split by concern:
- `lint.yml` — static analysis and formatting checks
- `test.yml` — unit and integration tests
- `build.yml` — compilation or bundling
- `release.yml` — publishing or deployment

Define dependencies between workflows where applicable — use `workflow_run` or job `needs:` to avoid wasting CI minutes on a build job when lint already failed.

## Least Privilege

Scope the `permissions:` block to the minimum required for each job. Unset permissions default to broad token scope in many repositories — never rely on the default.

```yaml
# Deny everything at the workflow level
permissions: {}

jobs:
  deploy:
    permissions:
      contents: write  # only this job needs write access
```

Never use `permissions: write-all`. Grant elevated permissions (`contents: write`, `pull-requests: write`) only to the specific job that needs them, not the whole workflow.

## Secrets

- Never print secrets to logs — not via `echo`, debug output, or error messages. Do not depend on GitHub's automatic secret masking.
- Never hardcode credentials in workflow files, even encoded or "obfuscated."
- Use the repository or organization secrets store exclusively: `${{ secrets.MY_SECRET }}`.
- Audit `env:` blocks — do not assign a secret to a plain env variable that later gets logged.

## Fork Safety

`pull_request` events from forks run with read-only permissions and no secret access by default — this is the safe default. The danger is `pull_request_target`.

Never check out and execute fork PR code under `pull_request_target` with elevated permissions. This is a critical RCE vector: fork code runs in the privileged context of the target repo.

If elevated actions are needed after a human reviews a fork PR (e.g., post a comment, deploy a preview), use a separate workflow gated on a label or manual approval — never automatically triggered by the fork PR itself.

Safe pattern for fork PRs that need secrets:

```yaml
# Workflow 1: runs on pull_request — no secrets, safe to run fork code
on: pull_request
jobs:
  test:
    permissions:
      contents: read
    steps:
      - uses: actions/checkout@v4
      - run: npm test
```

```yaml
# Workflow 2: triggered by workflow_run after tests pass + maintainer gates access
on:
  workflow_run:
    workflows: ["Test"]
    types: [completed]
```

## General Authoring Practices

- Pin action versions to a specific SHA or immutable tag for reproducibility and supply chain safety. Prefer `actions/checkout@v4` with a commit SHA over `@main` or `@latest`.
- Cache dependencies when possible (`actions/cache`) to reduce build time and cost.
- Validate workflow syntax locally before pushing (e.g., using the GitHub Actions schema linter or `act`).
