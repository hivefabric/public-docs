# HiveFabric Global Agent Context

Purpose: This repo is a multi-project workspace (Rust control plane + runtimes + multiple UIs + docs). Use the closest `AGENTS.md` in the subtree for local rules; this root file provides global context and guardrails.

Core concepts
- Control Plane: Honeycomb (REST + gRPC + NATS task queue).
- Executors: Bee runtime (WASM) and agent model based on WASM + OCI artifacts.
- Clients/UIs: Honeybee (user console) and Beekeeper (control-plane dashboard).

Primary references
- `public-docs/docs/private/docs/02_architecture/01_system_overview.md`
- `public-docs/docs/private/docs/02_architecture/03_executor_runtime.md`
- `public-docs/docs/private/docs/02_architecture/04_agent_model.md`
- `public-docs/docs/private/docs/03_engineering/01_engineering_playbook.md`
- `public-docs/docs/private/docs/03_engineering/04_technical_catalog/repo_map.md`
- `hive-sdk/README.md` and `hive-sdk/docs/architecture.md`

Global rules
- Respect the architecture split: Honeycomb = control plane, Stinger = client SDK, Wax = runtime.
- Prefer repo-local conventions and existing patterns over inventing new ones.
- If a change affects multiple projects, summarize impact and list each project touched.
