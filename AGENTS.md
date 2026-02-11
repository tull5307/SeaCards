# SeaCards Agent Instructions (read this first)

## Stack (do not change)
- Mobile: React Native + Expo (SDK 50+), TypeScript strict
- Maps: Mapbox (no Google Maps)
- Backend: Node.js TypeScript (NestJS preferred)
- Realtime: Socket.io (MVP), Redis-backed pub/sub
- DB: Postgres + PostGIS required
- Cache: Redis required
- IAP: RevenueCat integration

## Coding standards
- TypeScript strict everywhere
- Prefer small PRs: 200–600 LOC diff
- Always add/update tests when behavior changes
- Update docs when adding endpoints or env vars

## Definition of done for every PR
- `pnpm lint` passes
- `pnpm typecheck` passes
- `pnpm test` passes
- README updated if setup changed
