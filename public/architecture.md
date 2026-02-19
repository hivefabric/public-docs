# Architecture Overview

HiveFabric follows an infrastructure-first architecture for distributed edge compute.

## Core Hierarchy

- **HiveFabric**: platform boundary.
- **Hive**: federated compute domain (`GLOBAL` or `PRIVATE`).
- **Honeycomb**: owner-scoped cluster inside a hive.
- **Comb**: machine/node in a honeycomb.
- **Cell**: ephemeral isolated execution unit.
- **Agent (Bee)**: capability unit executed 1:1 in a cell.

## Control Planes

- **Queen Bee (Hive level)**: federation and cross-honeycomb scheduling.
- **Honeybee (Honeycomb level)**: local scheduling and cell lifecycle.

## Runtime and Security

- All cell execution is sandboxed in Wax (WASM runtime).
- Scheduling respects device/resource limits configured by users.
- Encrypted transport and signed messaging are mandatory design goals.

## Current Status

The codebase is in active transition from early single-service prototypes to this bounded-context model. See private architecture docs for canonical data model and repository boundaries.
