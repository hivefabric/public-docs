# Engineering Playbook

This playbook explains how HiveFabric’s AI workforce keeps the codebase, the architecture, and the business aligned. It is intentionally procedural so AI agents can follow it autonomously while humans remain the final decision makers.

## 1. Gitflow First

Every change happens inside a branch created from `main`:

* `feature/<short-purpose>` for new capabilities derived from the Product or Architecture backlog.
* `bugfix/<issue>` for regression hot spots discovered by QA or telemetry alerts.
* `release/<semver>` for candidate releases; merges into `main` only happen after QA, security, and business sign-off.
* `hotfix/<critical>` for urgent production fixes that bypass the regular release cadence but still require a legislator’s approval before deployment.

AI actors create PRs, run the prescribed CI/CD workflows, and report successes or failures back to the telemetry bus. Human legislators merge the PRs once they validate the tests, review the impact (code review notes, QA logs), and confirm budgetary/strategy alignment. This ensures the system always follows gitflow even while it self-heals.

## 1.1 Technical Catalog

All modules and repos are indexed in `docs/03_engineering/04_technical_catalog/README.md`. Add new projects there first, then link them from any other doc.

## 2. Autonomous Project Control Agents

AI personas form a self-governing layer:

* **Context Curator:** Keeps all docs (this playbook, architecture, vision) in sync, detecting duplicated or outdated information and flagging it back to the Chief Architect.
* **Task Guardian:** Watches scheduling queues, ensures that every agent task has ownership, automatically remediates failing tasks (retries, quarantines, rollbacks), and escalates to humans only when the Immutable Rules would be violated.
* **QA Conductor:** Runs integration suites, security scans, and randomized stress tests across WASM executors. Reports summary dashboards to both the Control Plane and the business telemetry loop.
* **Telemetry Steward:** Synthesizes health signals, business KPIs, and platform usage data to generate continuous improvement tickets.

Together, they ensure each commit, release, and runtime change is validated before it reaches the user or market.

## 3. Telemetry & Business Feedback

Telemetry is the nervous system that binds QA to product strategy:

1. **Observability Stack:** Logs, traces, and metrics flow through OpenTelemetry into Loki/ClickHouse and Grafana. Key signals include scheduling latency, local LLM success rates, and agent failure patterns.
2. **Marketplace Metrics:** Agent usage, ratings, downloads, churn, and revenue per agent are captured by Finance AI so we know which investments have traction.
3. **Evolution Signals:** Repeated pain points are automatically promoted into the Evolution Loop (`Objective → Execution → Failure → Analysis → Proposal → Sandbox → Promotion → Reuse`).

If telemetry shows a critical deviation (e.g., scheduler miss rate > 2% for 10 minutes or marketplace revenue drop > 8% QoQ), then the Control Plane creates a triage task. AI agents work it, but the final decision about scope, budget, or new permissions stays with human legislators.

## 4. Human Inputs & Control Gates

The AI workforce needs ongoing input to stay effective:

* **Objectives & Key Results:** Define quarterly goals, budgets, and acceptance criteria for new features (e.g., “Reduce cold-start time to 4s” or “Increase Pro subscriptions by 15%”).
* **Immutable Approval:** Any change that could violate the governing rules, increase cost beyond thresholds, or modify billing/permissions must be explicitly approved through the `Immutable Rules` checklist.
* **Telemetry Access:** Provide endpoints, credentials, or MCP server aliases (see question below) so telemetry agents can read raw data and write curated summaries.
* **Critical Decisions:** When the system surfaces multi-option trade-offs (e.g., use B2 vs. local GPU fallback), we describe the options and await your final selection before merging.

## 5. What the AI Team Needs from You

1. **Strategic Roadmap & Business Signal Thresholds:** Tell us the north-star metrics that matter most, which budget lines are fixed, and what risks you are willing to accept.
2. **Telemetry Destinations & MCP Servers:** Share the MCP (Model/Metadata Control Plane) server URIs, credentials, or resource names we should query through `list_mcp_resources`. If new MCP servers exist, please install them or provide access so AI agents can ingest the correct context.
3. **Human Approval Points:** Specify which types of changes (feature, release, permissions, cost increase) must pause for your explicit decision. We will not merge or deploy without that approval.
4. **Critical Platform Constraints:** Let us know if new hardware targets, compliance requirements, or deployment regions are coming so we can adjust the control plane and executor configurations.

With those inputs, the AI-managed workflows can run autonomously while you keep final control.
