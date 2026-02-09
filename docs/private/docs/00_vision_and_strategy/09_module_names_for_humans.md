# Module Naming Guide for Humans

This guide explains the narrative names we now use when humans talk about the HiveFabric control plane and its companion services. Using these names consistently keeps discussions aligned across product, architecture, and operations documents.

## Naming table

| HiveFabric Role | Story Name | What it Manages |
|-----------------|------------|-----------------|
| Control Plane | **Honeycomb** | Coordinates comb registration, trusted scheduling, and exposes APIs to clients/executors. |
| Agent Registry | **Apiary** | Stores agent manifests, versions, signatures, and marketplace metadata. |
| Runtime / Executor | **Wax** | Hosts WASP/WASM workloads on each node with sandboxing and resource controls. |
| Individual Node | **Comb** | Any registered executor (desktop, phone, server) that can process tasks. |

## Human usage notes

1. **Documentation:** Refer to these names when outlining architecture, deployment, or roadmap narratives. Use the technical role (control plane, registry, runtime) only when you need to clarify implementation details.
2. **Communication:** When briefing stakeholders, explain that Honeycomb represents the coordinating brain, Apiary stores reusable agents, Wax runs agents safely, and combs are the devices doing the work.
3. **Decision logs:** Flag HiveFabric decisions by these names to link the change to the intended component (e.g., “Honeycomb scheduler tuning”).

Keeping these names consistent helps humans reason about platform responsibilities without mixing metaphors.
