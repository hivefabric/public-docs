# Vision Execution Backlog

This backlog translates the long-term Hive vision into concrete next tasks.

## Track A: Execution Reliability

1. Complete end-to-end fix for scheduled tasks that do not emit terminal stream events.
2. Enforce/validate terminal state transitions with regression tests under churn.
3. Add a dedicated `/api/tasks/{id}` endpoint for faster single-task polling.
4. Expand task-event contract to include explicit `running` heartbeat and terminal acknowledgements.

## Track B: Orchestration and DAG

1. Add explicit DAG dependency fields in workflow submit API.
2. Implement join-node aggregation semantics for fork-join workflows.
3. Add workflow-level query API (`/api/workflows/{id}`) with child-task states.
4. Add retry policies at workflow-step level.

## Track C: Honeycomb Product Completion

1. Finalize Honeycomb service Docker/compose defaults and avoid port conflicts with Apiary.
2. Add UI pages for loop experiments, promotion audit trail, and per-task logs.
3. Add Android packaging pipeline and smoke tests.
4. Harden Telegram route auth and operator tooling.

## Track D: Marketplace and Agent Trust

1. Finish APIary registry index against GHCR with role-aware visibility.
2. Add OCI signature verification on pull path.
3. Define promotion policy from sandbox-generated agents to production catalog.
4. Add provenance metadata (generated-by loop, rationale, metrics links).

## Track E: IAM and Multi-Tenancy

1. Add end-to-end tests for user-scoped scheduling across mixed node ownership.
2. Add explicit forbidden tests for system-level operations from Worker scope.
3. Add audit-event trail for all privileged actions (prompt submit, experiment promote, workflow submit).

## Track F: CI/CD and Release

1. Ensure every repo has CI + security + release workflows and status dashboards.
2. Add integration job that runs `hive-dogfood stabilize` against ephemeral stack.
3. Gate GHCR publish jobs on stabilization/integration checks.
4. Add artifact verification jobs: pull image, run health probe, run sample task.
