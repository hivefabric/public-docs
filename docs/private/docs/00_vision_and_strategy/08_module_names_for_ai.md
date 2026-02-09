# Module Naming Guide for AI Personas

Agents and personas need clear labels when reasoning about HiveFabric components, so they stay aligned with the human story names. This guide defines the names and gives hints for when an AI should translate between narrative and technical roles.

## Name mappings for reasoning

| Component | Story Name | Technical Role | When to Use |
|-----------|------------|----------------|-------------|
| Control Plane | **Honeycomb** | REST/gRPC/NATS scheduler service | Use whenever you plan scheduling, registration, or API updates; pair with comb/queue logic. |
| Agent Registry | **Apiary** | Manifest store / marketplace metadata engine | Mention Apiary when tasks span cataloging, signing, or version history across agents. |
| Executor Runtime | **Wax** | Runtime host (WASP/WASM sandbox) | Use Wax when the plan touches sandbox limits, local LL/MS integration, or node isolation. |
| Node | **Comb** | Executor device | Always refer to comb when modeling heartbeats, resources, or scheduling destinations. |

## Reasoning tips

* When drafting code changes, keep the narrative name and technical role both visible: e.g., “Honeycomb (control plane) should publish comb status.”
* Avoid inventing new metaphors; translate requirements back to Honeycomb/Apiary/Wax/comb before generating patches, tests, or docs.
* If humans ask for “comb behavior,” there is no need to translate; treat comb as the executor instance in your reasoning chain.

Consistency ensures humans and AI share the same mental model.
