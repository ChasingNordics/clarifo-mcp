# Clarifo MCP server

Clarifo is a financial research platform for US and Nordic listed companies.
Its hosted, read-only MCP server lets AI assistants search company filings,
pull financial statements, compare and screen companies, and cite every
figure back to the page of the report it came from.

- **Data:** SEC filings (10-K, 10-Q, 8-K) and Nordic annual and interim
  reports (ESEF), with financial statements and key figures over multiple
  years.
- **Citations:** every read tool returns page ids that resolve to the source
  page (a rendered report page for Nordic filings, an SEC EDGAR link for US
  filings).
- **Read-only:** no tool creates, edits or deletes data.

Full documentation, the tool list, plans and limits:
**https://www.clarifo.com/docs/mcp**

> This repository holds the listing metadata and setup instructions for the
> hosted service. It is not the server's source code and is not open source.

## Endpoint

```text
https://mcp.clarifo.com/mcp
```

Streamable HTTP. Authentication is OAuth 2.1: on first connection your client
opens a browser and you sign in with your Clarifo account (a 7-day free trial
is available on the sign-in screen). Headless integrations can send a Clarifo
Data API key as a bearer token instead; see the documentation.

## Connect

**Claude (web, desktop, mobile):** open the Clarifo listing in the
[Claude Connectors Directory](https://claude.ai/directory/connectors/clarifo)
and click **Connect**.

**ChatGPT:** add the Clarifo app from the
[ChatGPT apps directory](https://chatgpt.com/plugins/plugin_asdk_app_6a620fee8fb081918a53bd0341a34664).

**Config-file clients** (Claude Desktop format shown; Cursor's file layout is in the
[documentation](https://www.clarifo.com/docs/mcp#config-file-cursor--others)):

```json
{
  "mcpServers": {
    "clarifo": {
      "url": "https://mcp.clarifo.com/mcp",
      "auth": "oauth"
    }
  }
}
```

Restart the client after editing the config; the first request triggers the
OAuth sign-in.

## Example prompts

- "Compare NVIDIA and AMD data-center segment revenue and gross margin across the last four quarters."
- "Get Nokia Q1 2026 revenue and compare it to Ericsson for the same quarter."
- "Summarize the AI risk factors in Microsoft's latest 10-K and compare them to Alphabet's."
- "How do Nordic industrial companies apply IFRS 16 to leases in their latest annual reports?"

## Support and security

Questions and security reports: [support@clarifo.com](mailto:support@clarifo.com).
Please do not open issues here; this repository does not track them.

## Links

- Product: https://www.clarifo.com/product/features
- MCP documentation: https://www.clarifo.com/docs/mcp
- Pricing: https://www.clarifo.com/pricing
