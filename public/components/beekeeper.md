# Control Plane UI

The control-plane UI visualizes nodes, task status, and scheduling outcomes.

## Run locally

```bash
cd hive-control-plane/ui
npm install
npm run dev
```

Default port: `5175` (config-dependent).

## What it shows

- Node inventory and capabilities (`/api/nodes`)
- Task lifecycle and assignment state (`/api/tasks`)
- Queue/execution timing and recent logs

See `hive-control-plane/ui/README.md` for environment and deployment details.
