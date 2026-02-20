# Executors and Nodes

A **comb-node** is an executor capable of receiving scheduled tasks from the control-plane.

## What nodes report

- CPU cores and memory
- LLM profile hints
- Node labels and runtime flags (`docker`, `wasm`)
- Heartbeat timestamps and lease expiry status

## Heartbeat and lease behavior

- Node registers and receives lease duration.
- Node heartbeats renew lease.
- Control-plane removes expired/offline nodes from active scheduling pool.

## Security model (current)

- API key + role checks are enforced through IAM-compatible auth.
- User-scoped routes are restricted to owned nodes.
- Platform routes (for Queen Bee and related operations) require elevated roles.
