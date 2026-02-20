# Runtime (WASM and Task Execution)

Hive executes tasks on comb-nodes with sandboxed runtime constraints. WASM remains the primary portable module target for platform agents.

## Current status

- Task execution pipeline is connected through control-plane scheduling and node event reporting.
- WASM-centric agent packaging is scaffolded through Apiary metadata and OCI artifacts.
- Runtime hardening (resource limits, trust policy, and broader module support) is still in progress.

## Related modules

- `comb-node` for execution host/runtime integration
- `hive-control-plane/service` for scheduler and lifecycle control
- `apiary-market` for packaging/index contracts
