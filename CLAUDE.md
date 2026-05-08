# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm install        # install dependencies
npm run dev        # start dev server at localhost:3000
npm run build      # production build
npm run lint       # run ESLint
npm test           # run all tests with Vitest
npx vitest run tests/components/Navbar.test.tsx  # run a single test file
```

## Architecture

**Pocket Heist** is a Next.js 16 app (React 19, TypeScript, Tailwind CSS v4) for managing small office mischief missions ("heists").

### Route Groups

- `app/(public)/` — unauthenticated pages (splash, login, signup, preview). No Navbar. The splash page at `/` is intended as a routing gate: redirect to `/heists` if logged in, `/login` if not.
- `app/(dashboard)/` — authenticated pages with `Navbar` in the layout. Contains `/heists`, `/heists/create`, and `/heists/[id]`.

### Styling

- Tailwind v4 is configured via `postcss.config.mjs` and imported in `app/globals.css`.
- Custom theme tokens (colors, font) are defined in `globals.css` under `@theme`.
- Global utility classes (`.page-content`, `.center-content`, `.form-title`) are also defined in `globals.css`.
- Component-scoped styles use CSS Modules (e.g., `Navbar.module.css`).

### Components

Reusable components live in `components/<Name>/` with a barrel `index.ts` export. Use `@/components/Name` import paths (aliases are configured via `tsconfig.json` and `vite-tsconfig-paths`).

### Testing

Tests live in `tests/` mirroring the source structure. Uses Vitest + Testing Library with jsdom. Setup file is `vitest.setup.ts`.
