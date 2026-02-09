# Pre-Code Checklist

This checklist captures the minimum decisions needed to start coding with minimal rework. Fill items as decisions are made.

1. **MVP Scope**: Which 1–2 end-to-end user workflows must work in v0?
2. **Language/Tooling Baseline**: Rust toolchain, WASM runtime choice (Wasmtime vs WAMR), package manager conventions.
3. **API Surface**: gRPC vs REST priority, auth model (JWT/OAuth/mTLS), initial resource schemas (Agent, Task, Executor).
4. **Data Model**: Postgres schema ownership, event sourcing vs CRUD, migration strategy.
5. **Runtime Limits**: Default CPU/RAM/timeouts for agent execution and any “no-go” permissions.
6. **Scheduling Policy v1**: Mandatory vs optional dimensions (cost, latency, trust, power state).
7. **Telemetry Minimums**: Must-have metrics and thresholds that will block release.
8. **Release Policy**: What qualifies a release candidate and who signs it off.
9. **Repo Split**: When to create control-plane/executor repos and how branching is synced.

Add notes under each item as decisions are made. Keep this list short and authoritative.
