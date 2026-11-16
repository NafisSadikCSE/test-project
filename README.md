# Test-project

A Next.js application written in TypeScript, with the UI built in React.

## Stack

- Node.js
- TypeScript
- Next.js (App Router)
- React
- Tailwind CSS
- ESLint
- npm

## Status

The Next.js app is not set up yet. `package.json` currently contains only `dotenv`. There is no `src/` app, and `npm run dev` is not available.

## Requirements

- Node.js
- npm

## Setup

From this folder, create the app in place:

```bash
npx create-next-app@latest . --ts --eslint --tailwind --src-dir --app --use-npm --import-alias "@/*" --disable-git
```

Start the dev server:

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000).

Do not run `create-next-app` again after the Next.js app exists.

## Scripts

These scripts exist after the Next.js app is created.

| Command | Purpose |
| --- | --- |
| `npm install` | Install dependencies |
| `npm run dev` | Start the dev server |
| `npm run build` | Build for production |
| `npm start` | Run the production server |
| `npm run lint` | Run ESLint |

Use npm only.

## Layout

```text
public/                 static files
src/app/                routes (page.tsx, layout.tsx, route.ts)
src/components/         UI shared by more than one route
src/lib/                shared non-UI code
```

Application code lives in `src/`. Config files stay at the repository root. Import app code with the `@/` alias, for example `@/components/button`.

Project conventions for agents are in `cursor.md`.
