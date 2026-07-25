# PR Completion Comments

Canonical, exact format for any completion comment an agent posts (PR description, PR comment, task completion summary). This is the single source of truth for this format — `templates/CLAUDE.md` and `templates/AGENTS.md` reproduce it directly for reliability, but this file governs.

## Required Format

```
## Summary
<one paragraph or bullet points>

## Validation
<what was run, what it returned>

## Test Plan
<what was tested and how>

## Notes
<anything requiring developer action or awareness>

## Review Notes
<context specifically useful to a human reviewer>
```

Omit any section entirely when there is nothing to say for it. Do not write "N/A" or leave a section header with no content.

## Section Rules

### Summary
- What changed and why — decision-oriented, not a diff narration.
- One paragraph or bullet points — whichever conveys the change more intuitively; not a requirement to force everything into a single prose paragraph.
- No file list.
- Do not restate the task description back to the user.
- Reference the GitHub issue the PR closes (e.g., `Closes #N`). If no issue exists for the change, confirm with the user whether to create one before opening the PR.

### Validation
- State exactly what was actually run (tests, lint, build, manual check) and what it returned.
- Only list checks that were actually executed.
- Never claim a check passed without having run it and observed the result.
- If nothing was validated, say so plainly rather than omitting the section silently when validation was expected.

### Test Plan
- Section must be named exactly "Test Plan".
- What was tested and how: concrete steps, commands, or scenarios actually exercised — not a bare assertion that "tests pass".
- Omit entirely if there is genuinely nothing to test.

### Notes
- Anything requiring developer action or awareness: follow-up work, known limitations, manual steps still needed, risk callouts.
- Omit entirely if there is nothing to note.

### Review Notes
- Context specifically useful to a human reviewer: risky areas, design tradeoffs, or anything they should pay special attention to.
- Omit entirely if there is nothing to note.

## Never

- Never repeat the task description back to the user.
- Never give a file-by-file walkthrough of the diff.
- Never pad with unnecessary detail to appear thorough.
- Never claim untested work is validated — this applies to both the Validation and Test Plan sections.
