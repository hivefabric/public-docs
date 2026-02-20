# Next Steps Plan (Internal)

**Plan Date:** 2026-02-19

This plan is execution-oriented and aligned with current repository state.

## Stage 1: Task Execution Maturity

- Lock lifecycle transitions to canonical states only.
- Ensure scheduler selects only `Queued` tasks.
- Add/finish tests for retries, timeout transitions, and completion handling.
- Verify logs always capture `context`, `input`, and `output` payloads.
- Validate queue-time and execution-time metrics on every terminal state.

## Stage 2: Node/Scheduler Robustness

- Validate lease expiry cleanup under heartbeat loss.
- Confirm node filtering by IAM user/role works at repository layer.
- Harden scheduling placement filters (labels, resources, ownership, roles).
- Add churn tests: node joins/leaves while queue remains active.

## Stage 3: Honeycomb Product Path

- Stabilize backend + UI runbooks for local UAT and dockerized flows.
- Improve operator UX for task streaming, failure reasons, and retry visibility.
- Keep embedded-node controls reliable and role-aware.
- Complete Telegram flow validation for admin/user routing.

## Stage 4: Apiary Marketplace Path

- Resolve catalog fetch failure paths with stronger UI/service diagnostics.
- Keep agent definitions declarative (`agent.yaml`) and external to compiled service logic.
- Harden OCI packaging/push/index flow and improve error surfaces.
- Prepare signature verification integration path (cosign-compatible).

## Stage 5: Autonomy Loop Progression

- Move PDCA loop from scaffold to measurable actions.
- Track proposal outcomes against task success rate and utilization deltas.
- Enforce strict IAM scope for all loop-spawned actions and generated agents.

## Delivery Cadence

- Weekly: reliability and regression pass (task lifecycle + node churn).
- Bi-weekly: UAT walkthrough (control-plane, Honeycomb, Apiary, comb nodes).
- Monthly: architecture checkpoint against IAM/scheduler/module-boundary constraints.
