# Executors

Executors are worker nodes that execute AgentFabric tasks. Hive supports executors across multiple platforms.

## Executor Types

- **[Mobile](mobile.md)** - Android and iOS devices
- **[Desktop](desktop.md)** - Windows, Linux, macOS machines
- **[Cloud](security.md)** - Containerized and managed services

## Key Concepts

### Registration
Executors register with HiveFabric and advertise capabilities:
- Platform (mobile, desktop, cloud)
- Resource constraints (CPU, memory, storage)
- Supported actions
- Security posture

### Task Acceptance
An executor:
1. Receives a task assignment from HiveFabric
2. Validates resource requirements
3. Executes the task in a sandboxed environment
4. Streams execution events back
5. Reports completion or failure

### Security & Isolation
All executors enforce:
- **Sandboxing**: Tasks run in isolated environments
- **Resource Control**: CPU, memory, network limits
- **Audit Logging**: All actions are logged
- **Authentication**: Cryptographic verification of task origin

See [Security](security.md) for detailed isolation models.
