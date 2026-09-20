# Banglar Darpan LIVE

A cinematic Bengali news IPTV viewer with a curated default lineup, local open-source stream testing, and a browser-local admin control room.

## Run & Operate

- `pnpm --filter @workspace/api-server run dev` — run the API server (port 5000)
- `pnpm run typecheck` — full typecheck across all packages
- `pnpm run build` — typecheck + build all packages
- `pnpm --filter @workspace/api-spec run codegen` — regenerate API hooks and Zod schemas from the OpenAPI spec
- `pnpm --filter @workspace/db run push` — push DB schema changes (dev only)
- Required env: `DATABASE_URL` — Postgres connection string

## Stack

- pnpm workspaces, Node.js 24, TypeScript 5.9
- API: Express 5
- DB: PostgreSQL + Drizzle ORM
- Validation: Zod (`zod/v4`), `drizzle-zod`
- API codegen: Orval (from OpenAPI spec)
- Build: esbuild (CJS bundle)

## Where things live

- `artifacts/banglar-darpan-live/src/App.tsx` — viewer, test-stream lane, local admin route, playlist state, and player source handling.
- `artifacts/banglar-darpan-live/src/index.css` — broadcast-inspired theme tokens, responsive layout, and component styling.
- `artifacts/banglar-darpan-live/vite.config.ts` — root web artifact routing and Vite configuration.

## Architecture decisions

- The first build is frontend-only so viewers can test links and local files immediately without account setup or a backend.
- The admin control room uses localStorage for lineup persistence and includes a reset-to-originals action for recovery.
- The player chooses YouTube iframe, native video, or local object URL rendering based on the submitted source type.

## Product

- Full-screen TV-style playback for the four exact Bengali news URLs requested in the brief.
- Open Source Test lane for YouTube, HLS, MP4, and local video sources.
- Persistent Bengali LIVE watermark, red LIVE badge, custom playback controls, responsive CTV/mobile/desktop layout.
- `/admin` lineup management with add, edit, delete, and reset-originals workflows.

## User preferences

- Use the exact pre-configured news report URLs from the brief; do not replace them with dummy or placeholder videos.

## Gotchas

- YouTube availability is controlled by the source video and embed permissions; the app preserves the requested URLs and surfaces the embed state.
- Local uploads stay in the current browser session and are not uploaded to a server.

## Pointers

- See the `pnpm-workspace` skill for workspace structure, TypeScript setup, and package details
