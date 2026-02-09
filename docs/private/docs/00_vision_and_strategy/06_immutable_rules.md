# Immutable Rules (The Constitution)

This document outlines the set of non-negotiable rules and constraints that define the "physics" of the HiveFabric system. These principles can only be changed with explicit, high-level approval from human legislators. They serve as the foundational constitution for all development.

## Core System Constraints

1.  **No Unbounded Execution:** Every agent task must have a defined, finite lifetime and resource limit (CPU, memory, time). There is no `while(true)`.
2.  **All Execution is Scheduled:** No agent or workload can run on an executor without being explicitly scheduled by the Control Plane. Local execution is a scheduling outcome, not an override.
3.  **Secure Sandbox by Default:** All agents must execute within a secure WASM sandbox. There is no option for privileged or non-sandboxed execution.
4.  **No Implicit Host Access:** Agents have no access to the host filesystem, network, or processes by default. Every capability must be explicitly declared in the agent's manifest and granted by the user at runtime.
5.  **All Agents Must Be Signed:** The system will refuse to run any agent that does not have a valid cryptographic signature from a trusted author.

## Privacy and Data Rules

1.  **User Data Stays Local by Default:** An agent cannot move user data off the device unless it is granted an explicit permission to do so for a specific, user-approved purpose (e.g., cloud backup).
2.  **Privacy is Not a Feature, It's the Foundation:** The system must be designed to be privacy-preserving at every layer. Convenience can never justify a compromise in user privacy.

## Development and Governance Rules

1.  **The Unified Documentation is the Source of Truth:** All development work by AI agents must be directly traceable to a requirement or design specified in the `docs` repository.
2.  **Pain-Driven Development:** No feature should be built simply because it "might be useful." All significant development must be justified by addressing a known, repeated failure or a validated user need.
3.  **Security Review is Non-Negotiable:** No new feature can be deployed without being audited by the Security AI and reviewed for potential security implications.
4.  **Gitflow Discipline:** Every change traverses the gitflow branches described in the Engineering Playbook (`feature/`, `bugfix/`, `release/`, `hotfix/`). AI personas may open, test, and rebase branches autonomously, but merges into `main` or `release` always wait for a legislator’s approval.
5.  **Autonomous Control with Human Oversight:** QA agents, telemetry stewards, and business feedback loops may detect, triage, and remediate issues without a human trigger, but they must always report the actions taken and pause when a new permission, billing model, or immutable rule is at stake.
6.  **Final Decisions are Human:** Any decision that affects pricing, platform guarantees, or long-lived infrastructure contracts remains under human control. AI agents can recommend options and simulate the trade-offs, but humans must provide the final sign-off before the change is published.
