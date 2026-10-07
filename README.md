# `@next/codemod agents-md` monorepo reproduction

A pnpm workspace. `next@16.4.0` is a dependency of `apps/web` only, and `AGENTS.md` is at the repo root.

```bash
pnpm install
```

From the app:

```bash
cd apps/web
npx @next/codemod@16.4.0 agents-md --output ../../AGENTS.md
```

The root `AGENTS.md` gets `root: ./node_modules/next/dist/docs`. That path is relative to `apps/web`, not to `AGENTS.md`, so it does not resolve.

Reset with `git checkout AGENTS.md`, then from the repo root:

```bash
npx @next/codemod@16.4.0 agents-md --output AGENTS.md
```

The codemod does not find `next`, downloads the docs into `.next-docs` and edits `.gitignore`.
