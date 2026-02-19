# Executors and Combs

A **comb** is a node capable of executing work. Today, combs primarily report their capabilities and heartbeats via Stinger. As Wax integration matures, combs will also execute WASM tasks.

## What combs report

- CPU, memory, storage, and network capacity
- Power and thermal state
- Availability metrics (uptime, utilization)
- Optional local models inventory

## Heartbeat behavior

- Stinger sends a heartbeat at a configured interval
- Honeycomb stores the latest report per comb
- Beekeeper visualizes the live status

## Security model (current)

- No public auth layer yet (local/dev focus)
- All requests are accepted if the payload is valid
- Production authentication/authorization is planned

For executor runtime details, see the Wax component page.
