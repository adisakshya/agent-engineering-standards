---
name: code-review
description: "Standards for producing and responding to code review feedback. Use this skill whenever you are reviewing a PR, reviewing a diff, responding to review comments, or addressing reviewer feedback. Triggers on: \"review this PR\", \"code review\", \"check my changes\", \"review this diff\", \"address the review comments\", \"respond to reviewer\", \"re-review\"."
---

# Code Review Standards

## Before Reviewing

Read the linked issue and PR description first to understand *what* the change is trying to accomplish and *why*. Reviewing without this context produces findings that miss the point.

## Regression Check

Every review must ask: does this change break anything that was previously working?

Check:
- Call sites affected by changed function signatures or behavior
- Dependent tests that may now have incorrect assumptions
- Adjacent behavior sharing state or control flow with the changed code

A regression is blocking regardless of how clean the new code looks in isolation.

## Findings

Every finding must include:

1. **Location**: `file:line` (exact)
2. **Concrete impact or failure scenario**: what breaks, how, and under what conditions — not "this could cause issues"
3. **Severity**:
   - `blocking` — must be fixed before merge; introduces a bug, regression, security issue, or violates a hard contract
   - `suggestion` — clearly better approach worth discussing; not a blocker
   - `nit` — minor clarity or style issue; lowest priority, author's call

Good finding:
> **blocking** — `auth/token.go:84`: `time.Now()` used for token expiry comparison without timezone normalization. In environments where server and client are in different timezones, valid tokens will be rejected. Use `time.Now().UTC()` throughout.

Bad finding:
> This could be better. Consider using UTC.

## No Manufactured Findings

A review with zero findings is complete and correct. Do not add soft concerns or stylistic preferences to appear thorough — manufactured findings erode trust in the real ones.

Do not raise style issues unless a configured linter or formatter rule is being violated. If the repo has a linter, run it rather than manually style-policing.

## Handling Feedback You Receive

Address every reviewer comment explicitly:
- **Fix it** → push the fix, point to the commit
- **Won't fix** → give clear reasoning
- **Disagree** → make your argument; do not silently ignore disagreement

Never skip a comment. If a comment is unclear, ask for clarification rather than guessing at intent.

## After Addressing Feedback

Summarize what changed — point to the specific commits or lines that resolve each prior comment. Do not ask the reviewer to re-read the entire diff.

Format:
Addressed all feedback from @reviewer:

blocking at auth/token.go:84 — fixed in abc1234, now using time.Now().UTC()
suggestion at config/loader.go:12 — agreed, refactored in def5678
nit at README.md:7 — updated wording in ghi9012