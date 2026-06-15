---
title: "Implementing the Airbyte MCP Part 1: Authentication"
url: "https://airbyte.com/blog/implementing-airbyte-mcp"
date: "2026-06-01"
author: "Cameron Kennedy"
feed_url: "https://airbyte.com/blog"
---
This post explains how Airbyte implemented authentication for their Model Context Protocol (MCP) server, using FastMCP's OIDCProxy class with Keycloak to handle OAuth 2.1 authentication. The approach allows MCP clients to securely access Airbyte connectors without directly exposing Keycloak tokens.
