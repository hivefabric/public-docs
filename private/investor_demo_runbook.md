# Investor Demo Runbook (2026-02-20)

Goal: demonstrate Hive scheduling, node orchestration, UI visibility, and marketplace wiring locally.

## 1. Bring up core stack

```bash
cd /Users/xivi/Code/hive-fabric

# Control-plane + 2 comb nodes + control-plane UI (local images)
docker compose \
  -f hive-control-plane/docker/docker-compose.with-ui-multi-node.yml \
  -f hive-control-plane/docker/docker-compose.with-ui-multi-node.local.yml \
  up -d
```

## 2. Verify control-plane health

```bash
curl -fsS http://localhost:8080/healthz
curl -fsS -H 'x-api-key: dev-hive-key' -H 'x-user-role: admin' http://localhost:8080/api/nodes | jq .
```

Expected:
- health returns `{"ok":true}`
- at least 2 nodes visible

## 3. Start Apiary catalog (Docker)

```bash
docker compose -f apiary-market/docker/docker-compose.yml up -d apiary-service apiary-ui
curl -fsS http://localhost:8090/healthz
```

Expected:
- Apiary service healthy
- Apiary UI available (default `http://localhost:5176`)

## 4. UI walkthrough

- Control-plane UI: `http://localhost:5175`
  - Show node list
  - Show task table (state, assignment, timing fields)
- Apiary UI: `http://localhost:5176`
  - Show catalog entries and search

## 5. Submit orchestration prompt

```bash
curl -X POST http://localhost:8080/api/prompts/queen-bee \
  -H 'content-type: application/json' \
  -H 'x-api-key: dev-hive-key' \
  -H 'x-user-role: admin' \
  -d '{"message":"Plan distributed processing for investor demo","agent":"queen-bee-advanced"}'
```

Then inspect tasks:

```bash
curl -fsS -H 'x-api-key: dev-hive-key' -H 'x-user-role: admin' http://localhost:8080/api/tasks | jq .
```

## 6. Stabilization report

```bash
cargo run --manifest-path hive-dogfood/Cargo.toml --bin hive-dogfood -- \
  --control-plane-url http://localhost:8080 \
  --api-key dev-hive-key \
  stabilize --min-nodes 2 --wasm-module-path /tmp/mock.wasm --llm-profile code-fast
```

Expected:
- machine-readable JSON report for scenario pass/fail.

## 7. Demo talking points

- Deterministic task lifecycle with scheduler-driven transitions.
- Node registration + heartbeat + lease model in action.
- Queen/Worker orchestration routes and IAM role boundaries.
- PDCA loop scaffolding and experiment tracking in Honeycomb.
- Apiary OCI-oriented packaging/indexing foundation.
