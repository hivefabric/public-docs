# API Reference (Public)

This page documents currently available local/dev APIs.

## Hive Control Plane (`http://localhost:8080`)

Auth headers expected by most endpoints:

- `x-api-key: <key>`
- `x-user-role: admin|user`

Core endpoints:

- `GET /healthz`
- `GET /api/nodes`
- `POST /api/nodes/register`
- `POST /api/nodes/heartbeat`
- `GET /api/tasks`
- `POST /api/tasks/create`
- `POST /api/tasks/{task_id}/events`
- `GET /api/tasks/{task_id}/stream` (websocket)
- `POST /api/workflows/submit`
- `POST /api/prompts/queen-bee` (admin/platform-scoped)
- `POST /api/prompts/worker-bee` (user-scoped, sandboxed)
- `GET /api/usage/summary`
- `GET /metrics`
- `GET /metrics/prometheus`
- `GET /api-doc/openapi.json`
- `GET /swagger-ui`

Simplified task creation payload example:

```json
{
  "task_id": "00000000-0000-0000-0000-000000000123",
  "agent": "queen-bee-advanced",
  "description": "Plan distributed execution for project X"
}
```

## Honeycomb Service (`http://localhost:8090` by default)

User app API:

- `POST /api/login`
- `GET /api/dashboard`
- `POST /api/messages`
- `POST /api/tasks/submit`
- `GET /api/loop/status`
- `POST /api/loop/run-once`
- `POST /api/loop/enabled`
- `GET /api/embedded-node/status`
- `POST /api/embedded-node/start`
- `POST /api/embedded-node/stop`

## Apiary Service (`http://localhost:8090` in Apiary stack)

Catalog API:

- `GET /healthz`
- `GET /api/skills`
- `GET /api/skills/search?q=...`
- `POST /api/skills`

Role hints:

- `x-user-role: user|admin`
- `x-user-id: <uuid>`

## Notes

- Ports can differ per compose profile.
- Honeycomb service and Apiary service both default to `8090` in their own stacks; change one port when running both on the same host.
- Contracts are still evolving; prefer OpenAPI (`/api-doc/openapi.json`) for control-plane service details.
