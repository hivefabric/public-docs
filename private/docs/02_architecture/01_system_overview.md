# System Architecture Overview

HiveFabric is designed as an edge-native distributed compute platform with a strict hierarchy:

1. **HiveFabric**: the global platform boundary (company/product scope).
2. **Hive**: a federated compute domain (`GLOBAL` or `PRIVATE`) and the top isolation boundary.
3. **Honeycomb**: an owner-scoped cluster inside a hive.
4. **Comb**: a machine/node in a honeycomb.
5. **Cell**: an ephemeral isolated execution unit on a comb.
6. **Agent (Bee)**: executable capability unit, deployed 1:1 as a cell.

## Platform Layers

- **Infrastructure layer**: Hive, Honeycomb, Comb, Cell lifecycle, scheduling, identity, encryption, and policy.
- **Software layer**: Agents, skill manifests, task graphs, and optional external LLM providers.
- **Management layer**: Apiary (registry/marketplace and management UX; evolves independently from core scheduling).

## Control Hierarchy

- **Queen Bee (Hive-level)**: federation coordinator for cross-honeycomb placement and hive policy enforcement.
- **Honeybee (Honeycomb-level)**: local scheduler/orchestrator for comb and cell lifecycle.

This keeps the control plane Kubernetes-shaped (declarative, reconciliation-based) without being Kubernetes-bound.

## Trust and Failure Assumptions

- Nodes, networks, and agents are treated as potentially unreliable.
- Disconnections and latency are expected; retries and reconciliation are first-class behavior.
- No direct communication between hives.
- Cell execution is always sandboxed by Wax (WASM runtime).

## High-Level Diagram

```
+--------------------------- HiveFabric ----------------------------+
|                                                                   |
|  +------------------- Hive (GLOBAL or PRIVATE) ----------------+  |
|  |  Queen Bee (federation + policy)                            |  |
|  |                                                             |  |
|  |  +--------------- Honeycomb A ---------------------------+  |  |
|  |  | Honeybee (local scheduler)                            |  |  |
|  |  |  +---------+  +---------+                             |  |  |
|  |  |  | Comb 1  |  | Comb 2  | ...                         |  |  |
|  |  |  | Cells   |  | Cells   |  (Agent 1:1 Cell)          |  |  |
|  |  |  +---------+  +---------+                             |  |  |
|  |  +-------------------------------------------------------+  |  |
|  |                                                             |  |
|  |  +--------------- Honeycomb B ---------------------------+  |  |
|  |  | Honeybee + Combs + Cells                               |  |  |
|  |  +-------------------------------------------------------+  |  |
|  +-------------------------------------------------------------+  |
|                                                                   |
|  Apiary (management + registry + marketplace, separate scope)     |
+-------------------------------------------------------------------+
```

## Canonical Reference

For canonical data model and repository boundaries, see `private/docs/02_architecture/08_canonical_domain_and_repo_model.md`.
