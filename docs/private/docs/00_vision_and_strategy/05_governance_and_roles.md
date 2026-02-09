# Governance and Roles

This document defines the roles and responsibilities for both AI and human contributors to the HiveFabric project, establishing a clear governance model.

## 1. Human Roles: The Legislators

Humans do not micromanage the day-to-day development or operation of agents. Instead, they act as **legislators and strategists** for the system.

*   **Responsibilities:**
    *   Define the high-level mission, vision, and strategy.
    *   Set and approve the project's budget and financial constraints.
    *   Make final decisions on core architectural changes and the "immutable rules."
    *   Approve new security permission classes for agents.
    *   Act as the final arbiters in case of disputes between AI agents.
    *   Interface with the external world (users, community, partners).

*   **Checklist for Human Approval:**
    *   [ ] Any change to the `immutable_rules.md` document.
    *   [ ] The introduction of a new, billable service or a change in the subscription model.
    *   [ ] The creation of a new security permission that could expose user data or system resources.
    *   [ ] Final approval of a major version release (e.g., 1.0, 2.0).
    *   [ ] Any decision that has significant legal or ethical implications.

## 2. AI Roles: The Executors

The AI Personas (defined in `llm_personas/workers/`) are the primary workforce for the project. They are responsible for the implementation, testing, and maintenance of the codebase.

*   **Responsibilities:**
    *   Execute tasks assigned by the Chief Architect AI, using the unified documentation as the source of truth.
    *   Write, test, and document code within their area of specialization.
    *   Review code from other AIs for correctness, performance, and style.
    *   Adhere strictly to the project's architectural and security guidelines.

*   **Checklist for AI Review:**
    *   [ ] Does the code correctly implement the feature described in the task?
    *   [ ] Are there sufficient unit, integration, and end-to-end tests?
    *   [ ] Does the code adhere to the style guide for the language?
    *   [ ] Has the Security AI audited the code for vulnerabilities?
    *   [ ] Does the implementation align with the project architecture as confirmed by the Chief Architect AI?
    *   [ ] Have potential impacts on cost and performance been analyzed by the Finance and Executor AIs?
