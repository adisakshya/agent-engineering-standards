# Adoption Guide

How to bring these standards into a repository, keep them current, and add repository-specific content without polluting the central library.

## New Repository

```bash
# 1. Copy the entry-point file(s) — whichever agent(s) you use in this repo
cp path/to/agent-engineering-standards/templates/CLAUDE.md ./CLAUDE.md
cp path/to/agent-engineering-standards/templates/AGENTS.md ./AGENTS.md   # if using Codex

# 2. Copy the guideline library — required, not optional.
#    Templates reference these files by relative path (agent-guidelines/...).
#    This form copies contents into the destination and is safe to rerun
#    even if ./agent-guidelines already exists (it won't nest directories).
mkdir -p ./agent-guidelines
cp -r path/to/agent-engineering-standards/agent-guidelines/. ./agent-guidelines/

# 3. Fill in Section 8 (REPO-SPECIFIC) in each copied template.
#    See templates/LOCAL-ADDITIONS.md in the central repo for a worked example.
#    Populate: Tech Stack, Commands (build/test/lint/format/run), Architecture Notes, Local Conventions.

# 4. Commit
git add CLAUDE.md AGENTS.md agent-guidelines/
git commit -m "chore: add agent instructions and guidelines from central standards"
```

`agent-guidelines/` must be copied in full and placed at the repository root — the templates reference it by relative path (`agent-guidelines/...`), and a partial or missing copy breaks every pointer in the template.

## Existing Repository

Follow the same steps as above, with one addition: before committing, read any `CLAUDE.md`/`AGENTS.md` already in the repository and migrate its local conventions into the new Section 8. Do not discard existing local context — carry forward anything repository-specific that isn't already covered by the central `agent-guidelines/` library.

## Updating From Central Standards

1. Diff the central repo's current `agent-guidelines/` directory against the local copy, and the central `templates/CLAUDE.md` / `templates/AGENTS.md` against the local copies.
2. **Guideline changes apply directly.** No local content lives inside `agent-guidelines/` — it is a pure mirror of the central library, so any diff there should be applied as-is.
3. **Template changes apply everywhere except Section 8.** Section 8 is always local and is always preserved across an update.
4. Update the sync header date at the top of each updated template (`<!-- Last synced: YYYY-MM-DD | Source: <short commit hash or reference> -->`).
5. Commit all changed files together in one commit.

There is intentionally no automated sync in V1 — this is a manual, deliberate process. Every standards update is a decision the maintainer reviews before it lands in a given repository.

## Authoring Discipline (for anyone editing the central repo)

1. Edit the relevant `agent-guidelines/*.md` file — this is the only place the detailed rule lives.
2. If the change affects a condensed summary, or the fully-reproduced Section 5 (PR Completion Comments) or Section 6 (Code Review), update both `templates/CLAUDE.md` and `templates/AGENTS.md` identically.
3. Update the sync header date in both templates.
4. Commit all changed files together in one commit — a commit touching one template but not the other for a Section 5/6 change is a visible signal of broken discipline.

Verify structural mirroring before committing:

```bash
diff <(grep "^## " templates/CLAUDE.md) <(grep "^## " templates/AGENTS.md)
```

This should show no differences — both templates must carry the same section headings in the same order.

## Verification Note (Read Before Relying on This for Automated Review)

Whether an agent reliably follows an `agent-guidelines/...` pointer during automated/non-interactive review surfaces (GitHub Actions-triggered review, bot-triggered PR review, cloud review tasks) has **not been empirically verified**. This is why Sections 5 and 6 of the templates fully reproduce their operative rules inline rather than relying solely on a pointer — it reduces, but does not eliminate, dependence on this unverified behavior for the two highest-frequency failure modes.

Before relying on this setup for a critical cross-agent review workflow (e.g., Claude reviewing a Codex-authored PR via a GitHub Action, or vice versa), run a scratch-repo test: add the full `templates/` + `agent-guidelines/` structure to a throwaway repository, trigger a PR review through your actual invocation path for each agent, and confirm the guideline pointers are actually opened and followed — not just the reproduced sections.
