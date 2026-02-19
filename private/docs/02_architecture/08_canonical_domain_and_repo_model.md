# Canonical Domain and Repository Model

This document is the canonical specification for HiveFabric v0 architecture and data model.

## 1. Canonical Domain Model

### 1.1 Hive

```yaml
Hive:
  id: UUID
  name: string
  type: enum { GLOBAL, PRIVATE }
  queen_endpoint: string
  created_at: timestamp
  policy:
    max_cross_honeycomb_allocation: float
    scheduling_strategy: enum
```

### 1.2 Honeycomb

```yaml
Honeycomb:
  id: UUID
  hive_id: UUID
  owner_id: UUID
  name: string
  resource_limits:
    max_cpu_percent: float
    max_memory_percent: float
    max_cells: int
  status: enum { ACTIVE, DEGRADED, OFFLINE }
  created_at: timestamp
```

### 1.3 Comb (Node)

```yaml
Comb:
  id: UUID
  honeycomb_id: UUID
  hostname: string
  architecture: enum { ARM64, X86_64 }
  os: string
  capabilities: [string]
  resources:
    cpu_cores: int
    total_memory_mb: int
    available_memory_mb: int
    battery_percent: float?
  limits:
    max_cpu_percent: float
    max_memory_percent: float
    max_cells: int
  status: enum { ONLINE, OFFLINE, DEGRADED }
  last_heartbeat: timestamp
```

### 1.4 Cell

```yaml
Cell:
  id: UUID
  task_id: UUID
  comb_id: UUID
  agent_id: UUID
  state: enum { PENDING, RUNNING, COMPLETED, FAILED }
  resource_allocation:
    cpu_percent: float
    memory_mb: int
  created_at: timestamp
  started_at: timestamp?
  completed_at: timestamp?
  failure_reason: string?
```

### 1.5 Agent (Bee)

```yaml
Agent:
  id: UUID
  name: string
  version: string
  wasm_module_hash: string
  capabilities: [string]
  runtime_requirements:
    architecture: [ARM64, X86_64]
    min_wasm_version: string
  resource_requirements:
    cpu_percent: float
    memory_mb: int
  preferred_location: enum { LOCAL, HIVE, ANY }
  input_schema: JSONSchema
  output_schema: JSONSchema
```

### 1.6 Task

```yaml
Task:
  id: UUID
  hive_id: UUID
  honeycomb_id: UUID
  submitted_by: UUID
  priority: enum { LOW, NORMAL, HIGH }
  graph: TaskGraph
  state: enum { QUEUED, RUNNING, COMPLETED, FAILED }
  result_location: string?
  created_at: timestamp
  completed_at: timestamp?
```

### 1.7 TaskGraph (Fork-Join DAG)

```yaml
TaskGraph:
  nodes:
    - id: string
      agent_id: UUID
      dependencies: [string]
      input_mapping: object
```

### 1.8 Message Envelope (Hive Protocol)

```yaml
Message:
  id: UUID
  type: enum {
    HEARTBEAT,
    TASK_SUBMIT,
    TASK_ASSIGN,
    CELL_START,
    CELL_RESULT,
    CELL_FAIL
  }
  sender_id: UUID
  recipient_id: UUID
  payload: object
  signature: string
  encrypted: boolean
  timestamp: timestamp
```

## 2. Security Model

- All combs authenticate with API key (minimum baseline).
- Messages are signed with per-node private key.
- Transport is TLS.
- Cells execute inside Wax (WASM sandbox).
- No direct comb-to-comb communication by default.
- No inter-hive communication.

## 3. Repository Model (Bounded Contexts)

### 3.1 `hive-protocol` (Foundational)

Responsibilities:

- Canonical structs/schemas.
- Serialization contracts.
- Signing and verification helpers.
- Encryption helpers.

Suggested structure:

```text
/schemas
  agent.yaml
  task.yaml
  message.yaml
  comb.yaml
/src
  message.rs
  signature.rs
  encryption.rs
  heartbeat.rs
```

### 3.2 `hive-queen`

Responsibilities:

- Hive registry.
- Honeycomb registry.
- Global scheduling and federation policy.
- Cross-honeycomb allocation.
- Task intake/routing.

### 3.3 `honeycomb`

Responsibilities:

- Local scheduler (Honeybee).
- Comb registry and health.
- Cell lifecycle.
- Task graph orchestration.

Depends on:

- `hive-protocol`
- `wax-runtime`

### 3.4 `comb-node`

Responsibilities:

- Register with honeycomb.
- Report resources and heartbeat.
- Execute cells.
- Return status/result.

### 3.5 `wax-runtime`

Responsibilities:

- Load and run WASM modules.
- Enforce CPU/memory/timeout limits.
- Mount ephemeral filesystem.
- Return output and logs.

Constraint: keep this component small, auditable, and stable.

### 3.6 `task-engine` (optional extracted module)

Responsibilities:

- Parse `TaskGraph`.
- Resolve dependencies.
- Spawn cells.
- Join/aggregate results.

This may initially live inside `honeycomb` and be extracted later.

## 4. Build Priorities

Infrastructure-first sequence:

1. Wax sandbox/runtime baseline.
2. Protocol contracts and message envelope.
3. Honeycomb local scheduling and cell lifecycle.
4. Queen federation path.
5. Agent skill/model expansion and Apiary integration.
