# Workspace

## Overview

pnpm workspace monorepo using TypeScript. Each package manages its own dependencies.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **API framework**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild (CJS bundle)

## Key Commands

- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- `pnpm --filter @workspace/api-server run dev` — run API server locally

See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details.

## Artifacts

### 메뉴 투표 (menu-vote)
- **Path**: `artifacts/menu-vote/`
- **Preview**: `/`
- **Type**: React + Vite web app
- **Purpose**: Menu voting website — users can vote for food items, add new items, filter by category, and see live voting results.

## Database Schema

### menus
- `id` serial PK
- `name` text NOT NULL
- `description` text nullable
- `category` text nullable
- `voteCount` integer default 0
- `createdAt` timestamptz default now()

## API Routes

- `GET /api/menus` — list all menus ordered by vote count
- `POST /api/menus` — create a new menu item
- `GET /api/menus/:id` — get a single menu item
- `DELETE /api/menus/:id` — delete a menu item
- `POST /api/menus/:id/vote` — vote for a menu item
- `POST /api/menus/:id/unvote` — unvote a menu item
- `GET /api/menus/summary` — get summary stats (total votes, top menu, category breakdown)
