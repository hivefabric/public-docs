# The Control Plane ("Honeycomb")

The Control Plane is the centralized brain of the HiveFabric system. It is designed as a cloud-hosted, Kubernetes-native application responsible for all coordination, scheduling, and management tasks.

## 1. Core Responsibilities

The Control Plane's primary job is to manage the fabric without executing any agent workloads itself. Its responsibilities include:

*   **Authentication & Identity:** Manages user and executor identities and secures API access.
*   **Agent Scheduling & Placement:** Contains the core scheduler logic that decides which agent runs on which executor.
*   **Executor Registry:** Maintains a real-time list of all connected executors, their health status, and their reported capabilities.
*   **Agent Registry & Marketplace:** Provides access to agent metadata for the scheduler and users.
*   **LLM Routing:** Implements the local-first logic for routing LLM requests.
*   **Auditing & History:** Keeps a persistent log of all tasks, their status, and their results for user review.

## 2. Core Infrastructure Services

The Control Plane is composed of several microservices and is built upon a foundation of robust, open-source infrastructure:

*   **Kubernetes:** The foundation for deploying, scaling, and managing the control plane services.
*   **API Gateway:** A central entry point (e.g., Traefik, NGINX Ingress) that handles gRPC and REST API traffic from clients and executors.
*   **NATS JetStream:** A persistent, high-performance messaging system used as the primary task queue for dispatching scheduled jobs to executors.
*   **PostgreSQL:** The primary relational database used as the state store for users, agents, tasks, and historical data.
*   **Redis:** An in-memory data store used for caching, real-time presence information (e.g., which executors are currently online), and other fast coordination tasks.
*   **MinIO (or other S3-compatible object storage):** Used to store large artifacts, primarily the signed WASM agent bundles and potentially extensive logs.
