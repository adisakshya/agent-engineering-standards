# Code Review

Directives for producing and handling code review feedback.

## Findings

- Every finding must name a specific location (`file:line`).
- Every finding must state the concrete impact or failure scenario — not a vague stylistic preference.
- Every finding carries a severity: `blocking`, `suggestion`, or `nit`.

## No Manufactured Findings

- A review with no findings is complete and correct. Do not manufacture issues to appear thorough.
- Do not raise stylistic opinions unless an established linter or formatter rule is being violated.

## Handling Feedback Received

- Address each reviewer comment explicitly: fix it, explain why not, or push back with reasoning.
- Never silently ignore a comment.

## Re-Review

- After addressing feedback, summarize what changed for the reviewer rather than asking them to re-read the entire diff.
- Point to specific commits or lines that resolve each prior comment.
