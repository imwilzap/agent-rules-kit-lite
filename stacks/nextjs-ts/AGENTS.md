# AGENTS.md: Next.js 16 + TypeScript (App Router)

Instructions for AI coding agents working in a Next.js 16 App Router project written in strict TypeScript with React 19.
Every line is a fact, a guard against a known agent mistake, or a verification step. Edit **Commands** and **Project map** to match this repo, and delete rules that do not apply.

## Commands
Run from the repo root. Commands assume pnpm. Swap in npm, yarn, or bun to match the lockfile. `pnpm lint` should run `eslint .` because `next lint` was removed in Next.js 16, and `next build` no longer lints. `pnpm test` must run once and exit (`vitest run` or `jest`); bare `vitest` starts watch mode and never returns.

**Verify** (run these before you say a task is done):
- Typecheck: `pnpm exec tsc --noEmit`
- Lint: `pnpm lint`
- Test: `pnpm test`
- Build: `pnpm build`

**Other** (run only when asked or when the task needs it):
- Install: `pnpm install`
- Dev server: `pnpm dev`

## Project map
- `app/` holds routes, layouts, route handlers, and Server Actions.
- `components/` holds shared UI. `lib/` holds server-side logic, data access, and the env module.
- `proxy.ts` (formerly `middleware.ts`) sits at the project root or inside `src/`.
- Tests sit next to the code as `*.test.ts(x)`. End-to-end specs live in `e2e/`.
- Next.js 16 needs Node.js 20.9+ and TypeScript 5.1+. From 16.2 the docs for the installed version ship in `node_modules/next/dist/docs/`.

## Working agreement
- Read the files you will change, plus one neighboring file that does a similar job, before writing code. Match the patterns already in the repo.
- For work that touches more than two files, post a 2-4 line plan first. Ask one specific question when a requirement is ambiguous or the change is hard to undo.
- Keep each diff to one concern. Leave unrelated code, formatting, and comments as they are.
- Reproduce a bug with a failing test before fixing it whenever a test can express it.
- Run the commands in the Verify list that apply before you say a task is done, and report each command with its result. State plainly anything you could not run. Run the Other commands only when asked or when the task needs them.
- Ask before adding a dependency, editing CI config, changing a lockfile by hand, deleting files, or touching data migrations that may already be applied.
- Read the installed version's docs or source when unsure of an API. Use only functions and options you have seen in this repo, its dependencies, or their docs.
- Keep secrets, tokens, and personal data out of code, tests, fixtures, logs, and chat output. Read config from the environment.
- Commit, push, or open pull requests only when asked.

## Conventions
- Treat every component in `app/` as a Server Component. Add `"use client"` to the smallest leaf that needs state, effects, or browser APIs.
- Await request APIs in server code: `params`, `searchParams`, `cookies()`, `headers()`, and `draftMode()` are Promises in Next.js 16. Type pages with the generated `PageProps<'/route'>` (run `npx next typegen`).
- Put request interception (redirects, rewrites, header checks) in `proxy.ts` with an exported `proxy` function. It runs on the Node.js runtime only; keep `middleware.ts` only if the project must run on the Edge runtime. Keep it thin and do real authorization next to the data.
- Before using a Next.js API from memory, read its page under `node_modules/next/dist/docs/` (16.2+) or the docs for the installed version. Model knowledge often describes Next.js 14 or 15.
- Fetch initial data in Server Components or route handlers. Use client-side fetching only for interaction-driven updates.
- Use Server Actions for mutations triggered from your own UI and route handlers for webhooks and external clients. Return a typed result for expected failures and throw only for unexpected ones.
- Treat Server Actions and route handlers as public endpoints: validate input with the repo's schema library (zod if present), check the session, then act.
- Write strict TypeScript. Narrow `unknown` instead of using `any`, and give any `@ts-expect-error` a one-line reason. Derive types from schemas where schemas exist.
- Read env vars through one validated module in `lib/`. Only `NEXT_PUBLIC_*` values reach the browser, and they are inlined at build time. Start modules that touch secrets or the database with `import "server-only"`.
- Use `next/link`, `next/image`, and `next/font`. Allow remote images with `images.remotePatterns` (`images.domains` is deprecated) and list local image paths that carry a query string in `images.localPatterns`.
- Add caching (`use cache`, `cacheComponents`, `cacheLife`) only when asked. Tag cached data with `cacheTag` and name what invalidates it.
- Invalidate with `revalidateTag('posts', 'max')`, passing a cacheLife profile as the second argument. Call `updateTag('posts')` inside a Server Action when the user must see their own write immediately.
- Give every parallel route slot (such as `@modal`) a `default.tsx` that returns `null` or calls `notFound()`. Next.js 16 fails the build when one is missing.
- Next.js 16 uses Turbopack for `next dev` and `next build`. A custom `webpack` config, sometimes added by a plugin, fails the build unless the script passes `--webpack`, so ask before adding one.
- Follow the styling system already in use (Tailwind, CSS modules, or other) instead of introducing a second one.

## Known agent mistakes
Check your diff against this list before you finish.
- Typing `{ params }: { params: { id: string } }` and reading `params.id` synchronously. Await the Promise instead.
- Creating `middleware.ts` in a Next.js 16 project. It is deprecated and cannot be configured for the Node.js runtime. Use `proxy.ts`, and keep `middleware.ts` only if the project must run on the Edge runtime.
- Running `next lint`. Use the repo's `lint` script.
- Calling `revalidateTag('posts')` with one argument, which is a TypeScript error in Next.js 16. Pass a cacheLife profile or use `updateTag` in a Server Action.
- Reading `cookies()` or `headers()` inside a `use cache` function. Read them outside and pass the values in as arguments.
- Adding `"use client"` to a whole page to silence one hook error. Extract the interactive part into a client leaf.
- Passing functions or class instances as props from a Server Component to a Client Component. Pass serializable data and move behavior into the client leaf.
- Importing server-only code into a client file, which bundles secrets. Check import chains when a client file gains an import from `lib/`.
- Reading `process.env.X` in a client component without the `NEXT_PUBLIC_` prefix, which is `undefined` in the browser.
- Expecting a changed `NEXT_PUBLIC_*` value to reach a deployed build without rebuilding, because it was inlined at build time.
- Trusting `await res.json()` as typed data. Parse it with the schema first.

## Testing
- Use the test runner already configured (Vitest or Jest) with Testing Library, and run it once with `vitest run` or `jest`. Query by role and label, and assert on what the user sees.
- Vitest does not support async Server Components. Move their logic into plain functions in `lib/` and cover the rendered page with a Playwright spec.
- Run Playwright against a production build (`pnpm build`, then `pnpm start`). Dev-mode compilation makes specs slow and flaky.
- Cover each Server Action and route handler with at least a valid case, an invalid-input case, and an unauthenticated case.
- Keep tests deterministic: freeze time, stub network calls at the boundary, and avoid arbitrary timeouts.

## Security
- Check authorization inside every Server Action and route handler, not only in `proxy.ts`. Verify the caller may touch that specific record.
- Read data through a `server-only` data access layer that checks the session and returns plain DTOs with only the fields the UI needs, never whole database rows.
- Treat every exported function in a `"use server"` file as a public HTTP endpoint, including ones you believe are unused.
- Behind a reverse proxy that changes the host, set `serverActions.allowedOrigins` instead of disabling the Origin check.
- Render user content as text. Use `dangerouslySetInnerHTML` only with sanitized, trusted HTML.
- Set auth cookies as `httpOnly`, `secure`, and `sameSite`. Keep tokens out of `localStorage` and logs.
- Return generic errors to the browser and log details on the server.

## Done means
- Every applicable command in the Verify list has run clean.
- New behavior has a test; a fixed bug has a test that failed before the fix.
- The final message lists what changed, the commands run with results, anything not verified, and follow-ups you noticed but did not do.
