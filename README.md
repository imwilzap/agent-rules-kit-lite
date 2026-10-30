# Agent Rules Kit Lite

Free instruction files for AI coding agents, for two stacks: **Next.js 16 + TypeScript (App Router)** and **Python + FastAPI**. Each stack comes in four formats so you can use the one your tool reads: `AGENTS.md`, `CLAUDE.md` (imports `AGENTS.md`), `.cursor/rules/*.mdc`, and `.github/copilot-instructions.md`.

The files are short (under 90 lines for `AGENTS.md`). Every line is a fact about the repo, a guard against a known agent mistake, or a verification step. They were checked against vendor documentation on 2026-10-29; see `SOURCES.md`.

## A real excerpt

From `stacks/nextjs-ts/AGENTS.md`, section "Known agent mistakes":

```md
- Typing `{ params }: { params: { id: string } }` and reading `params.id` synchronously. Await the Promise instead.
- Creating `middleware.ts` in a Next.js 16 project. It is deprecated and cannot be configured for the Node.js runtime. Use `proxy.ts`, and keep `middleware.ts` only if the project must run on the Edge runtime.
- Running `next lint`. Use the repo's `lint` script.
- Calling `revalidateTag('posts')` with one argument, which is a TypeScript error in Next.js 16. Pass a cacheLife profile or use `updateTag` in a Server Action.
```

## Install

```bash
git clone https://github.com/imwilzap/agent-rules-kit-lite.git
cp -R agent-rules-kit-lite/stacks/nextjs-ts/. /path/to/your/repo/
# or: cp -R agent-rules-kit-lite/stacks/python-fastapi/. /path/to/your/repo/
```

Then open `AGENTS.md`, fix **Commands** and **Project map** to match your repo, and delete rules that do not apply.

Keep only the files your tool reads, so the same rules are not loaded twice:

- Claude Code loads `CLAUDE.md`, which here imports `AGENTS.md`. Keep both files, or edit them together.
- Cursor reads `.cursor/rules/*.mdc` and also `AGENTS.md`. Keep one of them.
- GitHub Copilot reads `.github/copilot-instructions.md`, and its agents also read `AGENTS.md`.
- Check each tool's current documentation for which files it loads. They change.

## What this does not do

Rules guide an agent. They do not guarantee it follows them, and they have not been benchmarked against specific models. Keep your tests, linters, and code review in place.

## The full kit

The full Agent Rules Kit (CAD 19) adds Go, Rust, Django, and React Native stacks (six in total), a playbook PDF on writing, testing, and maintaining rules, a QA checklist, and a changelog: https://wilzap.gumroad.com/l/ofhjr.

The same free pack is also on Gumroad: https://wilzap.gumroad.com/l/dysxru

## License

This repo uses a custom Lite license, in `LICENSE.md` (not a standard open-source license). In short: you may use, copy, modify, and share the files, including in commercial projects. You keep the license file with unmodified copies and you may not sell the pack. A standard MIT license would allow reselling, which is not the intent, so GitHub shows the license as "Other".

Corrections are welcome as issues. See `CHANGELOG.md` for what changed.
