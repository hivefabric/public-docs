# Cost Strategy & Financial Basis

HiveFabric is intentionally designed to be the **cheapest possible distributed AI platform** without sacrificing required performance. This document lays out the financial philosophy, instrumentation, and decision points.

## 1. Cost Philosophy

* **Open-source first:** Prefer open-source runtimes (Wasmtime, Ollama, NATS, PostgreSQL, ClickHouse) and infrastructure so the platform is not dependent on proprietary vendors.
* **Local compute, cloud fallback:** Executors leverage user-owned hardware for most work. Cloud credits only kick in when no local device meets the requirements and the cost has been approved in the budget.
* **Telemetry-informed economics:** The Telemetry Steward tracks cost per execution (including power, bandwidth, cloud credits) and compares it to the value delivered (e.g., agent outcomes, marketplace revenue). When cloud fallback starts dominating, the steward raises an alert immediately.

## 2. Financial Controls

* **Budget Thresholds:** Humans define budget ceilings per quarter. Any change (e.g., supporting a new GPU, inviting a commercial API) that could push usage beyond 75% of the budget must pause for approval.
* **Cost Trade-offs:** When performance improvements require cost increases (e.g., new hardware support, paid cloud model), AI agents prepare a decision brief summarizing cost delta, impact, and alternatives. The brief routes to human legislators before the gitflow merge proceeds.
* **Cost Metrics to Monitor:** Cost per scheduled task, cloud credit spend per user, local vs. cloud execution ratio, and marketplace revenue per compute cycle.

## 3. Execution Discipline

* **Telemetry Automation:** Runs compute cost attribution per executor (device power profile, local LLM footprint) and surfaces deviations beyond acceptable variance (default ±10%) for review.
* **Open-source Procurement:** Preference for community-maintained WASM runtimes, open telemetry tools, and container registries. When a proprietary solution is considered for clear benefit, a comparison table is produced and approved.
* **Human Consultation Required:** No AI may adopt a new paid runtime, commit to a new cloud contract, or disable an open-source component without explicit legislative approval. This maintains direct human control over major financial commitments.
