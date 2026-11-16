# Cursor instructions

Project guidance for this repository. Cursor does not load this file on its own. To apply it in every chat, keep a copy in `AGENTS.md` or turn sections into rules under `.cursor/rules/`.

If `create-next-app` adds its own `AGENTS.md`, leave that file in place. It covers Next.js framework rules. This file covers this project's stack and layout.

## Project

- Name: Test-project
- Owner: Nafis
- Status: not scaffolded yet

## Tech stack

- Runtime: Node.js
- Language: TypeScript
- Framework: Next.js (App Router)
- UI: React
- Styling: Tailwind CSS
- Package manager: npm
- Linter: ESLint

Write application code in TypeScript. Build the UI with React inside Next.js. Use Next.js for routing and server code. Style with Tailwind. Install and run packages with npm. Do not add a separate backend unless the task needs one.

## Scaffold

The app does not exist until `package.json` is present. Create it from the repository root, in this folder, and do not create a nested project directory:

```bash
npx create-next-app@latest . --ts --eslint --tailwind --src-dir --app --use-npm --import-alias "@/*" --disable-git
```

After scaffolding, set Status above to `scaffolded` and record the Next.js version from `package.json`. Do not run `create-next-app` again once `package.json` exists.

## Commands

Use npm only. Do not add or invoke pnpm, Yarn, or Bun.

- Install: `npm install`
- Dev server: `npm run dev`
- Production build: `npm run build`
- Start production server: `npm start`
- Lint: `npm run lint`

Read `package.json` before running a script or adding a dependency. Do not add a package that duplicates Next.js or React.

## Project structure

Keep config at the root and application code in `src/`. `public/` stays at the root. Create a folder only when a file is going into it.

```text
.
├── public/                     # static files, served from /
├── src/
│   ├── app/                    # routes only
│   │   ├── layout.tsx          # root layout
│   │   ├── page.tsx            # /
│   │   ├── globals.css
│   │   ├── loading.tsx         # add when a route needs a loading state
│   │   ├── error.tsx           # add when a route needs an error state
│   │   ├── not-found.tsx       # add when a route needs a not-found state
│   │   └── api/                # HTTP endpoints other clients call
│   │       └── example/route.ts
│   ├── components/             # React UI used by more than one route
│   └── lib/                    # shared non-UI code: helpers, data, env
├── next.config.ts
├── package.json
├── tsconfig.json
└── cursor.md
```

`src/app` owns URLs. A folder there becomes a public route only when it contains `page.tsx` or `route.ts`.

## Where code goes

- A new screen is a `page.tsx` under `src/app`. Keep the page thin: compose the screen and load data. Do not put shared business logic in the page.
- A component used by one route stays next to that route in `_components/`. The `_` prefix keeps the folder out of the URL. Move it to `src/components/` when a second route needs it.
- Shared UI primitives go in `src/components/`.
- Shared non-UI code goes in `src/lib/`. Group by domain (`src/lib/projects/queries.ts`) once more than one helper exists. Do not add empty `services`, `utils`, `helpers`, or `managers` folders.
- Types live next to the code that uses them. Move a type to `src/lib/` only when more than one feature imports it.
- Route groups, written as `(name)`, change the layout without changing the URL. Add one only when two areas need different layouts.
- Do not create a `pages/` directory. This project uses the App Router only.
- Do not put `app` or `pages` at the repository root. `src/app` is the only router.
- Import application code with the `@/` alias, mapped to `./src/*`. Example: `import { Button } from "@/components/button"`.

## React and Next.js

- Components are Server Components by default. Add `"use client"` only for state, event handlers, or browser APIs. Keep that client boundary in a small component.
- Mutations from this app's own UI use Server Actions. Add `route.ts` only when a browser, webhook, or other service must call HTTP.
- Check access beside the data it protects. Hiding a button is not an access check.
- Read environment variables on the server. A value that must reach the browser uses the `NEXT_PUBLIC_` prefix. Keep secrets in `.env.local` and do not commit `.env*` files.

## Code style

- File names are kebab-case: `project-header.tsx`. Component names are PascalCase: `ProjectHeader`.
- One component per file.
- Name things for what they do.
- Use TypeScript strictly. Do not use `any`. Narrow an unknown value at the boundary where it enters the app.
- Handle errors where a failure would be silent or hard to diagnose. Use `error.tsx` for route-level render failures.
- Match the style of the surrounding code.
- Keep each change scoped to the request. Do not add files, dependencies, or refactors that were not asked for.

## How to work

- Read this file and `package.json` before editing.
- Implement, debug, and iterate in the code. Prefer a working change over a long plan.
- Verify behavior before calling a change done. For UI work, run `npm run dev` and exercise the affected flow in the browser, including the empty and error states that the change touches.
- Run `npm run lint` after a code change when a linter is configured.
- Do not create a git commit unless asked.
