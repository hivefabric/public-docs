# Technical Catalog

This folder is the single place to find technical modules and repos that make up HiveFabric.

## Core Platform Modules

### Hive Protocol (planned extraction)

**What it is:** canonical domain schemas and secure message envelope.

**Responsibilities:**

- Domain model contracts.
- Serialization and versioning.
- Signing/encryption helpers.

### Hive Queen (planned extraction)

**What it is:** hive-level coordinator.

**Responsibilities:**

- Hive/honeycomb registry.
- Cross-honeycomb allocation.
- Global policy enforcement.

### Honeycomb (local control plane)

**What it is:** honeycomb-level scheduler/orchestrator.

**Responsibilities:**

- Comb registry and health.
- Cell lifecycle.
- Local scheduling.

### Comb Node (planned extraction)

**What it is:** node agent runtime for each machine.

**Responsibilities:**

- Registration and heartbeat.
- Resource reporting.
- Cell execution.

### Wax Runtime

**What it is:** WASM execution and sandbox layer.

**Responsibilities:**

- Module lifecycle.
- Resource isolation/limits.
- Ephemeral execution boundary.

## Adjacent Product Modules

### Apiary

**What it is:** management and marketplace layer (outside core scheduling scope).

**Responsibilities:**

- Registry UX.
- Capability/agent visibility.
- Future economic and governance features.

## References

- Repo map: `private/docs/03_engineering/04_technical_catalog/repo_map.md`
- Canonical model: `private/docs/02_architecture/08_canonical_domain_and_repo_model.md`
