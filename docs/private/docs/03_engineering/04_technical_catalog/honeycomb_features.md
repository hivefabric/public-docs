# Honeycomb Control Plane Features

This document records the concrete features that the Honeycomb control-plane currently implements so the wider team (AI personas + humans) can refer back to the working surface that is already delivered.

## Runtime / API surface

1. **Stateless Honeycomb process** that runs REST and gRPC servers simultaneously, wired to a `TaskController`/`CombController` pair plus a NATS queue for messaging. It exposes `/combs` and `/tasks` endpoints (REST + gRPC) plus direct NATS publishing/subscribing channels for HEADLESS agents. citehive/crates/ms-honeycomb/README.md:1
2. **Configurable entry points** via `REST_PORT`, `GRPC_PORT`, `NATS_URL`, and `NATS_EMBEDDED` so deployments (Docker Compose, Kubernetes, local binary) can choose their ports and messaging endpoint without code changes. citehive/crates/ms-honeycomb/README.md:20

## Execution & orchestration logic

3. **Comb lifecycle management** (registering, heartbeating, pruning inactive combs) lives in `hive/crates/ms-honeycomb/src/controller.rs`, which keeps comb metadata with heartbeat timestamps and exposes helpers such as `list_active` and `remove_inactive`. citehive/crates/ms-honeycomb/src/controller.rs:10
4. **Task scheduling loop** continuously polls pending tasks, assigns them round-robin to active combs, and logs assignment actions; test helpers allow immediate assignment/immediately seeding tasks for integration validation. citehive/crates/ms-honeycomb/src/controller.rs:49
5. **NATS-backed queue layer** (`hive/crates/ms-honeycomb/src/queue.rs`) serializes tasks to JSON on the `tasks` subject and feeds them back into the controller loop via `subscribe_tasks`. citehive/crates/ms-honeycomb/src/queue.rs:20

## Engineering and delivery

6. **Docker Compose and Helm** support allow running Honeycomb locally, containerizing it, or deploying it into Kubernetes with Helm charts; documentation points to these resources for contributors. citehive/crates/ms-honeycomb/README.md:1hive/crates/ms-honeycomb/docker-compose.yml:1hive/crates/ms-honeycomb/helm/ms-honeycomb/Chart.yaml:1
7. **Tests** span controller logic, queue logic, config parsing, and REST handler checks so the Honeycomb behavior is verified through unit and integration suites before release. citehive/crates/ms-honeycomb/src/controller.rs:96hive/crates/ms-honeycomb/src/queue.rs:78hive/crates/ms-honeycomb/src/config.rs:74hive/crates/ms-honeycomb/tests/rest_tests.rs:1

Recording these features keeps the docs repo aligned with the repository state so both humans and AI teams know what’s implemented vs. what’s still planned.
