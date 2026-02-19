# Founder Conversation Context (Canonical Input)

Purpose: preserve the founder's long-form strategy and architecture discussion as reusable context for future planning, prompting, and implementation decisions.

Status: working context input (not a normative spec).  
Normative architecture/spec lives in:
- `docs/private/docs/02_architecture/08_canonical_domain_and_repo_model.md`
- `docs/private/docs/02_architecture/04_agent_model.md`
- `docs/private/docs/03_engineering/04_technical_catalog/repo_map.md`

## Why this exists

This project has a lot of intentional naming and product direction (Hive, Honeycomb, Apiary, Wax, combs, cells, queen-bee). That emerged from iterative founder conversations and should remain available as shared context for humans and AI agents.

This file is the canonical place to store that conversation context so it does not get lost in chat history.

## Conversation-derived decisions

1. Build sequence: infrastructure first, then advanced multi-agent layers.
2. Architecture direction: Kubernetes-shaped but Kubernetes-bound only where useful.
3. Core domain nouns:
- `HiveFabric` as company/system umbrella.
- `Apiary` for management/marketplace concerns (possibly adjacent scope).
- `Hive` as sharing/isolation boundary (global/private).
- `Honeycomb` as user-owned aggregate of nodes.
- `Comb` as an individual compute node.
- `Cell` as ephemeral isolated execution unit (pod-like).
- `Wax` as mandatory WASM sandbox runtime.
4. Security stance:
- Cell-level isolation via WASM runtime.
- Expect unreliable/disconnected nodes; design for distrust.
- Encrypted communications as baseline.
- No inter-hive communication by default.
5. Resource governance:
- User-defined caps per device; system must never exceed configured resource percentages.
- Agent specs must declare capabilities and resource needs.

## Product intent captured from the conversation

- Use idle edge/personal hardware first, with optional fallback to external LLM APIs.
- Enable a contributor economy where individuals contribute compute and companies buy capacity.
- Keep interoperability open so future workload types can run beyond initial agent scenarios.
- Prioritize practical utility over hype; establish trust through reliability, isolation, and predictable behavior.

## Open questions that still need explicit decisions

1. Hive-level coordinator naming and exact responsibilities relative to honeycomb-level coordinator.
2. Network model choice:
- Central relay only, managed overlay mesh, or hybrid.
3. Agent message protocol shape:
- Minimal custom protocol vs adopting/adapting a larger standard.
4. Execution model beyond fork-join DAGs:
- Consensus, streaming pipelines, actor/event patterns, or mixed model.
5. Multi-tenancy hardening path for enterprise:
- Isolation level tiers, compliance targets, audit design, and SLO definitions.
6. Economic model details:
- Pricing for contributed compute, quality scoring, fraud resistance, and settlement logic.

## Recommended usage

When starting a new AI-driven implementation cycle:
1. Load this document first as intent context.
2. Load canonical architecture/spec docs second.
3. Treat conflicts in favor of canonical architecture/spec docs.

## Source note

This file was created from a founder strategy conversation thread and condensed into durable context to avoid re-deriving the same direction repeatedly.

---

## Added Context: Control Plane + Distributed-First Dogfooding

This section captures a later conversation that clarified execution strategy.

### Core framing

- The platform has two planes:
- `Control Plane` (Honeycomb): prompt intake, planning orchestration, node registry, scheduling, lifecycle.
- `Data Plane` (Hive Runtime / Wax execution path): agent execution, tool calls, memory handling, LLM adapter invocation.

### Immediate build objective (solo-founder)

- Prioritize a narrow distributed MVP that uses existing hardware now.
- Main value proposition for early users: parallel agent execution across heterogeneous nodes.
- Start centralized (single Honeycomb), not federated/mesh.

### Minimal distributed MVP shape (v0)

1. `hive-node` daemon on each machine:
- Registers capabilities (CPU/RAM/LLM profiles/etc).
- Accepts assigned tasks.
- Executes task via configured LLM provider.
- Streams logs/results.
2. `Honeycomb` control service:
- Node registry.
- Task queue.
- Basic scheduler (round-robin/load-aware with per-node concurrency limits).
3. Task contract:
- Machine-readable JSON input/output.
- Structured planner output (task graph JSON), never free-text plan.
4. Planner behavior:
- Queen/planner is treated as a normal schedulable task type, not a privileged runtime primitive.

### Defer to later phases

- OCI packaging and marketplace mechanics.
- Full WASM-first enforcement on every path.
- Mobile/edge complexity beyond basic node participation.
- Federation, multi-queen election, and peer discovery.

### Why this was chosen

- Fastest path to dogfooding and compounding velocity.
- Lets agents help build the platform while infrastructure is already being utilized.
- Creates an immediately sellable technical narrative: distributed agent swarm over idle compute.

### Recommended first implementation order

1. Node registration + heartbeat + capability schema.
2. Task queue + assignment API + worker execution loop.
3. LLM profile abstraction and provider routing (`code-fast`, `reasoning-high`, etc.).
4. Planner task returning validated task-graph JSON.
5. Parallel worker execution + retry + observability baselines.
