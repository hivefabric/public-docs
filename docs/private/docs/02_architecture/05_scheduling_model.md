# Scheduling Model

The HiveFabric Scheduler is the intelligent core of the Control Plane. Its primary responsibility is to assign agent tasks to the most appropriate executor in the fabric, balancing a complex set of requirements and constraints.

## 1. Scheduling Philosophy

The scheduler is not a simple first-in, first-out queue. It is a sophisticated decision engine that aims to optimize for cost, performance, and user preferences simultaneously. Every execution on the fabric is a direct result of a scheduling decision.

## 2. Scheduling Dimensions

The scheduler evaluates multiple dimensions when placing a workload:

*   **Device Capability:** Does the executor have the required hardware (e.g., sufficient RAM, a required GPU)?
*   **LLM Availability:** Does the executor have the specific local model required by the agent (e.g., `qwen:7b-chat-v1.5-q4_K_M`)? This is a critical feature for the LLM routing strategy.
*   **Cost:** The scheduler heavily prioritizes local execution on a user's own devices, as this has a near-zero marginal cost. Cloud resources are treated as an expensive fallback.
*   **Latency & Geography:** For tasks that require low latency, the scheduler can place agents on executors that are geographically close to the user or the target data source.
*   **Trust & Ownership:** Privacy-sensitive tasks can be "pinned" to run only on devices owned by the user, ensuring data never leaves their personal hardware.
*   **Power State:** The scheduler is aware of device battery levels and power status. It can be configured to schedule heavy or long-running tasks only when the device is charging.

## 3. Fork-Join Execution (DAGs)

The scheduler has native support for Directed Acyclic Graphs (DAGs) of execution. This means a complex workflow can be defined as a series of dependent tasks. The scheduler can run independent tasks in parallel across different executors and then "join" the results for a final step, enabling powerful, distributed computation.
