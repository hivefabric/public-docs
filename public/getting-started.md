# Getting Started

Run a local stack with control-plane backend + UI, Apiary service + UI, and comb nodes.

## Prerequisites

- Docker + Docker Compose
- Rust toolchain (for local service runs)
- Node.js 20+ (for UIs)

## 1. Start Hive Control Plane

```bash
cd hive-control-plane
docker compose \
  -f docker/docker-compose.with-ui-multi-node.yml \
  -f docker/docker-compose.with-ui-multi-node.local.yml \
  up -d
```

Verify:

```bash
curl -fsS http://localhost:8080/healthz
```

## 2. Start Apiary Service + UI

```bash
cd apiary-market
docker compose -f docker/docker-compose.yml up -d apiary-service apiary-ui
```

Verify:

```bash
curl -fsS http://localhost:8090/healthz
```

## 3. Start comb nodes

Included in the control-plane multi-node compose stack above.

## 4. Open UIs

- Control plane UI: `http://localhost:5175`
- Apiary UI: `http://localhost:5176`

## 5. Smoke test task submission

Create a task:

```bash
curl -X POST http://localhost:8080/api/tasks/create \
  -H 'content-type: application/json' \
  -H 'x-api-key: dev-hive-key' \
  -H 'x-user-role: admin' \
  -d '{"task_id":"00000000-0000-0000-0000-000000000123","agent":"queen-bee-advanced","description":"Plan distributed execution for a hello-world task"}'
```

List tasks:

```bash
curl -H 'x-api-key: dev-hive-key' -H 'x-user-role: admin' http://localhost:8080/api/tasks
```
