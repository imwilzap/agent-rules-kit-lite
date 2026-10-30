# Agent Rules Kit Lite: AGENTS.md, CLAUDE.md, Cursor rules and Copilot instructions for Next.js 16 and FastAPI

Free, short instruction files that stop AI coding agents (Claude Code, Cursor, GitHub Copilot, Codex and anything else that reads `AGENTS.md`) from repeating the mistakes they repeat in **Next.js 16 + TypeScript** and **Python + FastAPI** projects.

Each stack is the same rules in four formats, so you copy the one your tool reads:

| Tool | File |
|---|---|
| Any tool that reads AGENTS.md (Codex, Cursor, Copilot agents, Claude Code without a CLAUDE.md) | `AGENTS.md` |
| Claude Code | `CLAUDE.md` (one `@AGENTS.md` import, so rules load once) |
| Cursor | `.cursor/rules/*.mdc` (always-on core, glob-scoped conventions and tests, agent-decided security) |
| GitHub Copilot | `.github/copilot-instructions.md` |

## What the rules catch

Next.js 16 (from `stacks/nextjs-ts/AGENTS.md`):
- Reading `params.id` synchronously. In Next.js 16 `params`, `searchParams`, `cookies()` and `headers()` are Promises.
- Creating `middleware.ts`. Next.js 16 uses `proxy.ts` (Node.js runtime only; `middleware.ts` stays only for Edge).
- Running `next lint`, which was removed, and calling `revalidateTag('posts')` with one argument.
- Trusting `proxy.ts` as the only authorization check on Server Actions.

FastAPI (from `stacks/python-fastapi/AGENTS.md`):
- `requests` or `time.sleep` inside `async def`, which stalls the event loop.
- Pydantic v1 idioms (`.dict()`, `@validator`, `class Config`) in v2 code, and `@app.on_event` instead of `lifespan`.
- Lazy relationships and `expire_on_commit` on an async session (`MissingGreenlet`), and one session shared across `asyncio.gather` tasks.
- `allow_origins=["*"]` with `allow_credentials=True`.

## Install

Pick one stack and copy its files into your repo root, then edit **Commands** and **Project map** to match your project and delete rules that do not apply:

```bash
git clone https://github.com/imwilzap/agent-rules-kit-lite
cp -R agent-rules-kit-lite/stacks/nextjs-ts/. /path/to/your/repo/        # or stacks/python-fastapi
```

Cursor only: copy `stacks/<stack>/.cursor/rules/` into your repo.

Avoid loading the same rules twice: Cursor reads both `AGENTS.md` and `.cursor/rules`, so keep one of them. Claude Code reads `AGENTS.md` only when no `CLAUDE.md` exists in your working directory or above it; this pack's `CLAUDE.md` imports `AGENTS.md` for that reason. Check your tool's current docs for what it loads.

## Honest limits

- Rules reduce mistakes. They do not guarantee an agent follows them, and they do not replace tests, linters or review.
- Nothing here was benchmarked against specific models.
- Facts and file formats were checked against the vendor documentation listed in [`SOURCES.md`](SOURCES.md) on 2026-10-29. Tools change quickly; check against your versions, and open an issue (Rule correction) if something is wrong.
- Written with AI assistance and reviewed against those sources by the maintainer.

## Want the other stacks?

The paid [Agent Rules Kit](https://wilzap.gumroad.com/l/ofhjr) (CAD 9) adds Go, Rust, Django and React Native stacks, a 4-page playbook on writing and testing rules, and a QA checklist. This Lite pack stays free, is MIT licensed, and is identical to those two stacks in the paid kit.

[`CHANGELOG.md`](CHANGELOG.md) · [`SOURCES.md`](SOURCES.md) · [`LICENSE`](LICENSE) (MIT)
