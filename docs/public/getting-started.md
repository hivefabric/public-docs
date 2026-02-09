# Getting Started

This guide gets a local Hive stack running with the control plane, comb clients, and the Beekeeper UI.

## Prerequisites

- Docker + Docker Compose
- Rust toolchain (optional, for running from source)
- Node.js 20+ (for Beekeeper and Honeybee UIs)

## 1. Start Honeycomb (control plane)

From the `hive` repo:

```bash
cd hive/crates/ms-honeycomb
docker compose up --build
```

Verify health:

```bash
curl -fsS http://localhost:8080/health
```

## 2. Start comb clients with Stinger

Option A: Docker compose helper (recommended)

```bash
cd hive/crates/sdk-stinger
./scripts/run.sh -s 2
```

Option B: Run from source

```bash
cd hive
cargo run -p sdk-stinger -- --base-url http://localhost:8080 --id comb-1 --mode both
```

## 3. Launch Beekeeper UI

```bash
cd ui-beekeeper
npm install
VITE_API_BASE_URL=http://localhost:8080 npm run dev -- --host 127.0.0.1
```

Beekeeper defaults to port `5173`.

## 4. (Optional) Launch Honeybee UI

```bash
cd ui-honeybee
npm install
VITE_CONTROL_PLANE_URL=http://localhost:8080 npm run dev
```

## Expected result

- `GET /combs` returns active combs
- Beekeeper lists combs and their latest report data
- `GET /tasks` returns the pending tasks queue (if any)

If you see combs but no data, confirm the Stinger base URL and that the Honeycomb container can be reached at `http://localhost:8080`.
