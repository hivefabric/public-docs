# Scheduling Model

HiveFabric scheduling is hierarchical and constraint-driven.

## 1. Two-Level Scheduling

1. **Hive-level placement (Queen Bee)**
   - Selects target honeycomb for each task/cell batch.
   - Applies hive policies and cross-honeycomb allocation limits.
2. **Honeycomb-level placement (Honeybee)**
   - Selects target comb and allocates cells locally.
   - Enforces per-device limits and runtime compatibility.

## 2. Scheduling Inputs

Placement decisions evaluate:

- Device architecture and runtime compatibility.
- Available CPU/memory and configured max usage percent.
- Maximum allowed cells per comb.
- Battery, charging state, thermal pressure, and network quality.
- Local-first preference before cross-honeycomb allocation.
- Task priority (`LOW`, `NORMAL`, `HIGH`).

## 3. Task Graph Execution

Task execution uses a DAG model (`TaskGraph`):

- Independent nodes can run in parallel.
- Dependencies gate downstream execution.
- Join/aggregation nodes combine intermediate outputs.

Fork-join is the baseline model. More advanced patterns (consensus, iterative loops) are represented as graph patterns above the same cell lifecycle.

## 4. Failure and Recovery

- Heartbeat loss marks comb offline.
- Running cells on unavailable combs are reconciled and requeued.
- Retry policy is task-defined and bounded.
- Partial results can be retained when graph semantics allow it.

## 5. Safety Constraints

- Scheduling never exceeds user-defined device limits.
- Cells are rejected if required resources cannot be reserved.
- No scheduling path bypasses Wax sandbox execution.
