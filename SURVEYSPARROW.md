# SurveySparrow Gemini CLI Extension

## Overview

This extension connects Gemini CLI to SurveySparrow's hosted Model Context Protocol (MCP) server at `https://integrations.surveysparrow.com/surveysparrow/mcp`.

## Installation

To install the extension, run the following command in your terminal:

```bash
gemini extensions install https://github.com/surveysparrow/surveysparrow-mcp
```

Once installed, start Gemini CLI by running:

```bash
gemini
```

## Authentication

Prior to using tools from the SurveySparrow MCP server you must authenticate. This is done by running `/mcp auth surveysparrow` which will open an OAuth flow in your browser:

```
/mcp auth surveysparrow
```

After authenticating, all the SurveySparrow tools will be available.

## Available Tools

The SurveySparrow MCP server exposes the following tools. Invoke them with natural language:

- **list_surveys**: List the surveys in your account (filter by type or archived state).
- **get_survey_info**: Get a survey's configuration and metadata.
- **list_responses**: Get responses for a survey, with an optional date range and limit.
- **analyze_responses**: Analyze and summarize a survey's responses over a time period.
- **preview_survey**: Build and preview a new survey draft (NPS, CSAT, CES, Classic, Conversational).
- **edit_survey**: Edit an existing survey.
- **publish_survey**: Publish a survey to start collecting responses.
- **share_survey**: Share a survey (for example, over email).

## Usage Examples

```
Create a CSAT survey to collect customer feedback
List all my surveys created this month
Show me responses for survey 123456789 from the last 7 days
Analyze the responses for my NPS survey
Share survey 123456789 by email
```

## Troubleshooting

If you have already installed the extension, below are some common troubleshooting steps:

- Run `/mcp list` to confirm the `surveysparrow` server is connected.
- Run `/mcp desc surveysparrow` to see a detailed overview of available tools.
- Run `/mcp auth surveysparrow` to authenticate with SurveySparrow.
