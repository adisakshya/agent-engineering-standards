# agent-engineering-standards

Governed source of truth for shared engineering standards followed by AI coding agents (Claude Code, Codex) across repositories. The primary audience for every file in this repo is the agents themselves — content is written as concise, actionable directives, not human-facing explanatory prose.

## Why This Exists

AI coding agents repeatedly repeat the same avoidable mistakes across sessions and repositories: bloated PR comments that re-narrate the task, manufactured code-review findings, scope creep, inconsistent GitHub housekeeping, and no carry-over of working standards between sessions. This repository centralizes the fix once, in one place, instead of re-explaining it in every repository, every session.

## Architecture

Two layers, deliberately separated:

- **`agent-guidelines/`** — the single source of truth. Detailed, topic-scoped directive files (conduct, scope, engineering quality, documentation, PR comments, and the full GitHub lifecycle). Read by an agent on demand, via an explicit pointer.
- **`templates/`** — thin, always-loaded entry points (`CLAUDE.md` for Claude Code, `AGENTS.md` for Codex). These carry only condensed always-on rules plus explicit pointers into `agent-guidelines/`, so there is nothing to duplicate or drift between the entry point and the detail. The two highest-frequency failure modes — PR completion comments and code review — are fully reproduced in both templates as a reliability safety net, since those are the behaviors this repo exists to fix.

This split means guideline content lives in exactly one place. The templates reference it by path; they do not restate it.

## Directory Structure

```
agent-engineering-standards/
├── README.md
├── LICENSE
├── ADOPTION.md                        # Full copy/reference/override/update workflow
├── agent-guidelines/
│   ├── agent-conduct.md
│   ├── scope-and-minimalism.md
│   ├── engineering-quality.md
│   ├── documentation.md
│   ├── pr-completion-comments.md
│   └── github/
│       ├── issues.md
│       ├── branches.md
│       ├── commits.md
│       ├── pull-requests.md
│       ├── code-review.md
│       └── github-actions.md
└── templates/
    ├── CLAUDE.md                      # Always-loaded entry point for Claude Code
    ├── AGENTS.md                      # Always-loaded entry point for Codex
    └── LOCAL-ADDITIONS.md             # Worked example for a repo's local section
```

## Adoption Quickstart

Copy `templates/CLAUDE.md` and/or `templates/AGENTS.md`, plus the entire `agent-guidelines/` directory, into the target repository's root, then fill in each template's repository-specific section before committing. Adoption is a deliberate manual copy in this version — there is no auto-sync into consumer repositories.

See [`ADOPTION.md`](./ADOPTION.md) for the full copy, override, and update workflow, including how to pull in future changes from this repository.
