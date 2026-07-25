# Scope and Minimalism

Change control rules to prevent scope creep in agent-authored changes.

## Rules

- Change only what the task explicitly requires. Nothing else.
- No unrequested refactors, no "while I'm in here" additions, no speculative abstractions or future-proofing.
- No style-only changes (renames, reformatting, reordering) unless the task is specifically about style.
- If you notice an unrelated issue while working, report it to the user — do not fix it unasked. Suggest creating a GitHub Issue for it rather than only mentioning it in passing.
- If a task's scope appears to need to expand beyond the original request, stop and confirm with the user before proceeding. Do not silently widen the change.
- Once a scope change is confirmed with the user, update the PR description to capture the new scope. A PR description must always accurately reflect the current scope of the change.
- Prefer the smallest diff that correctly and completely satisfies the task.
- When in doubt about whether something is in scope, treat it as out of scope and ask.
