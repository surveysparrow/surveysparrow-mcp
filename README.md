# SurveySparrow MCP Server

A Model Context Protocol (MCP) server for SurveySparrow. This integration exposes SurveySparrow surveys and responses to any MCP-compatible client via a hosted endpoint. It follows the Model Context Protocol spec for interoperability.

The service is actively optimized based on real-world usage and more tools are coming soon.

## Remote Server URL

```
https://integrations.surveysparrow.com/surveysparrow/mcp
```

Point any MCP-enabled client to this address to begin.

## Example Usage

Ask your AI assistant to:

- 🗂️ **List Surveys** — "List all my active surveys."
- 📊 **Analyze Responses** — "Analyze responses for my NPS survey over the last 7 days."
- 🧩 **Create a Survey** — "Create a CSAT survey to collect customer feedback."
- ⌨️ **Edit a Survey** — "Rename survey 123 to 'NPS Survey (Q4)'."
- 📬 **Share a Survey** — "Share survey 123 by email to my mailing list."
- 📄 **List Responses** — "Show the 50 most recent responses for survey 123."

## Compatibility

| Product | Deployment type | Support status |
|---------|----------------|----------------|
| SurveySparrow | Cloud (hosted endpoint) | ✅ Fully supported via https://integrations.surveysparrow.com/surveysparrow/mcp |

## Quick Start Guide

### 🔐 1) Authentication Setup (OAuth 2.0)

SurveySparrow MCP requires OAuth for every user on first connect.

1. Add the server URL in your MCP client
2. You'll be shown a SurveySparrow OAuth consent screen to authorize access to your SurveySparrow data
3. Approve the requested scopes to connect

Requested scopes: `view_survey`, `manage_survey`, `view_questions`, `view_question`, `manage_question`, `manage_survey_share`, `view_survey_responses`.

#### Manage / Revoke Access

Manage or revoke connected applications from your SurveySparrow account settings.

**Note:** OAuth 2.0 is required for all connections.

### 📦 2) Installation

No server install needed.

- Use the hosted endpoint: `https://integrations.surveysparrow.com/surveysparrow/mcp`
- Add the URL in your MCP-capable client and authorize

## 🛠️ IDE Integration

### Cursor IDE

Settings → MCP Servers → Add:

```json
{
  "mcpServers": {
    "surveysparrow": {
      "url": "https://integrations.surveysparrow.com/surveysparrow/mcp"
    }
  }
}
```

### Claude Desktop

Add to your configuration:

```json
{
  "mcpServers": {
    "surveysparrow": {
      "url": "https://integrations.surveysparrow.com/surveysparrow/mcp"
    }
  }
}
```

### VS Code Extension

Command Palette → "MCP: Add Server" → paste URL → Authorize

No extra configuration is needed after approval.

## Configuration

### ⚙️ Configuration Methods

Configuration options are minimal — only OAuth setup is required.

### 👥 HTTP Transport Configuration

The server communicates over HTTPS using the Streamable HTTP MCP transport with standard MCP client-server interactions.

## Tools

### Key Tools

- `list_surveys` - List the surveys in your account
- `get_survey_info` - Get a survey's configuration and metadata
- `list_responses` - Get responses for a survey
- `analyze_responses` - Analyze and summarize a survey's responses
- `preview_survey` - Build and preview a new survey draft
- `edit_survey` - Edit an existing survey
- `publish_survey` - Publish a survey to start collecting responses
- `share_survey` - Share a survey (for example, over email)

This MCP is actively maintained, and more tools will come soon.

### Tool Filtering & Access Control

Access control is managed via OAuth scopes. Only explicitly granted scopes are available to the client.

## Troubleshooting & Debugging

### Rate Limits

Rate limits follow the same per-user limits as the SurveySparrow REST API. If limits are exceeded, the server returns an HTTP 429 response.

**Important:** Ensure you complete the OAuth flow on first connect.

## Security

- OAuth 2.0 required for all connections
- Manage and revoke connected applications from your SurveySparrow account settings

## Contributing

Follow issues and discussions on this repository, or contact the SurveySparrow team for updates and early access to new tools.

## License

MIT

## Support

- **Developer docs**: https://developers.surveysparrow.com
- **Website**: https://surveysparrow.com
