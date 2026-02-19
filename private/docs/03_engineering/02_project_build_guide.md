# Step-by-Step Project Build Guide

This step-by-step guide is intended to be followed by the AI workforce (Chief Architect, Executor, Control Plane, DevOps, Security, Product Owner, etc.) with humans providing strategic inputs at the checkpoints described.

1. **Define Strategic Objectives**
   * Review `docs/00_vision_and_strategy/01_mission_and_vision.md` and `03_business_model.md` to ensure alignment.
   * Human legislators specify the current quarter's OKRs, budget headroom, and immutable constraints (new permissions, cost thresholds).
   * Telemetry Steward subscribes to these objectives to detect drift.

2. **Translate Objectives into Backlog & Tasks**
   * Chief Architect AI breaks objectives into epics and technical tasks, referencing the System Architecture, Agent Model, Scheduling Model, and Operational Autonomy documents.
   * Assign each task to the appropriate specialized persona. Ensure offers (agents) have acceptance criteria, tests, and telemetry hooks defined in the context repository.
   * Populated tasks trigger creation of `feature/` or `bugfix/` gitflow branches; Task Guardian ensures ownership.

3. **Execute & Validate Locally**
   * Executors run tasks within secure WASM sandboxes, invoking the `QA Conductor` to run unit/integration/fuzz suites before pushing branches.
   * Telemetry Steward collects runtime metrics (scheduler latency, LLM hit rate, resource usage) and compares them against thresholds.
   * Failures generate tickets and block merges until cleared by QA agents and human designers if immutable rules might be impacted.

4. **Review & Security Audit**
   * Security AI conducts static analysis, dependency scanning, manifest inspection, and sandbox penetration tests.
   * QA Conductor ensures regression suites pass across target platforms. Execution Validators confirm parity in WASM results per platform.
   * These reviews generate artifacts referenced in PR descriptions.

5. **Merge & Deploy via Gitflow**
   * Task Guardian and DevOps AI coordinate automated CI/CD pipelines (NATS, Kubernetes deployment, CLI release). Branch-specific steps include:
     * `feature/` merges after automated checks and a human legislator review.
     * `release/` branches receive smoke tests, telemetry validation, business metric review, and then human sign-off before merging to `main` and tagging.
     * `hotfix/` branches can be created in emergencies but wait for human legislator approval before deployment.
   * The Unified Documentation updates whenever architecture, product, or engineering changes are made; Context Curator triggers doc updates automatically.

6. **Monitor & Iterate**
   * Post-deployment, QA Conductor, Telemetry Steward, and Marketplace agents continue observing metrics.
   * If success metrics (scheduler latency, marketplace revenue, QA coverage) fall out of band, new tickets are generated with documented rationale.
   * Autonomous control tries remediation (e.g., auto-revert, reroute tasks), but any impactful change (cost, performance, permissions) pauses for human review.

7. **Document & Communicate**
   * Ensure every change has an associated entry in the Unified Context (e.g., new doc under architecture or product) so future AI tasks have fresh context.
   * Summaries go to legislators with key findings, metrics, and decision forks requiring input.
