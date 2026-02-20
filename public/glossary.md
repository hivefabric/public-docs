# Glossary

- **Hive Control Plane**: Backend service for node registry, task lifecycle, scheduling, and metrics (`hive-control-plane/service`).
- **Comb Node**: Worker runtime that registers, heartbeats, executes tasks, and reports results (`comb-node`).
- **Apiary**: Marketplace/packaging layer for skill and agent metadata (`apiary-market`).
- **Honeycomb App**: User-facing app (backend + UI + embedded node controls) (`honeycomb/service`, `honeycomb/ui`).
- **Queen Bee**: Platform-scoped orchestration prompt/task path (admin/operator role).
- **Worker Bee**: User-scoped orchestration path restricted to owned nodes.
- **Heartbeat**: Periodic lease-renewal signal from a node to control-plane.
