# Questions for Human Legislators

This list captures the open decisions and inputs the autonomous agents need before proceeding with significant changes or budget-sensitive work.

1. **Objectives & KPIs**: What are the current OKRs, revenue targets, or success metrics you want us to prioritize this sprint (e.g., scheduler latency, Pro churn, marketplace revenue)?
2. **Budget & Cost Controls**: Should we keep the meta-parameter percentages (80% dev compute, 90% testing) as-is, or adjust them based on new compute availability or strategic focus? Who signs off when we need to rebalance company/meta-agent vs. user compute spend?
3. **MCP Servers**: Which MCP servers (names/URIs/aliases) should the agents query when they become available? Where should credentials or access instructions be recorded so `list_mcp_resources` can find them?
4. **Decision Gates**: Which types of changes always pause for your input? (Examples: new billing models, cloud contract changes, expensive GPUs, permissions that allow data exfiltration.)
5. **Multi-Tenancy Boundaries**: How should we separate company/meta-agent compute from user workloads? Are there distinct quotas, cost centers, or monitoring dashboards we should honor?
6. **Telemetry Thresholds**: Are there specific upper/lower bounds (e.g., scheduler miss rate, QA failure rate, cost per task) that should auto-trigger human review before merging or scaling?
7. **New Repositories / Projects**: When a new repo spins up (control plane services, executor runtime, ops), should we add it to `docs/09_repo_organization/repo_map.md` automatically, or do you prefer a manual sign-off per repo?

Answering these questions ensures the autonomous loop respects human governance while keeping the project moving fast.
