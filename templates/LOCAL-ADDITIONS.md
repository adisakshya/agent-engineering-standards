# Local Additions — Worked Example

This file stays in the central `agent-engineering-standards` repository only. It is never copied into a consumer repository. It exists purely as a reference example of what to put in Section 8 (`[REPO-SPECIFIC]`) of a copied `CLAUDE.md` or `AGENTS.md`.

The example below is for a fictional Node/TypeScript API service, `orders-api`. Adapt the categories, not necessarily the exact content, to your repository.

---

## Example Section 8 content

```markdown
## 8. orders-api

### Tech Stack
Node.js 20, TypeScript (strict mode), Express, PostgreSQL via Prisma, deployed on AWS ECS.

### Commands
- Build: `npm run build`
- Test: `npm test` (unit) / `npm run test:integration` (requires local Postgres via `docker compose up -d db`)
- Lint: `npm run lint` (ESLint + `eslint-plugin-import`)
- Format: `npm run format` (Prettier — run before committing, CI fails on unformatted diffs)
- Type-check: `npm run typecheck`
- Run locally: `npm run dev` (starts on port 4000, requires `.env` — see `.env.example`)

### Architecture Notes
`orders-api` follows a layered structure: `routes/` handle HTTP concerns only and delegate immediately to `services/`, which contain business logic and are the only layer allowed to import from `repositories/` (Prisma-backed data access). Do not call Prisma directly from a route handler or a service that isn't the designated repository for that entity — this boundary is enforced by an ESLint import rule, not just convention.

### Local Conventions
- All new endpoints require a corresponding OpenAPI entry in `openapi/orders.yaml` before the PR is opened — CI validates the spec against the route table.
- Database migrations go through `prisma migrate dev --create-only`, are reviewed as a separate commit from the code that uses them, and are never edited after being merged to `main`.
- Feature flags are read exclusively through `src/lib/flags.ts`; do not read `process.env` for flag values anywhere else in the codebase.
```

---

## Notes on authoring your own Section 8

- Keep it to the four categories above (Tech Stack, Commands, Architecture Notes, Local Conventions) unless the repository genuinely needs more structure.
- Commands must be the real, current commands for the repository — verify them, don't guess.
- Architecture Notes: one paragraph is usually enough. State the boundary or invariant an agent is most likely to violate by not knowing it.
- Local Conventions: 2-4 bullets of repository-specific rules not covered by the central `agent-guidelines/` library. If a "local convention" is actually a general engineering practice, it belongs in a proposal to update the central guidelines instead, not buried in one repo's Section 8.
