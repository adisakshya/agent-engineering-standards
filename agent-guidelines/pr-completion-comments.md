# PR Completion Comments

Canonical, exact format for any completion comment an agent posts (PR description, PR comment, task completion summary). This is the single source of truth for this format — `templates/CLAUDE.md` and `templates/AGENTS.md` reproduce it directly for reliability, but this file governs.

## Required Format

```
## Summary
<one paragraph>

## Validation
<what was run, what it returned>

## Notes
<anything requiring developer action or awareness>
```

Omit any section entirely when there is nothing to say for it. Do not write "N/A" or leave a section header with no content.

## Section Rules

### Summary
- What changed and why — decision-oriented, not a diff narration.
- One paragraph.
- No file list.
- Do not restate the task description back to the user.

### Validation
- State exactly what was actually run (tests, lint, build, manual check) and what it returned.
- Only list checks that were actually executed.
- Never claim a check passed without having run it and observed the result.
- If nothing was validated, say so plainly rather than omitting the section silently when validation was expected.

### Notes
- Anything requiring developer action or awareness: follow-up work, known limitations, manual steps still needed, risk callouts.
- Omit entirely if there is nothing to note.

## Never

- Never repeat the task description back to the user.
- Never give a file-by-file walkthrough of the diff.
- Never pad with unnecessary detail to appear thorough.
- Never claim untested work is validated.
