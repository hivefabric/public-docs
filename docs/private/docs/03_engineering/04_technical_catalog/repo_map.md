# Repository Organization & Cross-Repo Context

This reference tells AI and human contributors where to find the primary documentation, code, and supporting projects so the agents can coordinate work across multiple repositories.

## 1. This Repository (public-docs)

* `README.md` – public documentation overview.
* `docs/` – public docs plus the `/private/` section for internal docs.

## 2. Active Repositories (Current)

| Repo Name | Purpose | Location/URL | Notes |
|---|---|---|---|
| hive | Core Rust workspace (Honeycomb, Stinger, Wax) | https://github.com/hivefabric/hive | Control plane + runtime + SDK |
| ui-beekeeper | Honeycomb monitoring UI | https://github.com/hivefabric/ui-beekeeper | React UI |
| ui-honeybee | Honeybee web console | https://github.com/hivefabric/ui-honeybee | Early web shell |
| hivefabric.github.io | Public website | https://github.com/hivefabric/hivefabric.github.io | Marketing + landing |
| public-docs | Unified docs (public + private) | https://github.com/hivefabric/public-docs | Source of truth |

## 3. Coordination Tips

* Agents should reference this map before creating inter-repo PRs or scheduling cross-functional work. When a new repo spins up, add it to the table immediately.
* Keep track of repository ownership and responsibilities in this file so AI actors know when to escalate to the appropriate persona or human.
