# MCP Server Configurations

This folder contains MCP (Model Context Protocol) server configs that connect your agent to external tools and data sources.

## Example Servers
- `snowflake` - Query execution against data warehouse
- `slack` - Channel monitoring, message triage, heartbeat polling
- `gmail` - Email ingestion for meeting notes and inbound requests
- `google-calendar` - Calendar reads for meeting prep, time-block writes for daily planning
- `google-drive` - Document sync and backup
- `mode` - Dashboard and query management
- `figma` - Design file reads

## How It Works
Each MCP server is configured in your agent's settings. The agent uses these connections to:
1. Sync cloud artifacts to your local project folders
2. Poll Slack and email for the heartbeat triage loop
3. Read and write calendar events for daily planning
4. Execute queries and back them up locally
