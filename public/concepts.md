# Core Concepts

## Comb
A **comb-node** is a worker runtime that registers with control-plane, reports capabilities, and executes assigned tasks.

## Control Plane
The control-plane (`hive-control-plane/service`) owns node registry, task state transitions, scheduling decisions, and execution observability.

## Task Lifecycle
Tasks follow canonical state transitions in control-plane:
`Created -> Queued -> Scheduled -> Running -> Succeeded|Failed|TimedOut -> Retried|Cancelled`.

## Apiary
Apiary (`apiary-market`) stores declarative agent/skill definitions and OCI packaging/index metadata for marketplace flows.

## Honeycomb App
Honeycomb app (`honeycomb/service` + `honeycomb/ui`) is the user-facing layer for auth, dashboard, role-routed prompts, and embedded node controls.

## IAM Scoping
Identity and role checks are centralized in IAM: admin/platform operations route to Queen Bee, user operations route to Worker Bee with ownership boundaries.
