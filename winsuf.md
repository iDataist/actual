# Cascade Chat Conversation

  Note: _This is purely the output of the chat conversation and does not contain any raw data, codebase snippets, etc. used to generate the output._

### User Input

Walk me through the architecture of this repo

### Planner Response

I'll scan the repository to tailor the architecture walkthrough and cite exact paths and configs. I'll list the root and `packages/` directories and open key config files like `package.json`, `lage.config.js`, `tsconfig.json`, and `eslint.config.mjs`.

*Listed directory [actual](file:///Users/hren/Downloads/actual) *

*Listed directory [packages](file:///Users/hren/Downloads/actual/packages) *

*Viewed [package.json](file:///Users/hren/Downloads/actual/package.json) *

*Viewed [lage.config.js](file:///Users/hren/Downloads/actual/lage.config.js) *

*Viewed [tsconfig.json](file:///Users/hren/Downloads/actual/tsconfig.json) *

*Viewed [eslint.config.mjs](file:///Users/hren/Downloads/actual/eslint.config.mjs) *

*Viewed [README.md](file:///Users/hren/Downloads/actual/README.md) *

### Planner Response

I'll open each package's package.json and look for key build/test scripts and names, and also locate a few critical entry/config files (vite config, electron main, sync server entry) to accurately describe responsibilities and flows. I'll run these lookups in parallel for speed.

*Viewed [package.json](file:///Users/hren/Downloads/actual/packages/loot-core/package.json) *

*Viewed [package.json](file:///Users/hren/Downloads/actual/packages/desktop-client/package.json) *

*Viewed [package.json](file:///Users/hren/Downloads/actual/packages/desktop-electron/package.json) *

*Viewed [package.json](file:///Users/hren/Downloads/actual/packages/api/package.json) *

*Viewed [package.json](file:///Users/hren/Downloads/actual/packages/sync-server/package.json) *

*Viewed [package.json](file:///Users/hren/Downloads/actual/packages/component-library/package.json) *

*Viewed [package.json](file:///Users/hren/Downloads/actual/packages/crdt/package.json) *

*Viewed [package.json](file:///Users/hren/Downloads/actual/packages/plugins-service/package.json) *

*Viewed [package.json](file:///Users/hren/Downloads/actual/packages/eslint-plugin-actual/package.json) *

*Searched filesystem*

*Searched filesystem*

*Searched filesystem*

*Searched filesystem*

*Listed directory [src](file:///Users/hren/Downloads/actual/packages/sync-server/src) *

*Searched filesystem*

*Listed directory [src](file:///Users/hren/Downloads/actual/packages/loot-core/src) *

### Planner Response

I'll open a few key entry/config files to accurately describe responsibilities and flows: the web Vite config, Electron main file, and the sync server app entry.

*Viewed [vite.config.mts](file:///Users/hren/Downloads/actual/packages/desktop-client/vite.config.mts) *

*Listed directory [src](file:///Users/hren/Downloads/actual/packages/desktop-client/src) *

### Planner Response

# Findings

- **Monorepo & Tooling**
  - **Root workspace**: Yarn 4 workspaces with Lage orchestrating tasks. See [package.json](cci:7://file:///Users/hren/Downloads/actual/package.json:0:0-0:0) scripts and [lage.config.js](cci:7://file:///Users/hren/Downloads/actual/lage.config.js:0:0-0:0).
  - **TypeScript config**: [tsconfig.json](cci:7://file:///Users/hren/Downloads/actual/tsconfig.json:0:0-0:0) sets strict-ish settings, path aliases (e.g., `loot-core/*`, `@desktop-client/*`), and noEmit for IDE/typecheck-first workflow.
  - **ESLint**: Flat config in [eslint.config.mjs](cci:7://file:///Users/hren/Downloads/actual/eslint.config.mjs:0:0-0:0) with custom rules from [packages/eslint-plugin-actual/](cci:7://file:///Users/hren/Downloads/actual/packages/eslint-plugin-actual:0:0-0:0) enforcing i18n, logging, and React/import patterns.

- **Key Packages ([packages/](cci:7://file:///Users/hren/Downloads/actual/packages:0:0-0:0))**
  - **[loot-core/](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core:0:0-0:0) (core logic)**
    - Platform-agnostic business logic for budgeting, DB/workflows, and client/server utilities.
    - Builds:
      - Browser bundle for the web client: `build:browser`, `watch:browser`.
      - Node/Electron bundle for desktop: `build:node`, `watch:node` (via Vite: `vite.desktop.config.ts`).
    - Public exports map is extensive (client hooks, queries, server APIs). See [packages/loot-core/package.json](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core/package.json:0:0-0:0) `exports`.
    - Source: [packages/loot-core/src/](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core/src:0:0-0:0) with subdirs:
      - `client/` (hooks, queries, Redux, platform shims)
      - [server/](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core/src/server:0:0-0:0) (server-side logic, calculations)
      - [platform/](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core/src/platform:0:0-0:0) (platform abstractions)
      - [shared/](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core/src/shared:0:0-0:0), [types/](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core/src/types:0:0-0:0)
  - **[desktop-client/](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-client:0:0-0:0) (@actual-app/web)**
    - React UI for web and desktop (Electron) using Vite.
    - Entry/config:
      - Vite config: [packages/desktop-client/vite.config.mts](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-client/vite.config.mts:0:0-0:0) (PWA for web mode, build-shims injection, watches `loot-core/lib-dist/*` for HMR).
      - App entry: [packages/desktop-client/src/index.tsx](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-client/src/index.tsx:0:0-0:0).
      - Service worker integration via [plugins-service](cci:7://file:///Users/hren/Downloads/actual/packages/plugins-service:0:0-0:0).
    - Scripts: `start` (Vite dev), `start:browser` (custom watch), `build`, E2E (`playwright`).
    - Source: [packages/desktop-client/src/](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-client/src:0:0-0:0) (React components in [components/](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-client/src/components:0:0-0:0), hooks, i18n, Redux, etc.).
  - **[desktop-electron/](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-electron:0:0-0:0) (Electron shell)**
    - Wraps the web client for desktop apps; bundles and signs installers.
    - Main process: [packages/desktop-electron/index.ts](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-electron/Users/hren/Downloads/actual/packages/desktop-electron/index.ts:0:0-0:0) (plus [preload.ts](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-electron/Users/hren/Downloads/actual/packages/desktop-electron/preload.ts:0:0-0:0), [menu.ts](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-electron/Users/hren/Downloads/actual/packages/desktop-electron/menu.ts:0:0-0:0), [server.ts](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-electron/Users/hren/Downloads/actual/packages/desktop-electron/server.ts:0:0-0:0), [security.ts](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-electron/Users/hren/Downloads/actual/packages/desktop-electron/security.ts:0:0-0:0)).
    - Pulls built web assets from `@actual-app/web/build*` into the packaged app. See `package.json build.files`.
    - Dev: `watch` starts Electron and points to local data dirs; E2E present.
  - **`@actual-app/sync-server/` (sync-server)**
    - Express 5 server for sync, auth, admin, and integrations.
    - Entry: [packages/sync-server/src/app.ts](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/app.ts:0:0-0:0) (CLI bin: `actual-server` via `build/bin/actual-server.js`).
    - Routes/components: [app-sync.ts](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/app-sync.ts:0:0-0:0), [app-openid.js](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/app-openid.js:0:0-0:0), [app-admin.js](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/app-admin.js:0:0-0:0), [app-cors-proxy.js](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/app-cors-proxy.js:0:0-0:0), banking integrations under [app-gocardless/](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/app-gocardless:0:0-0:0) and [app-pluggyai/](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/app-pluggyai:0:0-0:0).
    - DB and migrations under [src/sql/](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/sql:0:0-0:0) and scripts in [src/scripts/](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/scripts:0:0-0:0).
    - Scripts: `start`, `start-monitor` (nodemon), `db:*`, `test` (Vitest).
  - **`@actual-app/api/` (programmatic API)**
    - Node API built with `tsc`; depends on [loot-core](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core:0:0-0:0) build artifacts and `@actual-app/crdt`.
    - Scripts wire up building [loot-core](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core:0:0-0:0) API and CRDT first (`build:app`, `build:crdt`) before packaging to `dist/`.
  - **`@actual-app/components/` (component-library)**
    - Reusable React components and icons with strict exports (e.g., `./button`, `./menu`, `./icons/*`).
    - Used by [desktop-client](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-client:0:0-0:0).
  - **`@actual-app/crdt/`**
    - CRDT implementation for sync; protobuf-based, compiled to `dist/`.
    - Scripts include proto generation and TS builds.
  - **[plugins-service/](cci:7://file:///Users/hren/Downloads/actual/packages/plugins-service:0:0-0:0)**
    - Service worker for plugin system; built by Vite with Workbox.
    - Integrated into the web client via Vite PWA config.
  - **[eslint-plugin-actual/](cci:7://file:///Users/hren/Downloads/actual/packages/eslint-plugin-actual:0:0-0:0)**
    - Custom ESLint plugin containing project-specific rules.

- **Runtime Architecture**
  - **Web (Browser)**
    - React app in `@actual-app/web` serves UI, imports [loot-core](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core:0:0-0:0) client modules for data/query logic.
    - PWA in web mode: enabled via `VitePWA` in [vite.config.mts](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-client/vite.config.mts:0:0-0:0) and service worker built by [plugins-service](cci:7://file:///Users/hren/Downloads/actual/packages/plugins-service:0:0-0:0).
  - **Desktop (Electron)**
    - Electron main ([desktop-electron/index.ts](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-electron/Users/hren/Downloads/actual/packages/desktop-electron/index.ts:0:0-0:0)) loads the web client build.
    - [loot-core](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core:0:0-0:0) platform exports resolve to Electron/Node variants where needed (see [loot-core](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core:0:0-0:0) exports for `client/platform`).
  - **Sync Server**
    - Optional, for multi-device sync and open banking integrations.
    - Express app composition in [packages/sync-server/src/](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src:0:0-0:0): [app.ts](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/app.ts:0:0-0:0) mounts the specific `app-*` modules (sync, admin, proxies, auth).
  - **Programmatic API**
    - `@actual-app/api` provides Node consumers access to core functionality with a packaged dist and types.

- **Build/Dev Flows (root [package.json](cci:7://file:///Users/hren/Downloads/actual/package.json:0:0-0:0))**
  - **Browser dev**: `yarn start` → `start:browser` runs [plugins-service](cci:7://file:///Users/hren/Downloads/actual/packages/plugins-service:0:0-0:0) build-dev and parallel watchers:
    - `loot-core watch:browser` and `@actual-app/web start:browser`.
  - **Desktop dev**: `yarn start:desktop` runs in parallel:
    - `loot-core watch:node`, `@actual-app/web watch/build:browser`, `desktop-electron watch`.
  - **Server+Web dev**: `yarn start:server-dev` runs the sync server monitor plus the browser dev server.
  - **Builds**: `build:browser`, `build:desktop`, `build:server`, `build:api`, `build:plugins-service`.
  - **Quality**: `yarn typecheck`, `yarn lint:fix`.
  - **Tests**: `yarn test` uses Lage to run package tests in parallel with caching.

- **Testing**
  - **Unit**: Vitest across packages ([loot-core](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core:0:0-0:0), `@actual-app/web`, `@actual-app/api`, [sync-server](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server:0:0-0:0)).
  - **E2E**: Playwright in `@actual-app/web` (browser) and [desktop-electron](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-electron:0:0-0:0) (desktop).
  - Lage config enables output/caching; see [lage.config.js](cci:7://file:///Users/hren/Downloads/actual/lage.config.js:0:0-0:0).

- **Selected Entry Points & Important Files**
  - **Web entry**: [packages/desktop-client/src/index.tsx](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-client/src/index.tsx:0:0-0:0)
  - **Web build config**: [packages/desktop-client/vite.config.mts](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-client/vite.config.mts:0:0-0:0)
  - **Electron main**: [packages/desktop-electron/index.ts](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-electron/Users/hren/Downloads/actual/packages/desktop-electron/index.ts:0:0-0:0)
  - **Sync server app**: [packages/sync-server/src/app.ts](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/app.ts:0:0-0:0)
  - **Core exports**: [packages/loot-core/package.json](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core/package.json:0:0-0:0) `exports`
  - **Monorepo orchestration**: [lage.config.js](cci:7://file:///Users/hren/Downloads/actual/lage.config.js:0:0-0:0), [package.json](cci:7://file:///Users/hren/Downloads/actual/package.json:0:0-0:0) (root), [eslint.config.mjs](cci:7://file:///Users/hren/Downloads/actual/eslint.config.mjs:0:0-0:0), [tsconfig.json](cci:7://file:///Users/hren/Downloads/actual/tsconfig.json:0:0-0:0)

```mermaid
flowchart LR
  subgraph Web[@actual-app/web (desktop-client)]
    UI[React UI] --> LCClient[loot-core client APIs]
    UI --> Components[@actual-app/components]
    UI --> SW[plugins-service SW]
  end

  subgraph Core[loot-core]
    LCClient --> Shared[shared/types]
    LCServer[server logic] --> DB[(better-sqlite3)]
  end

  subgraph Desktop[desktop-electron]
    ElectronMain[index.ts] --> LoadsWeb[Loads @actual-app/web build]
    ElectronMain --> LCNode[loot-core node/electron exports]
  end

  subgraph Sync[@actual-app/sync-server]
    App[app.ts] --> SyncRoutes[app-sync.ts]
    App --> Admin[app-admin.js]
    App --> Auth[app-openid.js]
    App --> Banking[app-gocardless/*, app-pluggyai/*]
    Sync --> DB2[(better-sqlite3)]
  end

  API[@actual-app/api] --> Core

  Web -->|optional sync| Sync
  Desktop -->|optional sync| Sync
```

# How things fit together

- **Single source of truth** is in [loot-core](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core:0:0-0:0), which exposes both client and server utilities with platform-specific resolution (Electron vs browser) via its `exports` map and TS path config.
- **UI** in `@actual-app/web` consumes [loot-core](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core:0:0-0:0)’s client APIs and the shared component library. It runs in the browser or inside Electron.
- **Electron wrapper** packages the web build and switches [loot-core](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core:0:0-0:0) to Node/Electron paths as needed for file system, SQLite, etc.
- **Sync server** is independent; the UI can run with or without it. When enabled, clients use server endpoints from [app-sync.ts](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/app-sync.ts:0:0-0:0) for multi-device sync and integrations.
- **Programmatic API** packages a Node interface for external tools/scripts.

# Recommended Actions

- **Run in browser**: `yarn start`
- **Run desktop**: `yarn start:desktop`
- **Run with sync server**: `yarn start:server-dev`
- **Typecheck/lint/tests**:
  - `yarn typecheck`
  - `yarn lint:fix`
  - `yarn test` (Lage across workspaces)

# Status

- Provided a concise, repo-specific architecture walkthrough with concrete paths, build/test flows, and a system diagram. If you want a deeper dive into any package (e.g., [loot-core](cci:7://file:///Users/hren/Downloads/actual/packages/loot-core:0:0-0:0) query/data flows or [sync-server](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server:0:0-0:0) route layout), tell me which one.

*Viewed [README.md](file:///Users/hren/Downloads/actual/README.md) *

### User Input

Walk me through how to run this service locally via docker

### Planner Response

I'll open the Docker configuration files to give you precise, copy-pastable commands and explain the environment variables and volumes. I'll read [docker-compose.yml](cci:7://file:///Users/hren/Downloads/actual/docker-compose.yml:0:0-0:0), the root [Dockerfile](cci:7://file:///Users/hren/Downloads/actual/Dockerfile:0:0-0:0), and [sync-server.Dockerfile](cci:7://file:///Users/hren/Downloads/actual/sync-server.Dockerfile:0:0-0:0).

*Viewed [docker-compose.yml](file:///Users/hren/Downloads/actual/docker-compose.yml) *

### Planner Response

I'll open the Dockerfiles at the repo root to see how the images are built and what commands/ports/volumes they expect. I'll also search for any docker startup scripts referenced by the compose file (e.g., docker-start.sh) to ensure the run instructions are accurate.

*Viewed [Dockerfile](file:///Users/hren/Downloads/actual/Dockerfile) *

*Viewed [docker-start](file:///Users/hren/Downloads/actual/bin/docker-start) *

*Viewed [sync-server.Dockerfile](file:///Users/hren/Downloads/actual/sync-server.Dockerfile) *

### Planner Response

I'll locate the web client's watch script invoked by `@actual-app/web start:browser` to confirm the dev server port and behavior inside Docker.

*Searched filesystem*

### Planner Response

I’m going to scan the sync server source for its configuration and data directory settings so I can give you correct volume mounts and environment variables when running the sync server via Docker. I'll search for config loading and data dir references.

*Grep searched codebase*

*Viewed [load-config.js](file:///Users/hren/Downloads/actual/packages/sync-server/src/load-config.js) *

*Searched filesystem*

*Viewed [.yarnrc.yml](file:///Users/hren/Downloads/actual/.yarnrc.yml) *

*Viewed [app.ts](file:///Users/hren/Downloads/actual/packages/sync-server/src/app.ts) *

### Planner Response

# Findings

- **Dev compose**: [docker-compose.yml](cci:7://file:///Users/hren/Downloads/actual/docker-compose.yml:0:0-0:0) runs the web app dev server inside a container using the root [Dockerfile](cci:7://file:///Users/hren/Downloads/actual/Dockerfile:0:0-0:0) and [bin/docker-start](cci:7://file:///Users/hren/Downloads/actual/bin/docker-start:0:0-0:0). It maps port `3001:3001` and mounts the whole repo at [/app](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-client/src/app:0:0-0:0).
- **Prod server image**: [sync-server.Dockerfile](cci:7://file:///Users/hren/Downloads/actual/sync-server.Dockerfile:0:0-0:0) builds a production image for the sync server and bundles the built web UI inside it. It exposes port `5006`. Config/env names are defined in [packages/sync-server/src/load-config.js](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/load-config.js:0:0-0:0).

# Options to run locally via Docker

## Option A — Web client (dev server) via docker-compose
This is good for front‑end development; it does not start the sync server.

- **Files referenced**: [docker-compose.yml](cci:7://file:///Users/hren/Downloads/actual/docker-compose.yml:0:0-0:0), [Dockerfile](cci:7://file:///Users/hren/Downloads/actual/Dockerfile:0:0-0:0), [bin/docker-start](cci:7://file:///Users/hren/Downloads/actual/bin/docker-start:0:0-0:0), [packages/desktop-client/vite.config.mts](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-client/vite.config.mts:0:0-0:0).
- **What it does**:
  - Installs deps (if `node_modules/` is empty).
  - Runs `yarn start:browser` which starts the Vite dev server for `@actual-app/web` on port `3001`.

Steps:
```bash
# From repo root
docker compose up --build

# Open the web app
open http://localhost:3001
```

Notes:
- Compose maps the repo into the container ([.:/app](cci:7://file:///Users/hren/Downloads/actual/packages/desktop-client/src/app:0:0-0:0)), so changes on your host hot‑reload.
- HTTPS is off by default (compose sets `HTTPS` to empty). If you need HTTPS dev certs, set a non-empty value:
```yaml
# docker-compose.yml
services:
  actual-development:
    environment:
      - HTTPS=1
```

## Option B — Full app (sync server + bundled UI) via a single Docker image
This runs the production sync server that also serves the built React app.

- **Files referenced**: [sync-server.Dockerfile](cci:7://file:///Users/hren/Downloads/actual/sync-server.Dockerfile:0:0-0:0), [packages/sync-server/src/app.ts](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/app.ts:0:0-0:0), [packages/sync-server/src/load-config.js](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/load-config.js:0:0-0:0).
- **Defaults**:
  - Port: `5006` (config key `port`, env `ACTUAL_PORT`, default 5006).
  - Data dir: [/data](cci:7://file:///Users/hren/Downloads/actual/data:0:0-0:0) in the container (config key `dataDir`, env `ACTUAL_DATA_DIR`).
  - Web root auto-points at the bundled `@actual-app/web/build`.

Build and run:
```bash
# Build the image
docker build -f sync-server.Dockerfile -t actual-local .

# Create a host data dir for persistence
mkdir -p ./actual-data

# Run the server
docker run --name actual \
  -p 5006:5006 \
  -v "$(pwd)/actual-data:/data" \
  actual-local
```

Verify:
```bash
curl http://localhost:5006/health    # {"status":"UP"}
curl http://localhost:5006/info      # build info
open http://localhost:5006           # opens the UI
```

Common env overrides (from [packages/sync-server/src/load-config.js](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/load-config.js:0:0-0:0)):
```bash
# Change port or hostname
-e ACTUAL_PORT=5006 \
-e ACTUAL_HOSTNAME=0.0.0.0 \

# Persist data somewhere else
-e ACTUAL_DATA_DIR=/data \

# Authentication method: password|header|openid
-e ACTUAL_LOGIN_METHOD=password \

# Enable CORS proxy endpoint for plugins (off by default)
-e ACTUAL_CORS_PROXY_ENABLED=true
```

Enable HTTPS (two ways, the server supports file paths or raw PEM):
```bash
# If you have cert files on host:
# ./certs/server.key and ./certs/server.crt
docker run --name actual \
  -p 5006:5006 \
  -v "$(pwd)/actual-data:/data" \
  -v "$(pwd)/certs:/certs:ro" \
  -e ACTUAL_HTTPS_KEY=/certs/server.key \
  -e ACTUAL_HTTPS_CERT=/certs/server.crt \
  actual-local
```

Data layout inside the container (auto-created under `dataDir`):
- `server-files/` and `user-files/` hold server metadata and user budgets.
- A `config.json` can be picked up from `ACTUAL_CONFIG_PATH`, otherwise from `dataDir/config.json` if present.

## Option C — Dev server + Sync server together (two processes)
- Use compose (Option A) for the front‑end on `http://localhost:3001`.
- Run the sync server separately (Option B) on `http://localhost:5006`.
- In production mode, the sync server serves the UI itself; for dev‑proxy mode, the server would need `NODE_ENV=development` and a dev dependency (`http-proxy-middleware`) that isn’t included in the prod image. For simple local runs, prefer Option B (single server) or keep them separate as above.

# Recommended Actions

- **If you want the full app in one container**: follow Option B. It’s closest to production, persists data, and serves the UI at `http://localhost:5006`.
- **If you want hot‑reload for UI work**: use Option A (compose) at `http://localhost:3001`.

# Status

- Provided precise Docker run instructions for dev and prod flows, with ports, volumes, and optional HTTPS, citing [docker-compose.yml](cci:7://file:///Users/hren/Downloads/actual/docker-compose.yml:0:0-0:0), [Dockerfile](cci:7://file:///Users/hren/Downloads/actual/Dockerfile:0:0-0:0), [sync-server.Dockerfile](cci:7://file:///Users/hren/Downloads/actual/sync-server.Dockerfile:0:0-0:0), and [packages/sync-server/src/load-config.js](cci:7://file:///Users/hren/Downloads/actual/packages/sync-server/src/load-config.js:0:0-0:0).