# Repository Guidelines

## Source Of Truth

- `.agents/rules/*.md` is the normative source for this repository.
- This file is an entry point only. When there is tension between this file and a rule, follow the rule.
- Existing code that diverges from the rules does not create precedent for new work.
- When touching divergent code, keep the task scoped but move the directly affected unit toward the rules when safe and proportional.

## Main Technologies

- Main language: TypeScript.
- Backend: Node.js, Express, SQLite with `better-sqlite3` and `knex`.
- Frontend: React, Vite, Tailwind CSS.
- Tests: Jest. Real E2E belongs outside Jest, in Playwright/QA or an equivalent tool.
- Lint: ESLint.
- Format: Prettier.

## Project Shape

- Treat `backend/` and `frontend/` as independent projects.
- Backend business code lives in `backend/src/**` and is organized by bounded context.
- Frontend app code lives in `frontend/src/**` and is organized page-first.
- Do not share code, DTOs, schemas, entities, value objects, helpers, or packages between backend and frontend.
- The backend/frontend contract is the runtime API only: HTTP, JSON, multipart, status codes, and headers.

## Rules Map

| Rule | Path | Use when |
| --- | --- | --- |
| Code Standards | `.agents/rules/code-standards.md` | Any code edit. This is the baseline for TypeScript, naming, types, readability, imports, comments, and extraction. |
| Architecture | `.agents/rules/architecture.md` | Changing or reviewing boundaries, ownership, dependency direction, layers, composition, cross-context communication, DTOs, or backend/frontend separation. |
| Folder Structure | `.agents/rules/folder-structure.md` | Creating, moving, or reviewing files and folders in `backend/src/**` or `frontend/src/**`. |
| Backend | `.agents/rules/backend.md` | Working in `backend/src/**`, including modules, use cases, services, repositories, queries, controllers, handlers, parsers, database code, errors, logging, CLI adapters, and backend test support. |
| React | `.agents/rules/react.md` | Working in `frontend/src/**`, including pages, components, hooks, styles, forms, accessibility, frontend API clients, and React tests. |
| Tests | `.agents/rules/tests.md` | Adding, changing, fixing, or reviewing tests, fixtures, test helpers, test configuration, mocks, coverage, or verification gates. |

## Loading Order

1. Always load `.agents/rules/code-standards.md` before code edits.
2. Load `.agents/rules/architecture.md` before modifying responsibilities, dependencies, boundaries, composition, DTOs, public APIs, or backend/frontend contracts.
3. Load `.agents/rules/folder-structure.md` before creating, moving, or reviewing files under `backend/src/**` or `frontend/src/**`.
4. Load `.agents/rules/backend.md` for backend work in `backend/src/**`.
5. Load `.agents/rules/react.md` for frontend work in `frontend/src/**`.
6. Load `.agents/rules/tests.md` whenever tests, fixtures, helpers, mocks, coverage, or test configuration are involved.

## Verification

- Backend changes must run `cd backend && npm test` before reporting completion.
- Frontend changes must run `cd frontend && npm test` before reporting completion.
- Cross-cutting changes must run both test suites before reporting completion.
- Read the command output and confirm exit code zero before saying tests pass.
- If the full required suite cannot run, report the attempted command, the blocker, and any partial verification performed.

## Useful Commands

Backend:

- `cd backend && npm install`: install backend dependencies.
- `cd backend && npm run dev`: start the backend in development mode.
- `cd backend && npm run build`: type-check backend code.
- `cd backend && npm run lint`: run backend ESLint with zero warnings allowed.
- `cd backend && npm run format`: check backend Prettier formatting.
- `cd backend && npm run format:write`: apply backend Prettier formatting.
- `cd backend && npm test`: run the backend Jest suite with coverage.
- `cd backend && npm run db:init`: initialize the backend database.

Frontend:

- `cd frontend && npm install`: install frontend dependencies.
- `cd frontend && npm run dev`: start the Vite development server.
- `cd frontend && npm run build`: type-check and build the frontend.
- `cd frontend && npm run lint`: run frontend ESLint with zero warnings allowed.
- `cd frontend && npm run format`: check frontend Prettier formatting.
- `cd frontend && npm run format:write`: apply frontend Prettier formatting.
- `cd frontend && npm test`: run the frontend Jest suite with coverage.
