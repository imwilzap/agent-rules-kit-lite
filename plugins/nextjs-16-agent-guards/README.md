# nextjs-16-agent-guards

Four short Cursor rules for a Next.js 16 App Router project in strict TypeScript.

| Rule | Applies | What it covers |
|---|---|---|
| `00-core.mdc` | always | Verify commands, working agreement, definition of done |
| `10-conventions.mdc` | `*.ts`, `*.tsx` | Async `params`/`cookies()`/`headers()`, `proxy.ts`, `revalidateTag` profile argument, `use cache`, Turbopack, known agent mistakes |
| `20-testing.mdc` | test files | Vitest vs async Server Components, Playwright on a production build |
| `30-security.mdc` | agent decides | Server Action authorization, data access layer, `server-only`, cookies |

Edit the Commands and Project map in `00-core.mdc` to match your repo (the commands assume pnpm), and delete rules that do not apply.

If you also keep an `AGENTS.md`, Cursor loads both, so keep one source. The repo has an `AGENTS.md`, a `CLAUDE.md` that imports it, and a Copilot file for the same stack: https://github.com/imwilzap/agent-rules-kit-lite

Limits: rules reduce mistakes, they do not guarantee an agent follows them, and they are not benchmarked. Facts were checked against the Next.js 16 documentation on 2026-10-29 (see `SOURCES.md` in the repo). Tools change quickly; check against your versions.

Disclosure: free Lite version of a paid pack by the same author (six stacks) at https://wilzap.gumroad.com/l/ofhjr . Not affiliated with Vercel or Cursor.
