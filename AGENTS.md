# Repository Guidelines

## Project Structure & Module Organization

The Next.js surface lives in `app/`, with route groups such as `app/search/` and API handlers under `app/api/`. Reusable UI sits in `components/`; shared utilities, actions, and data access stay in `lib/`. Drizzle migrations live in `drizzle/`, and tests pair with their subjects in `__tests__/`. Root-level `config/`, `docs/`, and `scripts/` hold model presets, ops notes, and CLI helpers; static assets reside in `public/`.

## Build, Test, and Development Commands

- `bun install` installs dependencies and respects the required Bun 1.2.x runtime.
- `bun run dev` (`bun dev`) starts the Turbo Next.js dev server with hot reloading.
- `bun run build` compiles the production bundle; follow with `bun run start` to serve it locally.
- `bun run lint`, `bun run typecheck`, `bun run format:check` enforce linting, types, and formatting.
- `bun run migrate` applies the latest Drizzle migrations using `lib/db/migrate.ts`.
- `docker compose up -d` provisions the local Postgres/Supabase stack defined in `docker-compose.yaml`.

## Environment & Configuration

Copy `.env.local.example` to `.env.local` and fill required database and API credentials before migrating. Model presets live in `config/models/*.json`; update them when switching providers. Record new environment variables in `docs/CONFIGURATION.md` and flag them in PR descriptions. Keep Docker credentials aligned with `DATABASE_URL` so migrations and integration tests stay green.

## Coding Style & Naming Conventions

TypeScript and React files follow Prettier defaults (two spaces, 100-character soft limit). ESLint extends `eslint-config-next` plus `simple-import-sort`, so keep import groups alphabetical. Components and hooks use PascalCase; utilities stay camelCase; route handlers mirror the folder (`route.ts`). Prefer Tailwind composition and keep shared variants near the consuming component.

## Testing Guidelines

Vitest drives unit and integration coverage via the jsdom setup in `vitest.config.mts`. Keep tests in sibling `__tests__/` folders (for example `lib/actions/__tests__/chat.test.ts`) and use suffixes like `*.integration.test.ts` when touching Supabase RLS policies. Run the full suite with `bun run test` or iterate with `bun run test:watch`.

## Commit & Pull Request Guidelines

The history follows Conventional Commits (`feat:`, `fix:`, `refactor:`) as shown in recent log entries; keep scopes short and meaningful. Before opening a pull request, ensure lint, type check, tests, and migrations succeed locally. PRs should describe the problem, summarize the solution, link any tracking issues, and include screenshots or logs for UI or API changes. Flag schema updates and required environment variables in the description so deployment reviewers can react quickly.
