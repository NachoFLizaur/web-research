<div align="center">

# Web Research MCP

**MCP server for web research with DuckDuckGo search and content extraction.**

No API keys. No configuration. Just `npx` and go.

[![npm](https://img.shields.io/npm/v/web-research-mcp)](https://www.npmjs.com/package/web-research-mcp)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/NachoFLizaur/web-research/blob/main/LICENSE)
[![Node.js](https://img.shields.io/badge/Node.js-%3E%3D18-green.svg)](https://nodejs.org)

</div>

---

## Table of Contents

- [Quick Start](#quick-start)
- [What It Does](#what-it-does)
- [Looking for Pre-Built Agents?](#looking-for-pre-built-agents)
- [Tools](#tools)
  - [multi\_search](#multi_search)
  - [fetch\_pages](#fetch_pages)
- [How It Works](#how-it-works)
- [License](#license)

---

## Quick Start

Add the server to your MCP client config. No install needed — `npx` handles everything.

**Claude Code** (`.mcp.json` in project root):

```json
{
  "mcpServers": {
    "web-research": {
      "command": "npx",
      "args": ["web-research-mcp"]
    }
  }
}
```

**OpenCode** (`opencode.json`):

```json
{
  "mcpServers": {
    "web-research": {
      "command": "npx",
      "args": ["web-research-mcp"]
    }
  }
}
```

Or run it directly:

```bash
npx web-research-mcp
```

---

## What It Does

Two MCP tools for AI assistants to search the web and extract page content:

- **`multi_search`** — Search DuckDuckGo with multiple queries in parallel
- **`fetch_pages`** — Fetch and extract clean text from web pages

No API keys required. Works with any MCP-compatible client.

---

## Looking for Pre-Built Agents?

If you want ready-to-use AI agents for web research (not just the raw tools), check out [`web-research-toolkit`](https://www.npmjs.com/package/web-research-toolkit). It installs pre-built agents and skills for Claude Code and OpenCode — one command, fully configured.

```bash
npx web-research-toolkit install opencode
```

---

## Tools

### multi_search

Search the web using multiple queries via DuckDuckGo. Returns deduplicated results across all queries.

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `queries` | `string[]` | Yes | — | Search queries to execute |
| `results_per_query` | `number` | No | `5` | Number of results per query |

**Returns:** Deduplicated URLs, snippets, titles, and per-query mapping.

**Example call:**

```json
{
  "queries": ["rust async runtime", "tokio vs async-std"],
  "results_per_query": 3
}
```

### fetch_pages

Fetch and extract clean text content from multiple web pages in parallel.

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `urls` | `string[]` | Yes | — | URLs to fetch |
| `max_chars` | `number` | No | `15000` | Max characters per page |
| `timeout` | `number` | No | `30` | Timeout in seconds per request |

**Returns:** Extracted text content, page titles, and per-URL error details.

**Example call:**

```json
{
  "urls": ["https://docs.rs/tokio/latest/tokio/", "https://async.rs/"],
  "max_chars": 10000
}
```

---

## How It Works

- **Search** — Scrapes DuckDuckGo HTML results (no API key needed). Runs queries in parallel and deduplicates URLs across results.
- **Content extraction** — Uses [Mozilla Readability](https://github.com/mozilla/readability) to extract article text from raw HTML, stripping navigation, ads, and boilerplate.
- **Smart truncation** — Limits extracted text to `max_chars` to keep responses within context window limits.
- **Parallel fetching** — Fetches multiple pages concurrently with per-request timeouts.

---

## License

[MIT](https://github.com/NachoFLizaur/web-research/blob/main/LICENSE)
