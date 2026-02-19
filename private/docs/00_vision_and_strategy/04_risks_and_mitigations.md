# Risks and Mitigations

This document outlines the primary existential risks to the HiveFabric project and the mitigation strategies designed into the platform's architecture and product strategy.

## 1. Incentive for Compute Contribution (Primary Risk)

*   **Risk:** Users are historically hesitant to donate compute resources on personal devices due to concerns about battery drain, performance impact, heat, and bandwidth costs. If HiveFabric is perceived primarily as a "distributed compute network," it will likely fail to gain traction.
*   **Mitigation:** The product strategy is **outcome-first, not compute-first**. Users are drawn to HiveFabric to run "killer agents" that provide direct personal benefit. Compute sharing is an optional, secondary feature that users can opt into, with clear controls and rewards. The initial value proposition must be for the user themselves.

## 2. Scheduler Complexity

*   **Risk:** The scheduler must handle a massively heterogeneous network of devices with varying capabilities, power states, and network conditions. This can lead to a complexity explosion, making placement decisions non-deterministic and impossible to debug.
*   **Mitigation:** The v1 scheduler must be **explainable in a single paragraph**. Complexity will be added incrementally and only as required. Observability and explainability of scheduling decisions are first-class priorities.

## 3. Trust and Security

*   **Risk:** A single malicious or significantly buggy agent that compromises user data or device security can destroy the project's reputation and kill adoption permanently.
*   **Mitigation:** A multi-layered trust and security architecture is non-negotiable from day one. This includes:
    *   **Cryptographically Signed Agents:** All agents must be signed to verify their origin.
    *   **Strict WASM Sandboxing:** Agents run in a tightly controlled environment with no default access to the host system.
    *   **Explicit, Auditable Permissions:** Users must explicitly grant any required capabilities (e.g., network access).
    *   **Global Kill Switch:** The ability for the control plane and users to immediately terminate misbehaving agents.
