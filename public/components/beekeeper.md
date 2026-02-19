# Beekeeper (Control Plane UI)

Beekeeper is the React-based UI for Honeycomb. It visualizes comb inventory, task queue, and API activity.

## Run locally

```bash
cd ui-beekeeper
npm install
VITE_API_BASE_URL=http://localhost:8080 npm run dev -- --host 127.0.0.1
```

Beekeeper defaults to port `5173`.

## What it shows

- Active combs with the latest report
- Pending tasks from the Honeycomb queue
- Live polling controls and telemetry views

See `ui-beekeeper/README.md` for build and production details.
