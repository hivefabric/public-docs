# Honeybee (UI Shell)

Honeybee is the cross-platform UI shell intended to host Wax and orchestrate agent workflows. The current version is a React + Vite app that connects to Honeycomb.

## Run locally

```bash
cd ui-honeybee
npm install
VITE_CONTROL_PLANE_URL=http://localhost:8080 npm run dev
```

Honeybee is intentionally minimal today; it will grow into the primary orchestration UI.
