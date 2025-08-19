# Zenith — Web Project Management

Zenith is a web project management application. This repository contains a Next.js frontend and a Hono-based TypeScript server. The system uses Supabase Auth for authentication, a Neon (Postgres-compatible) database for storage, and Tailwind CSS for styling.

## Tech stack

- Frontend: Next.js (TypeScript) + Tailwind CSS
- Backend: Hono (TypeScript) running on Node.js
- Auth: Supabase Auth
- Database: Neon (Postgres-compatible)
- Other: pnpm as package manager

## Repository layout

- `client/` — Next.js frontend
- `server/` — Hono TypeScript server

## Prerequisites

- Node.js (v18+ recommended)
- pnpm
Access to a Supabase project (or another auth provider), and a Neon (Postgres-compatible) database or equivalent for local/dev

## Local development

1. Install dependencies

```bash
# from repo root
cd client && pnpm install
cd ../server && pnpm install
```

2. Run frontend

```bash
cd client
pnpm dev
```

3. Run backend

```bash
cd server
pnpm dev
```

The frontend runs using Next.js dev server. The backend runs the TypeScript Hono app (using `ts-node`) on the configured port (default: 3000 in server code).

## Environment variables (examples)

Create `.env` files for local development with the following keys (rename / adapt as needed):

Server (`server/.env`):

- DATABASE_URL=postgres://USER:PASSWORD@HOST:PORT/DATABASE  # Neon provides a Postgres-compatible connection string
- SUPABASE_URL=https://xyz.supabase.co
- SUPABASE_SERVICE_ROLE_KEY=service_role_key_here
- PORT=3000

Client (`client/.env.local`):

- NEXT_PUBLIC_SUPABASE_URL=https://xyz.supabase.co
- NEXT_PUBLIC_SUPABASE_ANON_KEY=public_anon_key_here
- NEXT_PUBLIC_API_URL=http://localhost:3000

## Build & start (production)

Build frontend:

```bash
cd client
pnpm build
pnpm start
```

Build backend and run:

```bash
cd server
pnpm build
node dist/index.js
```

## Database

This project expects a Postgres-compatible database; we've switched to using Neon (https://neon.tech) by default. Provide a `DATABASE_URL` connection string in the server environment. Neon is serverless and Postgres-compatible — connection strings work the same as standard Postgres. Consider using a migrations tool (Prisma, TypeORM, Knex) for schema management — not included by default.

## Authentication

Auth is implemented using Supabase Auth. Create a Supabase project, then copy the `SUPABASE_URL` and keys from the Project Settings. For the frontend, use the public anon key (`NEXT_PUBLIC_SUPABASE_ANON_KEY`); for the server, use the service role key (`SUPABASE_SERVICE_ROLE_KEY`) for admin operations. The server can verify JWTs issued by Supabase or call Supabase APIs using the service role key.

## Useful notes

- Keep `pnpm-lock.yaml` committed for reproducible installs.
- Add a `server/.env.example` and `client/.env.example` to show required variables to contributors.

## Next steps (recommended)

- Add a `.env.example` for both `client/` and `server/`.
- Add a migrations system (Prisma recommended) and example migration.
- Add basic CI to run lint/tests and make builds.

---