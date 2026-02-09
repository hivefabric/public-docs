# Agent Model

The HiveFabric Agent Model is designed for security, portability, and verifiability. Agents are not arbitrary code but well-defined, sandboxed modules.

## 1. Agents are WASM Modules

The core of the agent model is **WebAssembly (WASM)**. All agent logic is compiled into a WASM binary.

*   **Portability:** This allows a single agent artifact to be built once and run on any supported architecture and operating system where the Executor Runtime is present.
*   **Security:** WASM provides a memory-safe, capability-based security model by default. The sandbox isolates the agent from the host system, which is a cornerstone of the platform's trust model.

## 2. OCI Artifacts for Distribution

Agents are packaged and distributed as **OCI (Open Container Initiative) artifacts**. It is critical to note that these are **not Docker containers**. HiveFabric uses the OCI specification as a universal, content-addressed format for agent distribution.

This approach allows HiveFabric to leverage the vast, existing ecosystem of container registries, such as:
*   Docker Hub
*   GitHub Container Registry (GHCR)
*   Amazon Elastic Container Registry (ECR)

Benefits include existing tooling for versioning, immutability, and content-addressable storage.

## 3. Agent Manifest & Signing

Each agent bundle is composed of the WASM binary and a `manifest.yaml` file. This manifest declares critical metadata, including:
*   Agent name, author, and version.
*   Resource requirements (e.g., minimum RAM).
*   **Permissions:** A list of capabilities the agent requires, such as network access to specific domains. These permissions must be explicitly approved by the user.

For security, every agent bundle must be cryptographically signed (e.g., using `cosign`). The Executor will refuse to run any agent with an invalid or untrusted signature.
