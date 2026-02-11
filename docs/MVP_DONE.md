# SeaCards MVP Done

## End-to-end vertical slice (must work on device)
- User can sign up / log in
- Mapbox map loads
- Ships render near user from websocket stream (simulated data OK initially)
- Tap ship -> “Scanner” overlay -> Catch request -> server validates fuel + range (range can be GPS optional toggle)
- Catch success adds to Hangar
- Hangar shows list + filters + ship detail

## Backend
- Postgres + PostGIS + Redis running via docker-compose
- Swagger/OpenAPI available
- Websocket streaming endpoint available
- Sighting logs stored (append-only)

## Quality gates
- pnpm lint + typecheck + test pass
- basic CI workflow runs on PR
