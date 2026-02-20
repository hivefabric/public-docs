# FAQ

## What is Hive?

Hive is a distributed platform for orchestrating agent workloads across user-owned and platform-managed nodes, with IAM-scoped scheduling and marketplace-packaged skills.

## What is running today?

- `hive-control-plane` backend + UI
- `comb-node` runtime with registration, heartbeat, and execution reporting
- `apiary-market` service + UI catalog prototype
- `honeycomb` backend + UI scaffold with role-routed messaging

## Is the marketplace live?

An initial Apiary service/UI is available for skill catalog flows. Full production marketplace controls (signatures, policy, economics) are still maturing.

## Does Wax execute real workloads today?

Task execution is wired through control-plane and comb-nodes for UAT-level workflows. Runtime hardening is still in progress.

## Where should I start?

- Start control-plane: `hive-control-plane`
- Start apiary: `apiary-market`
- Start comb nodes: `comb-node`
- Start app layer: `honeycomb`

## How do I contribute?

Open a PR in the relevant repo and include a short design note when you change APIs or architecture.
