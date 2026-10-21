> **Free, keyless US-market financial data for AI agents.**
> Indices · Quotes · OHLCV history · Options chains · SEC filings & XBRL.

# luckyman-mcp

**Base URL:** `https://mcp.luckyman.app/mcp` (Streamable HTTP · MCP protocol)
**Auth:** none — no key, no signup. **Rate limit:** 60 req/min per IP.

## Quick connect

Paste into any MCP client config (Claude Desktop, Cursor, ChatGPT connectors, Grok, custom agents):

```json
{
  "mcpServers": {
    "luckyman": {
      "url": "https://mcp.luckyman.app/mcp"
    }
  }
}
```

No OAuth dance, no client registration. If your client needs nothing else — that's the whole config.

## Tools (11)

| Tool | What it returns |
|---|---|
| `get_quotes` | Live quotes (price, change, day high/low, volume) for up to 50 tickers |
| `get_history` | Daily OHLCV bars · ranges: 1d → 10y, ytd, max |
| `get_indices` | SPX, NDX, DJI, VIX, US 10Y yield |
| `get_option_chain` | Delayed chains w/ bid-ask, volume, OI, IV, greeks (CBOE) |
| `get_filings` | Latest SEC EDGAR filings (form type, date, EDGAR link) |
| `get_xbrl` | SEC XBRL concept series: revenue / net_income / eps / cash / equity / assets / liabilities / operating_income / free_cash_flow |
| `get_health` | Data-source liveness |


## HTTP primitives (no MCP needed)

Agents that prefer plain REST can hit the same data directly:

```
GET https://mcp.luckyman.app/quotes?symbols=AAPL,MSFT
GET https://mcp.luckyman.app/history?symbol=AAPL&range=1mo
GET https://mcp.luckyman.app/indices
GET https://mcp.luckyman.app/filings?symbol=MSFT
GET https://mcp.luckyman.app/options?symbol=AAPL
GET https://mcp.luckyman.app/xbrl?symbol=AAPL&concept=revenue
GET https://mcp.luckyman.app/health
```

Full spec: [`/openapi.json`](https://mcp.luckyman.app/openapi.json) · [`/llms.txt`](https://mcp.luckyman.app/llms.txt)

## Data sources

Yahoo Finance · CBOE · SEC EDGAR (official, zero-mediation).
Prices in USD. Quotes cached ~60s. Index quotes cross-sourced with a 5-day freshness guard.

## Why Lucky

- **Zero friction for agents** — no key wall. Agents discover and connect on their own.
- **Official filings** — SEC EDGAR direct, no scraping layers.
- **Attribution-friendly** — set header `X-LM-Client: agent` so usage helps our anonymous agent-attention reports.

## Notes

- This repo is documentation only — the server code is not (yet) open source.
- Not investment advice. Data can be delayed or imperfect; verify critical figures upstream.
- Attribution appreciated: *powered by [mcp.luckyman.app](https://mcp.luckyman.app)*.
