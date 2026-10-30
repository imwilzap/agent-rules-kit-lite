# fastapi-agent-guards

Four short Cursor rules for a Python 3.12+ FastAPI service with Pydantic v2, SQLAlchemy 2.x, Alembic and pytest.

| Rule | Applies | What it covers |
|---|---|---|
| `00-core.mdc` | always | Verify commands (uv, ruff, mypy, pytest), working agreement, definition of done |
| `10-conventions.mdc` | `*.py` | Thin routers, Pydantic v2 APIs, `lifespan`, async SQLAlchemy loading, session scope, Alembic, known agent mistakes |
| `20-testing.mdc` | test files | `AsyncClient` and `lifespan`, dependency overrides, `alembic check` |
| `30-security.mdc` | agent decides | Authorization in dependencies, JWT pinning, upload limits, docs in production |

Edit the Commands in `00-core.mdc` to match your repo (they assume uv), and delete rules that do not apply.

If you also keep an `AGENTS.md`, Cursor loads both, so keep one source. The repo has an `AGENTS.md`, a `CLAUDE.md` that imports it, and a Copilot file for the same stack: https://github.com/imwilzap/agent-rules-kit-lite

Limits: rules reduce mistakes, they do not guarantee an agent follows them, and they are not benchmarked. Facts were checked against the FastAPI, SQLAlchemy and Alembic documentation on 2026-10-29 (see `SOURCES.md` in the repo). Tools change quickly; check against your versions.

Disclosure: free Lite version of a paid pack by the same author (six stacks) at https://wilzap.gumroad.com/l/ofhjr . Not affiliated with Tiangolo or Cursor.
