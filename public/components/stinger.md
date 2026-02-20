# Comb Node Runtime

This page describes the current comb-node runtime (historically referred to as Stinger in older docs).

## Responsibilities

- Authenticate to control-plane using IAM-compatible API key flow.
- Register node capabilities.
- Send periodic heartbeats to renew lease.
- Receive/execute assigned tasks and post task events.

## Run with Docker

```bash
cd comb-node
docker compose -f docker/docker-compose.multi-node.yml up -d comb-node-1 comb-node-2
```

## Integration points

- Register: `POST /api/nodes/register`
- Heartbeat: `POST /api/nodes/heartbeat`
- Task events: `POST /api/tasks/{task_id}/events`

## Notes

- Heartbeat cadence should remain below lease TTL (typically half-lease interval).
- Node filtering and task placement are control-plane decisions, not node-local logic.
