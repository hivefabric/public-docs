# Architecture Overview

Hive currently runs as a control-plane + node runtime model with IAM-scoped APIs and marketplace-backed skills.

## Runtime Topology

- `hive-control-plane/service`: scheduler, task state manager, node registry, metrics, task streaming.
- `comb-node`: execution runtime that registers, heartbeats, receives task dispatch, and reports task events.
- `hive-control-plane/ui`: operator UI for node/task state.
- `apiary-market/service` + `apiary-market/ui`: skill catalog and OCI-oriented packaging/indexing toolchain.
- `honeycomb/service` + `honeycomb/ui`: user app layer (auth, role-routed messaging, embedded node controls, loop scaffold).

## Canonical Contracts

- Node lifecycle: lease-based register + heartbeat + automatic expiry.
- Task lifecycle: `Created -> Queued -> Scheduled -> Running -> Succeeded|Failed|TimedOut -> Retried|Cancelled`.
- Identity: API keys and roles resolved through IAM; no parallel identity model.
- Scheduling: control-plane is state-driven and places tasks on eligible nodes by capability and scope.

## Execution Boundaries

- Control-plane owns scheduling and task state transitions.
- Nodes execute and report completion/events, but do not own scheduler state.
- Worker-scoped flows are restricted to user-owned nodes; platform flows remain admin-gated.

## Current Maturity

- Control-plane task execution and status transitions are functional for manual/UAT flows.
- Marketplace and Honeycomb app are scaffolded and integrated at API level.
- Persistence remains lightweight/in-memory for core state in current iteration.
