# Honeycomb / Control Plane

Honeycomb is the control-plane service used by nodes, UIs, and app-layer services.

## Responsibilities

- Node registration/heartbeat with lease renewal and expiry cleanup.
- Task lifecycle management with scheduler-driven state transitions.
- Task dispatch to node execution endpoints.
- Task event ingestion + websocket stream fanout.
- Role-aware APIs for Queen Bee / Worker Bee prompt submission.
- Usage and metrics surfaces for observability.

## Main endpoints

- `GET /healthz`
- `POST /api/nodes/register`
- `POST /api/nodes/heartbeat`
- `GET /api/nodes`
- `POST /api/tasks/create`
- `GET /api/tasks`
- `POST /api/tasks/{task_id}/events`
- `GET /api/tasks/{task_id}/stream`
- `POST /api/workflows/submit`
- `POST /api/prompts/queen-bee`
- `POST /api/prompts/worker-bee`
- `GET /api/usage/summary`

## Developer surfaces

- OpenAPI: `GET /api-doc/openapi.json`
- Swagger UI: `GET /swagger-ui`
- Metrics: `GET /metrics`, `GET /metrics/prometheus`
