# Technical Catalog

This folder is the single place to find **all technical modules and repos** that make up HiveFabric. Each entry provides a short description and the primary reference location.

## Core Runtime + Control Plane

### Hive (Rust workspace)

**Path:** `hive/`

**What it is:** The core Rust workspace that contains the control plane, runtime, and SDK.

**Modules:**
- **Honeycomb** (control plane service): `hive/crates/ms-honeycomb/`
- **Stinger** (SDK/client): `hive/crates/sdk-stinger/`
- **Wax** (runtime): `hive/crates/runtime-wax/`

**Primary docs:** `hive/README.md`

**Technical features:** `docs/03_engineering/04_technical_catalog/honeycomb_features.md`

---

## User Interfaces

### Beekeeper UI

**Path:** `ui-beekeeper/`

**What it is:** React UI for Honeycomb status and dashboards.

**Primary docs:** `ui-beekeeper/README.md`

### Honeybee UI (Web)

**Path:** `ui-honeybee/`

**What it is:** Early web UI shell intended to integrate Stinger + Wax in a unified console.

**Primary docs:** `ui-honeybee/README.md`

---

## Public Web

### Website

**Path:** `hivefabric.github.io/`

**What it is:** Public website (marketing / docs landing).

**Primary docs:** `hivefabric.github.io/README.md`

---

## Documentation

### Unified Docs (Private Section)

**Path:** `public-docs/docs/private/`

**What it is:** Source of truth for architecture, product, and engineering decisions for AI/human operators.

**Primary docs:** `public-docs/docs/private/index.md`

---

## Cross-Repo Map

See `docs/03_engineering/04_technical_catalog/repo_map.md` for cross-repo coordination and external dependencies.

---

## Notes

- Each module above has its own README and local documentation. This catalog should only point to those sources and briefly summarize purpose.
- If a new repo/module is created, it must be added here.
