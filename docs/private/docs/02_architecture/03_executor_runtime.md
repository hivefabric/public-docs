# The Executor Runtime ("Bee")

The Executor Runtime is a lightweight, cross-platform service that runs on a user's devices (laptops, desktops, servers, phones), turning them into worker nodes in the HiveFabric network.

## 1. Supported Platforms

The Executor is designed to be highly portable and will run on:

*   Linux
*   macOS
*   Windows
*   Android
*   iOS (Planned for a future release)

## 2. Core Responsibilities

The Executor's role is to securely run assigned tasks and communicate with the Control Plane. It does not make any decisions about what to run.

*   **Registration & Heartbeat:** On startup, it securely registers the device with the Control Plane and sends a periodic heartbeat to signal its availability.
*   **Capability Reporting:** It inspects the host device and reports its capabilities to the Control Plane. This includes:
    *   **Hardware:** CPU (architecture, cores), RAM, GPU (if available).
    *   **Software:** Operating System, available local LLMs (e.g., via an Ollama server).
    *   **State:** Current battery level, power status (charging/discharging), and network conditions (Wi-Fi/cellular).
*   **Task Execution:** It subscribes to a dedicated task queue in NATS. When a task is assigned to it, it pulls the corresponding agent bundle from object storage.
*   **Secure Sandboxing:** It executes the agent's logic inside a **secure WASM sandbox**, enforcing all resource limits (CPU, memory) and permissions (network access). This is the most critical security feature of the Executor.
*   **Reporting:** After execution, it reports the results, logs, and final status back to the Control Plane.
