# Honeycomb (Control Plane)

Honeycomb is the stateless control-plane service. It manages comb registration, heartbeat tracking, and a pending task queue backed by NATS.

## What it provides

- Comb registration and heartbeat endpoints
- In-memory comb registry with last report
- Task queue and NATS publishing
- REST + gRPC API surface

## REST endpoints

- `GET /health`
- `POST /combs/register`
- `POST /combs/heartbeat`
- `GET /combs`
- `GET /tasks`

## Environment variables

- `REST_PORT` (default: 8080)
- `GRPC_PORT` (default: 50051)
- `NATS_URL` (default: nats://127.0.0.1:4222)
- `NATS_EMBEDDED` (default: false)
- `NATS_SERVER_BIN` (default: nats-server)
- `CONFIG_PATH` (optional)
- `REGISTER_TEST_DATA` (optional)

## Run with Docker

```bash
cd hive/crates/ms-honeycomb
docker compose up --build
```

## Run from source

```bash
cd hive
cargo run -p ms-honeycomb
```

## Related docs

See `hive/crates/ms-honeycomb/README.md` for full CLI flags and deployment notes.
