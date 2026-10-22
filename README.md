# Recoup MCP server

Recoup checks every ticket an ecommerce brand's AI support agent (Gorgias, Zendesk, Intercom Fin and others) closes against Shopify and Stripe, and flags refunds promised but never issued, refunds issued twice, wrong amounts and credits outside policy. Read-only: it never moves money.

This MCP server answers product, pricing and fit questions about Recoup and runs a refund exposure estimate from the numbers you give it. It reads no customer data.

- **Endpoint:** `https://recoupaudit.com/mcp/`
- **Transport:** Streamable HTTP
- **Sign-in:** none. No API key, no account.
- **Access:** every tool is read-only.
- **MCP Registry name:** `io.github.Aguna18/recoup`

This repository holds setup instructions and the registry entry only. It contains no product code.

## Add it to Claude

Customize, Connectors, Add, Add custom connector, then paste:

```
https://recoupaudit.com/mcp/
```

ChatGPT: in developer mode, add a connector with the same URL.

## Cursor, VS Code, Windsurf and other clients

Add this to your MCP config:

```json
{
  "mcpServers": {
    "recoup": {
      "type": "http",
      "url": "https://recoupaudit.com/mcp/"
    }
  }
}
```

## Tools

| Tool | What it returns |
| --- | --- |
| `get_recoup_overview` | What Recoup checks, who it is for, what it needs and what it never does. |
| `get_recoup_pricing` | The free browser audit, the done-for-you audit and the Monitor plans. |
| `estimate_refund_exposure` | Money promises, mismatches and dollars at stake per month from your ticket volume. Defaults come from a labelled sample dataset. |
| `list_supported_sources` | Help desks and money systems Recoup reads, with the page for each. |

A GET request to `https://recoupaudit.com/mcp/` shows the server's name and tools.

## Things to ask it

- How do I check whether refunds our Gorgias AI Agent promised were actually issued in Shopify?
- We close 4,000 AI tickets a month. Roughly how much refund money could be off?
- Is there a read-only tool that audits Intercom Fin refunds against Stripe?

## Privacy

The server reads no customer data and stores nothing you send it. It only answers questions about Recoup and runs estimates from the numbers you give it. Full policy: https://recoupaudit.com/privacy/

## Links

- Website: https://recoupaudit.com/
- Guide for AI agents: https://recoupaudit.com/agents/
- Privacy: https://recoupaudit.com/privacy/

## Registry publishing

`server.json` is published to the official MCP Registry (registry.modelcontextprotocol.io) by `.github/workflows/publish-mcp.yml`, which logs in with GitHub OIDC. No token is stored in this repository.

---

Made by AGUNA WELLNESS LTD.

The MIT license covers the files in this repository.
