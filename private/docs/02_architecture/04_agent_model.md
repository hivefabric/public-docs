# Agent Model

HiveFabric agents (bees) are capability units executed in isolated cells.

## 1. Core Rules

- Agents are deployed 1:1 as cells.
- Cells are ephemeral and sandboxed by Wax.
- Agent definitions are declarative; runtime implementation is separate.
- Agent behavior is capability-driven (skills + limits), not implicit.

## 2. Agent Types

- **Orchestrator agent** (example: Queen Bee extensions): can decompose tasks and coordinate other agents.
- **Worker agent**: performs one scoped task (reasoning, retrieval, transform, validation, etc.).
- **Wrapper agent**: if orchestration skills are missing, acts as a client/wrapper around external providers.

## 3. Skill and Capability Model

Each agent declares:

- Functional skills/capabilities.
- Resource requirements (CPU, memory, timeout).
- Runtime requirements (arch, wasm compatibility).
- Input/output schemas.

If an agent lacks multi-agent coordination skills, it must run in wrapper mode and cannot spawn/coordinate swarms.

## 4. External LLM Provider Integration

Agents may use external providers (OpenAI, Anthropic, etc.) as processing backends, but:

- API keys are referenced as secrets, never embedded in agent packages.
- Provider access is policy-controlled.
- Local execution remains the default preference where possible.

## 5. OCI Packaging Model

Agent definition artifacts are distributed as OCI artifacts (not Docker containers):

- `agent.yaml` / manifest and schemas.
- Skill metadata/bundles.
- Policy metadata.

Runtime binaries and secrets are not part of the definition artifact. This keeps supply chain and execution concerns separate.

## 6. Security Requirements

- Signed artifacts only.
- Runtime sandbox enforcement by Wax.
- Explicit capability permissions.
- Encrypted transport and signed messaging.
