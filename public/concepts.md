# Core Concepts

## Comb
A **comb** is a node that can execute work. In practice, a comb is a device or container that connects to Honeycomb, reports capabilities, and receives tasks.

## Stinger
The **Stinger SDK** is the client used by combs. It registers a comb and sends heartbeat reports containing CPU, memory, power, and network stats.

## Honeycomb
**Honeycomb** is the control plane microservice. It exposes REST/gRPC APIs, stores combs and pending tasks, and publishes tasks via NATS.

## Wax
**Wax** is the WASM runtime that executes sandboxed modules. It is under active development and will be embedded by Honeybee.

## Beekeeper
**Beekeeper** is the control-plane UI that visualizes comb status and the task queue.

## Honeybee
**Honeybee** is the cross-platform UI shell that will host Wax and orchestrate agent workflows.
