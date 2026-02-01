# AgentFabric Runtime Specification

## Overview

The AgentFabric runtime executes fork-join DAGs (Directed Acyclic Graphs) that define multi-step agent workflows.

## DAG Structure

### YAML Format

```yaml
version: "1.0"
name: "example-task"
description: "Example fork-join workflow"

nodes:
  - id: "fetch-data"
    type: "step"
    action: "fetch_from_source"
    params:
      source: "api"
  
  - id: "process-parallel"
    type: "fork"
    join_strategy: "all"
    children:
      - id: "process-a"
        type: "step"
        action: "process"
        params:
          variant: "a"
      
      - id: "process-b"
        type: "step"
        action: "process"
        params:
          variant: "b"
  
  - id: "aggregate"
    type: "step"
    action: "aggregate_results"
    depends_on:
      - "process-parallel"
```

### JSON Format

```json
{
  "version": "1.0",
  "name": "example-task",
  "nodes": [
    {
      "id": "fetch-data",
      "type": "step",
      "action": "fetch_from_source",
      "params": {"source": "api"}
    }
  ]
}
```

## Execution Model

### Fork-Join Semantics

- **Fork**: Create parallel branches of execution
- **Join**: Synchronize branches before proceeding
- **Join Strategies**: `all` (wait for all), `any` (first completes), `majority`

### State Management

Each node maintains:
- `status`: pending, running, completed, failed
- `output`: Result data from node execution
- `error`: Failure information (if applicable)

## Task Output

Tasks emit structured events during execution:

```json
{
  "task_id": "abc123",
  "node_id": "process-a",
  "timestamp": "2026-02-01T10:00:00Z",
  "event": "node_completed",
  "output": {...}
}
```

See [Examples](examples.md) for real-world patterns and [SDK](sdk.md) for programmatic APIs.
