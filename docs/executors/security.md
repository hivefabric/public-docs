# Executor Security Model

Hive implements defense-in-depth security for all executors.

## Sandboxing

### Container Isolation (Linux/Desktop)

Tasks run in Docker containers or VMs with:
- Separate filesystem root
- Network namespace isolation
- Resource quotas (cgroups)
- Read-only system files

```dockerfile
# Example task container
FROM alpine:3.18
RUN apk add python3
COPY task.py /task/
WORKDIR /task
ENTRYPOINT ["python3", "task.py"]
```

### App Sandboxing (Mobile)

Android:
- SELinux policies
- Runtime permission model
- App-specific storage isolation

iOS:
- XPC services
- App container restrictions
- Entitlement-based access control

## Resource Control

All executors enforce limits:

```yaml
tasks:
  cpu_limit: "2000m"
  memory_limit: "1Gi"
  disk_limit: "10Gi"
  network_egress_limit: "100Mb/s"
  timeout_seconds: 3600
```

## Audit Logging

Every task execution logs:
- Task ID and definition
- Executor node and timestamp
- Input parameters
- Output and exit status
- Resource usage
- Security events (permission denials, etc.)

```json
{
  "timestamp": "2026-02-01T10:00:00Z",
  "task_id": "abc123",
  "executor": "desktop-1",
  "event": "task_completed",
  "resources_used": {
    "cpu_ms": 5000,
    "memory_peak_mb": 512,
    "disk_mb": 100
  }
}
```

## Cryptographic Verification

- Tasks are signed by HiveFabric
- Executors verify signatures before execution
- Results are signed by executors
- Chain of custody maintained

## Best Practices for Task Authors

1. Request minimum necessary permissions
2. Use resource constraints appropriate to your task
3. Implement error handling gracefully
4. Avoid hardcoding secrets; use secure credential stores
5. Sanitize all external inputs
