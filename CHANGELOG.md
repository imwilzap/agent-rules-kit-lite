# Changelog (Lite)

Format follows Keep a Changelog. Dates are calendar dates.

## 1.0.0 (revised 2026-10-29)

Technical review against current vendor documentation (see `SOURCES.md`), with corrections and new rules for both lite stacks. File names and layout are unchanged, so you can diff against an earlier copy.

### Fixed
- Copilot file now includes the **Testing** rules. Earlier builds had them in `AGENTS.md` and Cursor only, so the four formats differed.
- FastAPI CORS rule now covers `allow_origins`, `allow_methods`, and `allow_headers` with credentials (the docs forbid wildcards for all three).
- Next.js: `middleware.ts` is described as deprecated, and `proxy.ts` as Node.js-only.

### Added
- **Next.js 16**: `revalidateTag` profile argument and `updateTag`, `default.js` for parallel routes, Turbopack versus `--webpack`, `images.remotePatterns` and `localPatterns`, `use cache` request-API pitfall, `NEXT_PUBLIC_*` build-time inlining, `vitest run` versus watch mode, Vitest and async Server Components, Playwright against a production build, data access layer and DTO rules, `serverActions.allowedOrigins`, bundled version-matched docs.
- **FastAPI**: `fastapi dev` and `fastapi run` notes, `expire_on_commit=False`, `lazy="raise"`, one `AsyncSession` per task, `asyncio.gather` pitfall, `AsyncClient` not running `lifespan`, Alembic rename and autogenerate limits, naming conventions, `alembic check`, `extra="forbid"`, JWT algorithm pinning, disabling docs in production.
- `CLAUDE.md` notes on hooks for enforcement, `CLAUDE.local.md`, and `/memory`.
- `SOURCES.md` listing every vendor page checked, and this changelog.

### Changed
- Version-specific claims cite `SOURCES.md`.
- Rules that duplicated generic advice were merged or tightened. Every rule is still one sentence under 420 characters, and `AGENTS.md` files stay under 110 lines.
