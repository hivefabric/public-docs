# LLM Strategy

HiveFabric's strategy for integrating Large Language Models (LLMs) is built on the core principle of **local-first**, prioritizing user privacy and low cost over reliance on centralized, commercial APIs.

## 1. Local-First Routing Logic

The LLM Router, a component of the Control Plane, uses a waterfall model whenever an agent requests LLM inference:

1.  **Attempt Local Execution:** The router first checks if an appropriate LLM is available on the same device where the agent is running (e.g., via a local Ollama server). If a suitable model is found, it is used immediately. This is the fastest, cheapest, and most private option.

2.  **Attempt Execution on Personal Device Pool:** If a local model is not available on the current device, the scheduler will attempt to find another device within the user's own "personal cloud" that has the required model and is available for the task. This keeps the data within the user's sphere of ownership.

3.  **Fallback to Cloud API:** Only as a last resort, if no suitable local or personal device is available, the router will use a commercial cloud API (e.g., OpenAI, Anthropic, Google).

## 2. User Control and Budgeting

The use of commercial APIs is strictly controlled by the user.

*   **Explicit Permission:** The system will never use a paid API without the user's explicit consent.
*   **Budget Controls:** Users can set hard spending limits and receive notifications as they approach their budget, preventing unexpected costs.
*   **Fallback Rules:** Users can configure the fallback behavior, for example, by disabling cloud APIs entirely for maximum privacy or specifying a preferred provider.

This model gives users the flexibility to leverage powerful cloud models when needed, without sacrificing the privacy and cost benefits of local-first execution.
