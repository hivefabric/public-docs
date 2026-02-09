# Current Status

**Version/Date:** 2026-02-09

## What works now

- Honeycomb control plane runs via Docker and exposes REST.
- Stinger SDK can connect and report node properties (CPU/RAM/etc.).
- Beekeeper UI shows Honeycomb data when connected.

## What you can see in a demo

- Live combs registering + heartbeating.
- Honeycomb REST responses for combs/tasks.
- Beekeeper UI dashboards updating.

## Known limitations

- Honeybee UI install may require manual `npm install` depending on local registry/network.
- Full WASM execution pipeline is stubbed (runtime-wax has a simple host stub; Wasmtime runtime is optional).

## Primary user value today

- Real-time visibility into connected nodes (combs) and their capabilities.
- A working control plane + UI foundation for agent scheduling.

## Supported Features

### Supported

- Honeycomb control plane REST API
- Comb registration + heartbeat
- NATS-backed task queue (plumbed, not fully demoed)
- Beekeeper UI with live comb data

### Not yet supported / in progress

- Full WASM execution pipeline
- Task scheduling UI in Beekeeper
- Multi-tenant auth and permissions
- Production-grade persistence
