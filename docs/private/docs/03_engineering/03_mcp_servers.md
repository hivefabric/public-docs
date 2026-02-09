# MCP Server Inventory

This file tracks the MCP (Model/Metadata Control Plane) servers that the AI project agents can query via `list_mcp_resources`. Update this list as soon as a new MCP is available and provide the following details:

| Name | Purpose | Access Details | Owner | Notes |
|---|---|---|---|---|
| (example) telemetry-ingest | Telemetry ingestion endpoints for Loki/ClickHouse events | server-id: `telemetry-prod`, credentials stored in Vault | DevOps AI | Use `list_mcp_resources` to read latest dashboards |

Add entries when MCP slots become available, including credentials or alias instructions, so agents can fetch necessary context without delay.
