---
name: github-issue-standards
description: "Standards for creating, triaging, and closing GitHub issues. Use this skill whenever you are about to create a new GitHub issue, triage existing issues, update issue state, or close an issue. Triggers on: \"create an issue\", \"open a ticket\", \"file a bug\", \"add a feature request\", \"close this issue\", \"triage\", \"link these issues\", \"add a label\"."
---

# GitHub Issue Standards

## Before Creating

Search existing issues first to avoid duplicates. A duplicate fragments discussion and wastes team time.

## Creation

**Title**: State the problem or feature specifically — not a vague summary. A good title answers "what is wrong" or "what needs to be built" in one line.

**Body must include:**
- Explicit context (system, component, version, environment)
- A clear problem statement or feature description
- Actionable items required to resolve it
- Acceptance criteria: how will you know when this issue is done?

**Bug reports must include:**
1. Numbered reproduction steps (specific, not "just try it")
2. Expected behavior
3. Actual behavior

**Feature requests must include:**
- Clearly bounded scope: what is included and explicitly what is not
- Motivation — why this is needed, not just desired

**Large issues:** Break into smaller sub-issues with parent-child relationships. One mega-issue makes progress untraceable and PRs oversized.

## Triage

- Apply labels (type, priority, area) from the repository's existing label set — do not invent new labels without checking what already exists.
- Link related issues and PRs explicitly via `#N` references or GitHub's linked issues feature — not just described in prose.

## Closure

- Close only when the stated acceptance criteria are met — not just when a PR is merged.
- Reference the PR or commit that resolved it (e.g., "Closed by #42").
- Set `state_reason` (completed / not_planned / duplicate) when the tooling supports it.

## Quality Bar

Before submitting: can someone unfamiliar with the context read this issue and know exactly what needs to be done and how to verify it's done? If not, fill the gaps.