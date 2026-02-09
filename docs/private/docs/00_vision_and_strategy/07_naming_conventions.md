# Hive Naming Conventions

This document tracks the hive/bee metaphor across the product so naming stays consistent and fun. It is the canonical reference for component names, UI labels, and internal terminology.

## Core Product Names

| Concept | Hive-Themed Name | Notes |
|---|---|---|
| Control Plane | Honeycomb | Central coordination and scheduling brain. |
| Scheduler | Queen Bee | Assigns work across the hive. |
| Task Queue | Nectar Flow | Dispatch pipeline between control plane and executors. |
| Executor Node | Bee / Worker | A device contributing compute. |
| Executor Runtime | Wax | The software running on devices. |
| Agent Workload | Agent | Task or process. |
| Artifact Storage | Honey Store | Storage for WASM bundles and logs. |
| Observability | Scout Bees | Monitoring and health agents. |
| Capability Report | Forage Report | Device capability and status report. |
| Cluster of Nodes | Hive / Comb | Group of executors. |

## UI/UX Labels

Use these hive labels in the UI when appropriate, while keeping API names and documentation professional and unambiguous:

* Dashboard: "Hive Dashboard"
* Scheduler view: "Queen Bee" (explain in tooltip)
* Node list: "Worker Bees"
* Logs & metrics: "Scout Reports"

## Rules

1. Keep APIs and public documentation professional; include hive labels as friendly aliases.
2. When a new component is created, add its hive name here before shipping.
3. Avoid overloading names (each concept should map to a single hive label).

Update this file whenever a new service or UI component is introduced.
