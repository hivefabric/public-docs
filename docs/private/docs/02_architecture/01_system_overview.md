# System Architecture Overview

HiveFabric consists of a central **Control Plane** that schedules tasks and a distributed network of **Executor Runtimes** that execute them. Executors, running on user devices, report their capabilities and availability, and the Control Plane assigns work based on a sophisticated scheduling model.

## High-Level Diagram

```
            +------------------+
            |  Clients / UIs   |
            | (Web, CLI, Mobile) |
            +--------+---------+
                     |
                     v
        +--------------------------+
        |  HiveFabric Control Plane|
        |      (Kubernetes)        |
        |--------------------------|
        | - API Server & Auth      |
        | - Scheduler              |
        | - Agent & Executor Registry |
        | - LLM Router             |
        | - State Store (Postgres) |
        | - Task Queue (NATS)      |
        +--------------------------+
          /          |           \
         /           |            \
        v            v             v
+-------------+ +-------------+ +-------------+
| Executor    | | Executor    | | Executor    |
| (Laptop)    | | (Phone)     | | (Server)    |
|-------------| |-------------| |-------------|
| - WASM      | | - WASM      | | - WASM      |
|   Runtime   | |   Runtime   | |   Runtime   |
| - Capability| | - Capability| | - Capability|
|   Reporter  | |   Reporter  | |   Reporter  |
+-------------+ +-------------+ +-------------+
```

## Component Summary

*   **Clients (UIs):** User-facing applications (web dashboard, CLI, mobile app) that allow users to manage agents, view results, and configure their settings. They communicate with the Control Plane.

*   **HiveFabric Control Plane ("Honeycomb"):** The cloud-hosted, Kubernetes-native brain of the system. It is responsible for all coordination and scheduling but does not execute agent workloads itself.

*   **Executor Runtime ("Bee"):** A lightweight, cross-platform service that runs on user devices. It registers itself with the Control Plane, reports its capabilities, and executes the agent tasks it is assigned in a secure WASM sandbox.

```
