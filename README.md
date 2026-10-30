# Clarifo MCP server: SEC filings and Nordic financial data for Claude, ChatGPT and Cursor

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

### Claude (web, Claude Desktop, mobile)

1. Open the Clarifo listing in the
   [Claude Connectors Directory](https://claude.ai/directory/connectors/clarifo)
   and click **Connect**.
2. Sign in with your Clarifo account when the OAuth window opens.

The connector is stored on your Claude account, so it works the same in
Claude Desktop (macOS, Windows), on the web and on mobile.

If the directory is turned off for your workspace, add it as a custom
connector: in Claude go to **Customize > Connectors**, click **+ Add >
Add custom connector**, name it `Clarifo` and paste
`https://mcp.clarifo.com/mcp`. On Team and Enterprise plans an owner adds it
under **Organization settings > Connectors**, and members then click
**Connect**.

### Claude Code

```bash
claude mcp add --transport http --scope user clarifo https://mcp.clarifo.com/mcp
```

Then run `/mcp` inside Claude Code and choose Clarifo to sign in.

### ChatGPT

Add the Clarifo app from the
[ChatGPT apps directory](https://chatgpt.com/plugins/plugin_asdk_app_6a620fee8fb081918a53bd0341a34664).

### Cursor

Add to `~/.cursor/mcp.json` (or `.cursor/mcp.json` in a project):

```json
{
  "mcpServers": {
    "clarifo": {
      "url": "https://mcp.clarifo.com/mcp"
    }
  }
}
```

### Claude Desktop config file (optional)

`claude_desktop_config.json` only starts local servers, so the connector
above is the recommended way. If you manage Claude Desktop through the config
file, the [`mcp-remote`](https://github.com/geelen/mcp-remote) bridge
(Node.js 18+) connects it to the hosted server:

```json
{
  "mcpServers": {
    "clarifo": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.clarifo.com/mcp"]
    }
  }
}
```

The file is at `~/Library/Application Support/Claude/claude_desktop_config.json`
on macOS and `%APPDATA%\Claude\claude_desktop_config.json` on Windows. Restart
Claude Desktop after editing it; the first request opens the OAuth sign-in in
your browser.

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
