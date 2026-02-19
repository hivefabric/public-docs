# Repository Organization and Cross-Repo Context

This map tracks both current repositories and the target bounded contexts for the next architecture phase.

## 1. Current Workspace Repositories

| Repo Name | Purpose | Notes |
|---|---|---|
| `docs` | Public/private documentation and architecture decisions | Source of truth for definitions and ADR-like docs |
| `hive-sdk` | Rust workspace for current control-plane/runtime/sdk prototypes | Includes `ms-honeycomb`, `stinger`, `runtime-wax`, `queen-bee`, `data-models` |
| `honeycomb` | UI and supporting components under active iteration | Legacy/transition surface |
| `ui-honeybee` | User-facing web shell | Early console and UX experiments |
| `hivefabric.github.io` | Public website | Marketing and public positioning |
| `apiary` | Early management/marketplace workspace | Planned to evolve with registry/economic layer |

## 2. Target Bounded Context Repositories (Planned)

| Target Repo | Responsibility |
|---|---|
| `hive-protocol` | Canonical schemas, message envelope, signing/encryption helpers |
| `hive-queen` | Hive-level control plane (federation + cross-honeycomb scheduling) |
| `honeycomb` | Honeycomb-level control plane (comb registry + local scheduling + cell lifecycle) |
| `comb-node` | Node agent that executes cells and reports telemetry/heartbeats |
| `wax-runtime` | WASM sandbox runtime used by all cells |
| `task-engine` | DAG/fork-join orchestration engine (optional extraction from honeycomb) |
| `apiary` | Management UX + registry/marketplace layer (adjacent, not core scheduler) |

## 3. Coordination Rules

- Keep the domain contract in `hive-protocol` authoritative.
- Treat Wax as the mandatory execution boundary for cells.
- Keep no direct inter-hive communication.
- When responsibilities move between repos, update this map in the same PR.
