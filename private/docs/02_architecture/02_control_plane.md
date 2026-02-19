# Control Plane Architecture (Queen Bee + Honeybee)

HiveFabric uses a hierarchical control model instead of a single monolithic scheduler.

## 1. Queen Bee (Hive-Level Control Plane)

Queen Bee is responsible for hive-wide coordination:

- Hive and honeycomb registry.
- Cross-honeycomb allocation decisions.
- Global task intake and routing.
- Hive policy enforcement (limits, placement rules, isolation boundaries).
- Secure message validation and routing.

Queen Bee does not execute workloads directly.

## 2. Honeybee (Honeycomb-Level Control Plane)

Honeybee is the local control plane for one honeycomb:

- Comb registration and heartbeat tracking.
- Local task decomposition into cells.
- Cell scheduling against comb capabilities and user-defined limits.
- Cell lifecycle management (create, monitor, terminate, retry).
- Local telemetry and status reporting to Queen Bee.

Honeybee is where device-specific constraints are enforced (CPU, memory, battery, thermal, and max cells).

## 3. Communication Model

- All routing is mediated by Queen Bee or Honeybee.
- No direct comb-to-comb communication by default.
- No inter-hive communication (hive boundary is an isolation boundary).
- Message exchange uses a signed/encrypted envelope.

## 4. Reliability Model

The control plane assumes unreliable conditions:

- Network partition and latency are normal states.
- Heartbeat expiry marks combs unavailable.
- Orphaned/failed cells are requeued by reconciliation loops.
- At-least-once task delivery is preferred over silent loss.

## 5. Security Baseline

- API key auth for comb registration and API access.
- Message signing with per-node keys.
- TLS transport for all control-plane communication.
- Wax WASM sandbox required for all cell execution.

## 6. State and Persistence

Initial persistence target is PostgreSQL for metadata and lifecycle state. The model is intentionally modular so storage can evolve without changing domain contracts.
