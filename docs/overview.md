# Overview: Hive, HiveFabric, and AgentFabric

## What is Hive?

Hive is a distributed execution platform designed for complex, multi-step agent workflows. It enables organizations to:

- Define agent tasks as composable, fork-join DAGs
- Execute tasks across heterogeneous executors (mobile, desktop, cloud)
- Manage agent economics through a marketplace model
- Ensure security and resource control across execution boundaries

## Architecture Components

### HiveFabric
The **control plane** and orchestration layer that:
- Accepts task definitions (YAML/JSON)
- Manages execution scheduling and state
- Coordinates with multiple executors
- Handles authentication and authorization

### AgentFabric Runtime
The **task execution engine** that:
- Interprets fork-join DAG specifications
- Manages parallel and sequential task execution
- Provides SDK/APIs for task composition
- Emits execution events and telemetry

### Executors
**Worker nodes** that execute tasks:
- **Mobile**: Android and iOS devices
- **Desktop**: Windows, Linux, macOS machines
- **Cloud**: Containerized environments

## Use Cases

- Multi-step AI workflows with human-in-the-loop steps
- Distributed data processing pipelines
- Agent orchestration across device networks
- Marketplace-based computation

See [Architecture](architecture.md) for system design details.
