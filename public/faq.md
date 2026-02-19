# FAQ

## What is Hive?

Hive is a distributed platform for orchestrating autonomous agent workloads across heterogeneous devices. The current focus is on building a reliable control plane and node telemetry layer.

## What is running today?

- Honeycomb control plane with REST APIs
- Stinger SDK for comb registration and heartbeat reporting
- Beekeeper UI for live comb/task visibility

## Is the marketplace live?

Not yet. Marketplace and economics are planned and are not active in the current release.

## Does Wax execute real workloads today?

Wax exists as a Rust runtime crate. Integration with Honeybee and task execution is in progress.

## Where should I start?

- Start the control plane: `hive/crates/ms-honeycomb`
- Start combs: `hive/crates/sdk-stinger`
- Open Beekeeper: `ui-beekeeper`

## How do I contribute?

Open a PR in the relevant repo and include a short design note when you change APIs or architecture.
