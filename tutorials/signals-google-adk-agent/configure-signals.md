---
title: "Configure Snowplow Signals"
sidebar_label: "Configure Signals"
position: 4
description: "Create an attribute group from the Basic Web template, publish it, and expose the attributes through a Signals service for lookup by session ID."
keywords: ["Signals", "attribute group", "service", "Basic Web", "domain_sessionid"]
date: "2026-04-17"
---

Now that events are flowing, you need to tell Signals what to compute from them. You define attribute groups — the specific metrics you care about — and Signals keeps them current as events arrive.

## Use a templated attribute group

Instead of building an attribute group from scratch, use one of Signals' built-in templates.

1. In Snowplow Console, navigate to **Signals → Attribute Groups**
2. Click **Create attribute group** and choose **Basic Web** (or a template suited to your use case)
3. Set the **Attribute Key** to `domain_sessionid` to aggregate attributes at the session level

The Basic Web template includes these attributes:

| Attribute               | Description                               |
| ----------------------- | ----------------------------------------- |
| `page_views_count`      | Total number of page views in the session |
| `unique_pages_viewed`   | A map of each distinct page path to the number of times it was viewed in the session (e.g. `{"/products/electronics/wireless-headphones": 3, "/pricing": 1}`) |
| `first_event_timestamp` | When the session started                  |
| `last_event_timestamp`  | When the most recent event was recorded   |

Click **Run Preview** to validate the attribute group against recent events in your warehouse, then click **Create Attribute Group**.

## Publish the attribute group

Attribute groups need to be published before they start computing:

1. Open your attribute group and click **Publish**
2. Confirm the publish — this deploys the computation logic to the pipeline

Once published, Signals starts computing attributes for each user session as events arrive.

## Create a service

A service is a pull-based API endpoint that exposes your computed attributes for a specific lookup key. You'll fetch attributes by `domain_sessionid` from your Python agent.

1. Navigate to **Signals → Services**
2. Click **New Service**
3. Configure:
   - **Name**: `web_agent_context` (must match `SNOWPLOW_SIGNALS_SERVICE_NAME` in your `.env`)
   - **Attribute Group**: the one you just published
4. Click **Create**

The service's response for a given session ID looks like:

```json
{
  "page_views_count": 12,
  "unique_pages_viewed": {
    "/": 1,
    "/products/electronics": 2,
    "/products/electronics/wireless-headphones": 4,
    "/products/electronics/smart-speaker-mini": 2,
    "/pricing": 3
  },
  "first_event_timestamp": "2026-04-09T14:23:01.000Z",
  "last_event_timestamp": "2026-04-09T14:41:03.000Z"
}
```

Because `unique_pages_viewed` is a map of paths to view counts, the agent sees exactly which products and categories the user has been browsing on.
