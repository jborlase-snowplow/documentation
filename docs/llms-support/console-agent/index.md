---
title: "Console Agent"
sidebar_label: "Console Agent"
sidebar_position: 50
description: "The Console Agent is an AI assistant built into Snowplow BDP Console that lets you manage your tracking plans, pipelines, and data quality through natural language."
keywords: ["console agent", "ai assistant", "ai agent", "natural language", "console", "automation"]
date: "2026-04-10"
---

The Console Agent is an AI assistant embedded in [Snowplow BDP Console](https://console.snowplowanalytics.com). It lets you manage your tracking implementation, monitor pipelines, troubleshoot issues, and configure Signals through natural language conversation.

## How it works

The Console Agent runs as a chat interface inside the Console. When you send a message, the agent determines which tools and skills to use, calls the relevant Snowplow APIs on your behalf, and returns the results in a conversational format.

It is context-aware: the agent knows which Console page you're on and can tailor its responses accordingly. If [Signals](/docs/signals/concepts/index.md) is enabled for your account, the agent can also incorporate real-time behavioral attributes from your current session.

### Permissions

The Console Agent operates with **your existing Console permissions**. It authenticates using your current session and can only perform actions that your account is authorized to do. It cannot escalate privileges or access resources outside your organization.

Any action that modifies data (creating a schema, updating an enrichment, deleting an alert) requires your explicit confirmation before the agent proceeds.

## Capabilities

The agent provides assistance across several areas of the Console. It loads specialized skills on demand based on your request.

### Tracking design

Design and implement your event tracking using natural language:

- Create and manage [data structures](/docs/fundamentals/schemas/index.md) (Iglu schemas)
- Create and manage [event specifications](/docs/event-studio/tracking-plans/event-specifications/index.md) with entity contexts
- Create and manage [tracking plans](/docs/event-studio/tracking-plans/index.md)
- Search [Iglu Central](https://github.com/snowplow/iglu-central) for reusable public schemas
- Browse the data catalog to understand what is already being tracked

### Implementation guidance

Get help instrumenting Snowplow trackers in your applications:

- Generate copy-paste-ready tracking code for web, mobile, and server-side platforms
- Look up schema definitions and event specifications for correct implementation
- Follow a guided workflow from instrumentation through to production deployment

### Pipeline management

Explore and understand your pipeline infrastructure:

- List pipelines with their status, collector endpoints, and labels
- View real-time pipeline metrics including throughput, enrichment latency, and bad row rates
- Review collector configuration (CNAME, cookie policy, DNS)
- List and manage enrichments
- View mini and Micro development instances

### Troubleshooting

Diagnose and resolve pipeline issues:

- Investigate [failed events](/docs/fundamentals/failed-events/index.md) with detailed error breakdowns
- Analyze schema validation failures and enrichment errors
- Drill into specific errors by app ID and tracker version
- Get targeted recommendations for fixes

### Data quality

Manage alerts for data quality issues:

- Create and manage data quality alerts via email or Slack
- Filter alerts by app ID, issue type, or data structure
- Update or remove existing alert configurations

### Console operations

Perform day-to-day management tasks:

- View and manage source applications, including their platform, app IDs, and entity definitions
- Navigate directly to relevant Console pages from the chat
- Search and browse the Snowplow documentation

### Signals

If [Signals](/docs/signals/concepts/index.md) is enabled for your organization, the agent can help you configure and manage it:

- Define and manage attribute keys and attribute groups
- Create services for pull-based attribute access
- Set up interventions for push-based actions
- Test attribute groups against sample data
- Publish and unpublish configurations
- Query real-time attributes for specific users
