# Frequently Asked Questions

## General Questions

### What's the difference between Hive and other distributed systems?

Hive focuses on **agent participation** in distributed computation. Unlike centralized cloud systems, Hive enables individuals and organizations to contribute computational resources to a marketplace, earning rewards while maintaining security and autonomy.

### Can I run Hive on my personal device?

Yes. Executors are available for Android, iOS, Windows, Linux, and macOS. You can join the marketplace and earn by participating.

### Is there a minimum task complexity?

No. Tasks can be simple (single step) or complex (multi-step DAGs with parallel branches). The runtime automatically optimizes execution.

## Technical Questions

### What languages can I use in tasks?

Tasks are platform-agnostic. You can invoke:
- Native binaries (compiled languages)
- Scripted languages (Python, JavaScript, etc.)
- Containerized applications
- HTTP APIs

### How do I debug task failures?

1. Check execution logs: `hive-executor logs --task-id <id>`
2. Review event stream for node-level errors
3. Test locally before marketplace submission
4. Use structured error handling in DAG definitions

### Can tasks communicate across executors?

No, by design. Each node runs independently. Communication happens through input parameters and output results, creating implicit ordering through DAG structure.

### What happens if an executor crashes mid-task?

HiveFabric detects the failure (heartbeat timeout) and reassigns to another executor. Already-completed nodes aren't re-executed; only failed nodes are retried.

## Marketplace Questions

### How is pricing determined?

Task creators specify maximum budget. Agents bid on tasks. Competition drives prices toward marginal cost. HiveFabric selects the cheapest available agent.

### What prevents cheating?

- **Cryptographic validation**: Results are signed and verified
- **Spot checking**: Random tasks re-executed by different executors
- **Reputation system**: Dishonest agents lose access
- **Slashing**: Deposit loss for misbehavior

### Can I get paid immediately?

Payments settle after task completion and validation (typically within minutes). Agents can withdraw to blockchain or traditional payment methods.

## Security Questions

### How are my tasks kept private?

- Tasks are encrypted in transit
- Results visible only to task creator
- Executor sandboxes prevent side-channel access
- Audit logs track all access

### Can executors see my task input/output?

Executors see the data they need to run your task. You should:
- Avoid embedding secrets in task definitions
- Use secure credential management
- Implement data obfuscation if needed

### Is the system quantum-resistant?

Current implementation uses RSA-3072 and ECDSA. Quantum-safe algorithms are on the roadmap.

## Performance Questions

### How long do tasks take to start?

Average: 2-5 seconds from submission to execution start. Includes HiveFabric routing, executor pickup, and sandbox setup.

### Can I set timeouts?

Yes, per-node and per-task timeouts are configurable:

```yaml
nodes:
  - id: "fetch"
    timeout_seconds: 300  # 5 minute timeout
```

### How do I optimize for cost?

- Use fewer parallel branches (reduces executor count)
- Request only necessary resources
- Prefer high-reputation, lower-cost executors
- Batch similar tasks for amortized overhead

## Support

For more help:
- Check [Architecture](architecture.md) for system design
- Review [Examples](agentfabric/examples.md) for patterns
- File an issue on GitHub
- Contact support@hive.io
