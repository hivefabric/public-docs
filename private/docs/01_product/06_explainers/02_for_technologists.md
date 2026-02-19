# HiveFabric Explained for Technologists

HiveFabric is a distributed control plane built atop Kubernetes, NATS, and WASM, orchestrating autonomous agents across a mesh of user-owned executors. Clients (web, CLI, mobile) interact with the control plane API, which schedules tasks via a Queen Bee scheduler.

The scheduler is multi-dimensional: it understands hardware, LLM availability, latency, trust, and power state. Executors report capabilities (CPU, RAM, GPU, battery) and pull signed agent OCI artifacts for WASM execution. Observability is baked in via OpenTelemetry; telemetry stewards aggregate metrics for latency, failure rates, and business KPIs.

A meta-scheduler keeps QA, telemetry, and business personas synchronized, automatically generating gitflow branches, running CI/CD, and triaging issues. Humans retain final approval on immutable rules, billing, and significant infrastructure changes.
