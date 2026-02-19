# LLM Strategy

HiveFabric uses an infrastructure-first, local-first LLM strategy.

## 1. Execution Preference Order

When an agent requires model-backed reasoning:

1. Prefer local execution in the current honeycomb.
2. If unavailable, route to another eligible honeycomb inside the same hive (policy permitting).
3. Use external providers (OpenAI/Anthropic/etc.) only when local/hive options cannot satisfy the request.

## 2. Agent-Centric Provider Use

External LLMs are treated as processing backends for agents, not as the control plane itself.

- Agents with orchestration skills can coordinate multi-agent workflows.
- Agents without orchestration skills run in wrapper mode and forward scoped requests.
- Provider selection and fallback are policy controlled.

## 3. Secrets and Access Model

- API keys are managed as secrets and referenced by agents/policies.
- Keys are never embedded in agent OCI definition artifacts.
- Access can be constrained per hive, honeycomb, task class, or agent capability.

## 4. Cost and Safety Controls

- Hard budget limits for external provider usage.
- Explicit fallback controls (including disabling external providers).
- Usage telemetry tied to task IDs for auditability.

## 5. Strategic Goal

Maximize useful work on owned/idle infrastructure first, and treat external LLM providers as optional augmentation for high-complexity workloads.
