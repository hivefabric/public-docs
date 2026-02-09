# Operational Autonomy & Feedback Control

This architecture supplement focuses on the **execution context** that keeps HiveFabric evolving safely and reliably. It documents how the project **autonomously governs its own progress**, how QA and telemetry agents verify every change, and how the platform continually feeds business intelligence back into future development decisions.

## 1. Context as an Autonomous Project Controller

All AI personas operate under a shared context repository that is the single source of truth for objectives, constraints, and architectural guardrails. This document is part of that context, and it is leveraged by:

* **Chief Architect AI, Control Plane AI, Executor AI, DevOps AI, Security AI, Product Owner AI,** and additional oversight personas in `llm_personas/workers/`.
* **Execution Orchestrators:** lightweight “project agents” responsible for keeping the plan aligned with the documentation (e.g., `context-curator`, `task-guardian`, `gitflow-enforcer`).

These agents run autonomously on the fabric: they read the unified docs, translate updates into tasks, verify completion, and escalate only when human intervention is required. Context data includes telemetry, QA reports, and business signals so the project can alter priorities without a constant person in the loop. Human legislators retain final say by approving irreversible changes (see Immutable Rules) and by reviewing gitflow merges before the release branch is cut.

## 2. QA & Verification Agents

The fabric continuously validates itself through dedicated QA agents embedded in the Control Plane and Executor Runtime.

* **Execution Validators:** run regression and scenario-based suites whenever a manifest changes, ensuring scheduling, WASM sandboxes, and CI runners behave identically across platforms.
* **Observability Monitors:** synthetic agents run health checks (APIs, scheduler throughput, queue lag) and feed metrics back to the telemetry pipeline. Any deviation triggers a rollback or an investigation task.
* **Security Auditors:** specialized personas (Security AI + static scanners) inspect agent manifests, NATS stream policies, and control plane configs before a merge is tagged for production.
* **QA Feedback Loop:** Each QA pass emits structured reports that the Control Plane ingests, storing them alongside task histories. If a failure repeats, the system flags that pain point as the next required capability per the evolution loop.

## 3. Telemetry & Business Feedback Loop

Telemetry is architected as a closed-loop system that turns usage data into prioritization signals:

1. **Event Collection:** Executors and control plane services emit critical events (task lifecycle, scheduling decisions, local LLM hits/misses, billing triggers) into the global observability bus (NATS -> Loki/ClickHouse, tracing via OpenTelemetry).
2. **Aggregation & Analysis:** Telemetry AI (a persona that owns analytics) aggregates latency, cost, accuracy, and error KPIs. Results feed both the **business narrative** (market adoption, revenue per agent, churn) and the **engineering narrative** (failure rates, hot paths, node distribution).
3. **Decision Rules:** When business metrics (engagement, revenue per user, SSE) or operational metrics (scheduler latency, QA coverage) degrade beyond thresholds, the Control Plane automatically creates prioritized tickets. These tickets mention the impacted stakeholders (Product Owner AI, Chief Architect AI, Finance AI). The fabric can reroute compute to remediation tasks without waiting for human touch, but humans are notified before any irreversible scaling action is taken.

## 4. Business Signals and Product Evolution

Business personas constantly surface market data:

* **Marketplace Health:** Tracks agent downloads, ratings, revenue share, and optional compute-sharing incentives.
* **Usage Trends:** Identifies which LLM models and WASM agents are underutilized, enabling new investments.
* **Cost-to-Impact:** Finance AI measures the ROI of cloud fallback vs. local execution, allowing gating of premium agents and cloud credits.

These signals feed the roadmap via the same event bus that QA uses, ensuring the product evolves in lockstep with what actually matters to users.

## 5. Gitflow & Human-in-the-Loop Control

All work happens via **Gitflow branches** so every change is traceable and reviewable:

* `feature/` branches for experiments and new capabilities.
* `bugfix/` for critical fixes spotted by QA agents.
* `release/` branches for candidate releases after QA convergence.
* `hotfix/` for urgent remediation.

AI agents manage these branches by generating PRs and automated tests, but **humans (legislators)** approve merges into `main` or `release`. When an AI needs to deviate (e.g., to fix a security hole), it creates a `hotfix/` branch and waits for the legislator's merge approval. The human’s sign-off is also required for any change to the Immutable Rules, new billing models, or new permissions.

## 6. Control Feedback Orchestration

The Control Plane owns a meta-scheduler that keeps the QA, telemetry, and business agents working together. It listens for:

* **Pain Loops:** repeated failures in the same DAG that trigger a rewrite or new helper agent.
* **Improvements:** new metrics that exceed expectations, prompting the Promotion and Reuse stages of the Evolution Loop.
* **Telemetry Drift:** when data patterns shift (e.g., new hardware types, emergent GPUs), the Control Plane updates capability descriptors and scheduling heuristics.

These threads keep HiveFabric not only working but improving while respecting human governance.
