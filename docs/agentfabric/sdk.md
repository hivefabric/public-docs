# AgentFabric SDK/API Reference

## Overview

The AgentFabric SDK provides programmatic APIs for task composition, submission, and monitoring.

## Core APIs

### Python SDK

```python
from agentfabric import Task, Fork, Step

# Define a task
task = Task(name="my-workflow")

# Add sequential steps
task.add_step(Step(
    id="fetch",
    action="fetch_data",
    params={"source": "api"}
))

# Add parallel branches
fork = Fork(id="parallel-processing", join_strategy="all")
fork.add_child(Step(id="process-a", action="process", params={"variant": "a"}))
fork.add_child(Step(id="process-b", action="process", params={"variant": "b"}))
task.add_node(fork)

# Submit task
result = task.submit(executor="auto")
```

### REST API

```bash
POST /api/v1/tasks
{
  "definition": {...}
}

GET /api/v1/tasks/{task_id}
GET /api/v1/tasks/{task_id}/events
```

## Event Streaming

Monitor task execution in real-time:

```python
task = Task.get(task_id)
for event in task.stream_events():
    print(f"Node {event.node_id}: {event.status}")
```

## Error Handling

```python
try:
    result = task.submit()
except TaskError as e:
    print(f"Task failed: {e.node_id} - {e.message}")
```

See [Examples](examples.md) for integration patterns.
