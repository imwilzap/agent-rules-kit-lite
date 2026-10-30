# Sources

Every stack and tool statement in this Lite pack was checked against the vendor pages below on 2026-10-29. Tools change quickly: when a page and a rule disagree, trust the page and fix the rule (see `CHANGELOG.md`).

## Agent tools and file formats

- Claude Code memory and `CLAUDE.md`/`AGENTS.md` loading, `/memory`, `CLAUDE.local.md`, 200-line target: https://code.claude.com/docs/en/memory
- Cursor rules (`.mdc` types, `AGENTS.md`, size guidance): https://cursor.com/docs/context/rules
- GitHub Copilot repository instructions (`copilot-instructions.md`, `*.instructions.md`, `AGENTS.md`, `CLAUDE.md`): https://docs.github.com/en/copilot/how-tos/configure-custom-instructions/add-repository-instructions
- GitHub Copilot custom instructions concepts, and code review reading the head branch: https://docs.github.com/en/copilot/concepts/prompting-and-context/custom-instructions and https://docs.github.com/en/copilot/how-tos/copilot-on-github/use-copilot-agents/copilot-code-review
- Copilot code review no longer stops reading instruction files at 4,000 characters (2026-06-12): https://github.blog/changelog/2026-06-12-copilot-code-review-new-configurations-and-controls/

## Next.js 16 + TypeScript

- Upgrading to 16 (`proxy.ts`, async request APIs, `next lint` removal, Turbopack default and `--webpack`, `revalidateTag` profile argument, `updateTag`, `default.js` for parallel routes, `images.remotePatterns`/`localPatterns`, Node.js 20.9+, TypeScript 5.1+): https://nextjs.org/docs/app/guides/upgrading/version-16
- Data security (Server Actions as public endpoints, data access layer, DTOs): https://nextjs.org/docs/app/guides/data-security
- Testing with Vitest (async Server Components are not supported): https://nextjs.org/docs/app/guides/testing/vitest
- Bundled version-matched docs for agents (`node_modules/next/dist/docs/`): https://nextjs.org/docs/app/guides/ai-agents

## Python + FastAPI

- Lifespan events replace `on_event`: https://fastapi.tiangolo.com/advanced/events/
- FastAPI CLI (`fastapi dev`, `fastapi run`, entrypoint discovery): https://fastapi.tiangolo.com/fastapi-cli/
- CORS (wildcards and credentials): https://fastapi.tiangolo.com/tutorial/cors/
- Async tests and the lifespan caveat: https://fastapi.tiangolo.com/advanced/async-tests/
- SQLAlchemy asyncio (`expire_on_commit`, lazy loading, one session per task, `dispose`): https://docs.sqlalchemy.org/en/20/orm/extensions/asyncio.html
- Alembic autogenerate limits (renames, `alembic check`): https://alembic.sqlalchemy.org/en/latest/autogenerate.html
