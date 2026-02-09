# Architecture Overview

Hive is split into a control plane, lightweight SDK clients, and runtime components. The core flow is:

1. Honeycomb exposes REST/gRPC endpoints for comb registration and task telemetry.
2. Stinger clients register combs and send periodic heartbeat reports.
3. UIs (Beekeeper/Honeybee) poll Honeycomb to display real-time system status.
4. Wax (runtime) executes WASM workloads (early-stage integration).

## Components at a glance

- **Honeycomb (ms-honeycomb)**: Control plane service. Owns comb registry and task queue.
- **Stinger (sdk-stinger)**: Client SDK/CLI for combs.
- **Wax (runtime-wax)**: WASM runtime, early-stage.
- **Beekeeper (ui-beekeeper)**: Control plane visualization UI.
- **Honeybee (ui-honeybee)**: UI shell that will host Wax.

## Data flow (today)

- Stinger sends `CombReport` via `/combs/register` and `/combs/heartbeat`.
- Honeycomb stores the latest heartbeat in memory and exposes it via `/combs`.
- Beekeeper polls `/combs` and `/tasks` to render status and charts.

For deeper internal diagrams and architecture notes, refer to the private documentation set.
