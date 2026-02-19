# Executor Runtime (Bee + Wax)

The executor runtime turns a device into a comb worker for a honeycomb.

## 1. Runtime Components

- **Bee Agent**: node-side control agent responsible for registration, heartbeats, telemetry, assignment handling, and result reporting.
- **Wax Runtime**: WASM sandbox responsible for isolated cell execution.

## 2. Core Responsibilities

- Register comb identity with Honeybee.
- Send heartbeats and resource/capability reports.
- Receive cell assignments.
- Pull agent definition/artifacts and execute in Wax.
- Enforce local limits (CPU, memory, max cells, timeout).
- Return status, logs, and outputs.

## 3. Device and Network Constraints

The runtime is designed for unreliable edge conditions:

- Intermittent connectivity is expected.
- High latency and temporary disconnections are expected.
- Device state (battery, charging, thermal) affects scheduling eligibility.

## 4. Security Baseline

- API key auth and signed message validation.
- TLS transport for control communication.
- No direct comb-to-comb communication by default.
- Cell execution must occur inside Wax sandbox.

## 5. Platform Scope

Target platforms include Linux, macOS, Windows, and mobile-class devices where runtime constraints permit stable operation.
