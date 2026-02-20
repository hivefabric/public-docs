# Hive Platform Documentation

Public documentation for the current Hive stack: control-plane scheduling, node execution, marketplace APIs, and Honeycomb app integration.

## What works today

- `hive-control-plane` service for node registration, task lifecycle, scheduling, usage metrics, and task streams.
- `comb-node` execution nodes registering via IAM API keys and lease-based heartbeats.
- `hive-control-plane/ui` for node/task visibility.
- `apiary-market/service` + `apiary-market/ui` skill catalog prototype.
- `honeycomb/service` + `honeycomb/ui` app scaffold for login, messaging, embedded node controls, and Telegram bridge.

## Start here

- Getting started: `public/getting-started.md`
- Architecture overview: `public/architecture.md`
- API reference: `public/apis.md`
- Roadmap: `public/roadmap.md`

## Scope note

Public docs describe stable and testable contracts. Internal planning, detailed status, and architecture decisions are tracked in `docs/private/`.
