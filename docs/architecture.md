# Hive System Architecture

## High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        Task Creators                         │
│                  (CLI, SDK, Web Interface)                   │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           ▼
┌─────────────────────────────────────────────────────────────┐
│                      HiveFabric                              │
│  ┌──────────────┐  ┌──────────────┐  ┌─────────────────┐   │
│  │ Task Router  │  │ Scheduler    │  │ Marketplace     │   │
│  └──────────────┘  └──────────────┘  └─────────────────┘   │
│  ┌──────────────┐  ┌──────────────┐  ┌─────────────────┐   │
│  │ State Store  │  │ Event Stream │  │ Audit Logger    │   │
│  └──────────────┘  └──────────────┘  └─────────────────┘   │
└──────────────────────────┬──────────────────────────────────┘
                           │
        ┌──────────────────┼──────────────────┐
        │                  │                  │
        ▼                  ▼                  ▼
    ┌────────┐         ┌────────┐        ┌────────┐
    │ Mobile │         │Desktop │        │ Cloud  │
    │Executor│         │Executor│        │Executor│
    └────────┘         └────────┘        └────────┘
    (Android/iOS)    (Linux/Win/Mac)  (Containers)
```

## Component Details

### HiveFabric (Control Plane)

**Task Router**: Routes incoming task definitions to appropriate executors based on:
- Required capabilities
- Cost optimization
- Load balancing
- Fault tolerance

**Scheduler**: Manages task queuing and execution scheduling:
- Priority queues per executor
- Deadline tracking
- Resource reservation
- Retry logic

**Marketplace**: Matches tasks to agents:
- Reputation scoring
- Price negotiation
- Availability checking
- Matchmaking algorithm

**State Store**: Persistent storage for:
- Task definitions and status
- Executor registrations
- Agent reputation data
- Payment records

**Event Stream**: Real-time event bus:
- Task progress updates
- Executor status changes
- Payment events
- Audit trail

### Executors

Each executor maintains:
- **Task Queue**: Pending tasks for this executor
- **Sandbox Manager**: Task isolation and resource control
- **Event Emitter**: Real-time status updates
- **Result Validator**: Cryptographic proof generation
- **Agent Interface**: Marketplace and state reporting

## Data Flow

### Task Execution Flow

```
1. Task Definition (YAML/JSON)
         │
         ▼
2. HiveFabric Validation
         │
         ▼
3. Marketplace Matching
         │
         ▼
4. Executor Assignment
         │
         ▼
5. Task Download & Validation
         │
         ▼
6. Sandbox Setup & Execution
         │
         ▼
7. Result Generation & Signing
         │
         ▼
8. Result Upload & Payment
```

### Event Stream

Events flow in real-time to task creators:

```json
{
  "task_id": "abc123",
  "timestamp": "2026-02-01T10:00:00Z",
  "events": [
    {"type": "scheduled", "executor": "desktop-1"},
    {"type": "node_started", "node_id": "fetch"},
    {"type": "node_completed", "node_id": "fetch", "output": {...}},
    {"type": "node_started", "node_id": "process"},
    {"type": "task_completed", "result": {...}}
  ]
}
```

## Fault Tolerance

- **Task Replay**: Failed tasks resubmitted to different executor
- **Partial Results**: Completed nodes cached to avoid re-execution
- **State Checkpointing**: Executor periodically saves progress
- **Deadline Enforcement**: Tasks with unmet deadlines fail explicitly

## Scalability

- Horizontal executor scaling (add more executors)
- Marketplace manages supply/demand
- Event streaming handles real-time coordination
- Sharded state store for large deployments

See [Executors](executors/) and [AgentFabric Runtime](agentfabric/) for implementation details.
