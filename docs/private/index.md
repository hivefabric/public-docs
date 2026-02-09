# HiveFabric Documentation Repository

> **Purpose**: This repository is the single source of truth for HiveFabric. It is a living document designed to be used as a long-term architectural and product vision, a context repository for AI-driven development, and a north-star reference for all contributors.

# Vision & Philosophy

## What is HiveFabric?

**HiveFabric** is a distributed, local-first platform for running and scheduling autonomous AI agents across a global pool of user-owned devices (phones, laptops, desktops, servers), with optional cloud coordination.

**The One-Liner:**

> *Kubernetes + BOINC + Ollama — for autonomous AI agents.*

HiveFabric allows anyone to run AI agents continuously, schedule them anywhere in a shared “personal cloud,” prefer local execution with local LLMs, and fall back to cloud APIs only when necessary. It is an operating system for distributed, evolving autonomous agents.

## Core Philosophy: Emergent Intelligence

HiveFabric does not encode intelligence directly. It creates the conditions where intelligence emerges from constraints, pressure, and reuse. The system becomes smart over time, even if individual agents are not.

* **Pain-Driven Evolution:** Capabilities are not created because they *might* be useful. They are crystallized only when an agent fails repeatedly and a proposed solution proves reusable and survives real-world usage. Everything in HiveFabric exists because something hurt before.
* **The Evolution Loop:** The core loop of the system is `Objective → Execution → Failure → Analysis → Proposal → Sandbox → Promotion → Reuse`. Failure is not an error; it is data that drives the system's evolution.

## Guiding Principles

1. **Local-First, Cloud-Coordinated:** Agents run on user hardware by default. The cloud is for coordination, not primary execution.
2. **Users Own the Compute:** HiveFabric turns personal hardware into a personal and shared AI cloud, giving users ownership over their data and computation.
3. **WASM for Security and Portability:** All agents run as sandboxed WASM modules, ensuring they are portable, secure, and have a low footprint.
4. **Scheduling is as Important as Execution:** The platform's core is its ability to intelligently schedule agents across a heterogeneous network of devices.
5. **Zero Marginal Cost for Most Workloads:** By leveraging idle local resources, the cost of running most AI agent workloads trends toward zero.
6. **Open Core, Extensible Ecosystem:** The core platform is open, with value accruing in the ecosystem of agents, skills, and tools.

## The Problem It Solves

* **Cloud AI is Expensive & Centralized:** Today's powerful AI is locked in data centers, creating high costs and vendor lock-in.
* **Local LLMs are Underutilized:** Powerful local models on desktops and phones are mostly idle.
* **Agent Frameworks are Not Platforms:** Most agent frameworks are libraries that lack a runtime, scheduler, and operational tooling.
* **There is no "Scheduler for AI Agents":** No system exists to manage and schedule AI workloads across a distributed, heterogeneous network of personal devices.

---

# System Architecture

## High-Level Overview

HiveFabric consists of a central **Control Plane** that schedules tasks and a distributed network of **Executor Runtimes** that execute them. Executors, running on user devices, report their capabilities and availability, and the Control Plane assigns work based on a sophisticated scheduling model.

```
            +------------------+
            |  Clients / UIs   |
            | (Web, CLI, Mobile) |
            +--------+---------+         
                     |
                     v
        +--------------------------+
        |  HiveFabric Control Plane|
        |      (Kubernetes)        |
        |--------------------------|
        | - API Server & Auth      |
        | - Scheduler              |
        | - Agent & Executor Registry |
        | - LLM Router             |
        | - State Store (Postgres) |
        | - Task Queue (NATS)      |
        +--------------------------+
          /          |           \
         /           |            \
        v            v             v
+-------------+ +-------------+ +-------------+
| Executor    | | Executor    | | Executor    |
| (Laptop)    | | (Phone)     | | (Server)    |
|-------------| |-------------| |-------------|
| - WASM      | | - WASM      | | - WASM      |
|   Runtime   | |   Runtime   | |   Runtime   |
| - Capability| | - Capability| | - Capability|
|   Reporter  | |   Reporter  | |   Reporter  |
+-------------+ +-------------+ +-------------+
```

## The Control Plane ("Honeycomb")

The Control Plane is a cloud-hosted, Kubernetes-native application responsible for being the brain of the entire fabric.

* **Responsibilities:**
  * Authentication & Identity
  * Agent scheduling and placement logic
  * Registry and health tracking of all connected Executors
  * Agent registry and marketplace access
  * LLM routing decisions (local-first, cloud-fallback)
  * Auditing, logging, and task history
* **Core Infrastructure Services:**
  * **Kubernetes:** The foundation for deploying and managing control plane services
  * **API Gateway:** Handles gRPC and REST API traffic from clients and executors
  * **NATS JetStream:** A persistent, high-performance task queue for scheduling
  * **PostgreSQL:** The primary state store for users, agents, tasks, and history
  * **Redis:** Used for caching, presence information, and fast coordination
  * **MinIO (or other S3-compatible):** Stores agent artifacts (WASM bundles) and logs

## The Executor Runtime

The Executor is a lightweight, cross-platform runtime installed on user devices that turns them into nodes in the HiveFabric network.

* **Supported Platforms:** Android, Linux, macOS, Windows (iOS planned)
* **Responsibilities:**
  * Registers the device with the Control Plane and advertises its capabilities
  * Pulls scheduled tasks from the NATS queue
  * Executes agents securely within a **WASM sandbox**
  * Enforces resource limits (CPU, RAM, battery, thermal)
  * Reports health, logs, and results back to the Control Plane
* **Capabilities Reported:** CPU/RAM/GPU, available local LLMs (via Ollama), battery/power state, and network conditions

## Node Capability & Geolocation Model

The Control Plane maintains a detailed model of each node's capabilities to make intelligent scheduling decisions. For observability, the system uses IP-based geolocation to infer a node's approximate location. This data is used to render a global map visualization, providing insight into the fabric's distribution without compromising user privacy with precise GPS data.

---

# Agent & Scheduling Model

## The Agent Model: Portable & Secure

* **Agents are WASM Modules:** Agents are compiled to WebAssembly (WASM) for ultimate portability and security. They are built once and can run on any device with an Executor.
* **OCI Artifacts:** Agents are packaged and distributed as OCI artifacts (but are not Docker containers). This allows leveraging existing registry infrastructure like Docker Hub or GHCR for storage, versioning, and signing (via `cosign`).
* **Agent Manifest:** Each agent bundle includes a `manifest.yaml` that declares metadata, version, resource requirements, and security permissions.
* **Strict Sandboxing:** Agents execute in a sandbox with no default access to the host filesystem, network, or OS. All permissions must be explicitly granted by the user and enforced by the Executor.

## Agent Roles & Patterns

Agents are semi-autonomous; they follow rules, report state, and react to events but do not have independent, open-ended intent. They are specialized for roles such as:

* Monitoring & Observability
* Scheduling & Optimization
* Event-Driven Automation
* Data Processing
* Local LLM Workloads

## The Scheduling Model: Intelligent Placement

The HiveFabric scheduler is the core of the platform's intelligence. It assigns tasks to Executors based on a multi-dimensional analysis.

* **Scheduling Dimensions:** Device capability, LLM availability, cost, latency & geography, trust & ownership, power state
* **Fork-Join Execution:** The scheduler can break a complex workflow (DAG) into multiple tasks and run them on different executors in parallel.

## LLM Strategy: Local-First Routing

HiveFabric's LLM router follows a waterfall model designed to prioritize privacy and low cost:

1. **Try Local LLM:** Attempt to use a locally available model via Ollama first.
2. **Try Shared Device Pool:** If no local LLM fits, try to find another available device in the user's personal pool that has the required model.
3. **Fallback to Cloud API:** As a last resort, and only with explicit user permission and budget controls, use a commercial API (OpenAI, Anthropic, Google).

---

# Ecosystem & Strategy

## Marketplace Vision

The Agent Marketplace is envisioned as the **"GitHub + App Store for AI agents."** It is not just a store but a "memory of what worked."

* Agents are discoverable, rated, reviewed, versioned, and signed.
* Developers can publish free or paid agents.
* The platform takes a commission on sales, creating a revenue-sharing model that incentivizes a high-quality ecosystem.

## Risks & Mitigation

* **Incentive to Contribute (Primary Risk):** Users won't share compute without a reason.
  * **Mitigation:** The product strategy is **outcome-first**. Users install HiveFabric for direct personal benefit from a "killer agent." Compute sharing is an optional, secondary feature.
* **Scheduler Complexity:**
  * **Mitigation:** The v1 scheduler must be simple and explainable. Complexity will be added incrementally.
* **Trust & Security:** A single malicious agent could destroy trust.
  * **Mitigation:** A multi-layer trust architecture is non-negotiable, including cryptographic signing, strict sandboxing, explicit permissions, and a global kill switch.

## Business Model

HiveFabric follows a freemium and open-core model.

* **Users (Freemium):**
  * **Free Tier:** Run local agents using local devices and local LLMs at near-zero cost.
  * **Pro Tier (Subscription):** Pay for convenience, priority scheduling, cloud credits, and access to premium marketplace agents.
* **Enterprises (Contracts):**
  * Self-hosted control planes, private agent registries, and compliance/audit features.
* **Revenue Sources:** Subscriptions, marketplace commissions, and enterprise contracts.

## The Human Role: Legislators, Not Operators

Humans do not micromanage agents. They act as legislators for the system by:

* Defining high-level objectives
* Approving new security permission classes
* Tuning global constraints (e.g., budgets)
* Deciding the overall direction of their personal Hive

---

# Naming & Terminology

## Official Naming

* **Long / Story Name:** `HiveFabric` (Used for official branding and narrative)
* **Short / Operational Name:** `bHive` or `h1v3` (Used for CLI, repos, and shorthand)

## Internal Metaphors

To maintain conceptual integrity, the following hive-themed metaphors are used internally. APIs and user-facing documentation remain neutral and professional.

| Concept | Hive-Themed Name | Description |
|---|---|---|
| Control Plane | Honeycomb | The central brain and coordination service. |
| Executor Node | Bee / Worker | A device contributing resources to the fabric. |
| A Group of Nodes | Hive / Comb | A logical cluster of executors. |
| Agent Workload | Agent | An individual task or process running in the fabric. |
| Task Scheduler | Queen Bee | The core scheduling component in Honeycomb. |
| Task Queue | Nectar Flow | The flow of tasks from the scheduler to executors. |
| Storage Layer | Honey Store | Persistent storage for artifacts and state. |
| Observability | Scout Bees | Agents responsible for monitoring and reporting. |

---

# LLM-Driven Development

## Overview

HiveFabric is built using a methodology of **LLM-Driven Development**. This README acts as the master prompt and single source of truth for a team of specialized AI "personas" or agents. The goal is to leverage LLMs to accelerate development, maintain architectural consistency, and automate tasks.

## Core LLM Personas

* **Chief Architect AI:** Guardian of the vision in this document. Reviews major changes for architectural alignment and makes key technical decisions.
* **Control Plane AI (Rust Specialist):** Implements the "Honeycomb" control plane in Rust, integrating with Kubernetes, NATS, and Postgres.
* **Executor AI (Rust/WASM Specialist):** Builds the cross-platform Executor Runtime in Rust, focusing on the WASM sandbox and host interactions.
* **Frontend AI (React Specialist):** Develops all user-facing components, including the dashboard and marketplace.
* **DevOps AI (K8s/CI-CD Specialist):** Manages all infrastructure, deployment pipelines, and release engineering.
* **Security AI:** Audits the entire system for vulnerabilities, with a special focus on the WASM sandbox and inter-agent communication.
* **Product Owner AI:** Acts as the voice of the user, ensuring the project builds useful, desirable features and prioritizes work based on impact.

## Development Workflow

1. **Task Generation:** The **Chief Architect AI** breaks down features described in this document into actionable tasks, assigning each to the relevant specialist AI.
2. **Implementation:** The specialist AI takes the task and its context (a section of this document) and generates the required code, tests, or configuration.
3. **Review:** Code is reviewed by other AIs and human supervisors. The **Security AI** audits for vulnerabilities, and the **Chief Architect AI** confirms architectural alignment.
4. **Integration:** The **DevOps AI** integrates the new code into the main branch and deploys it through the CI/CD pipeline.
5. **Iteration:** The **Product Owner AI** reviews the result from a user perspective, providing feedback for the next iteration.

---

# Repository Structure

* `docs/` – Living documentation categorized by domain:
  * `00_vision_and_strategy/` – Mission, manifesto, philosophy, governance, immutable rules, naming, and meta-parameters.
  * `01_product/` – Product context, marketplace vision, gap analysis, and roadmap.
  * `02_architecture/` – System overview, control plane, executor, agent model, scheduling, LLM strategy, and operational autonomy.
  * `03_engineering/` – Engineering playbook, project build guide, MCP servers, technical catalog, and autonomous control procedures.
  * `04_finance/` – Cost strategy, budget discipline, and financial decision controls.
  * `01_product/05_diagrams/` – Mermaid diagrams capturing system flow and agent lifecycle for quick visualization.
  * `01_product/06_explainers/` – Audience-specific explainers (beginner, technologist, AI expert) for communication.
* `llm_personas/` – Definitions of each autonomous AI persona driving the project.

# Usage

1. **Humans** define objectives, budgets, and approvals (Immutable Rules).
2. **AI personas** consult this repo, create gitflow branches, execute tasks, and document updates.
3. **Telemetry/QA agents** monitor metrics, feed back success/failure, and trigger tickets when thresholds are violated.
4. **Humans** review key decisions, especially costs, permissions, and architectural changes, before merging into `main`.

# Quick Links

* `docs/00_vision_and_strategy/meta_parameters.yaml` – Dynamic compute and budget controls.
* `docs/03_engineering/04_technical_catalog/repo_map.md` – Cross-repo coordination guide for active modules.
* `docs/03_engineering/05_process_steps.md` – Engineering process steps and execution guidance.
