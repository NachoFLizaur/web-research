# Web Research

A web research toolkit for AI coding assistants — an MCP server for search and content extraction, plus pre-built agents for Claude Code and OpenCode.

## What's Included

This monorepo ships two npm packages:

- **`web-research-mcp`** — MCP server with two tools: `multi_search` (DuckDuckGo) and `fetch_pages` (parallel content extraction)
- **`web-research-toolkit`** — Installs pre-built AI agents and skills into your project for Claude Code or OpenCode

## Quick Start

```bash
# Install agents for your tool
npx web-research-toolkit install claude-code
# or
npx web-research-toolkit install opencode
```

That's it. The toolkit installer configures the MCP server for you — no separate setup needed.

## MCP Server

The `web-research-mcp` package provides two MCP tools. If you only want the server (without agents), add it to your MCP client config manually:

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

### multi_search

Search the web using multiple queries via DuckDuckGo.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `queries` | `string[]` | *(required)* | Search queries to execute |
| `results_per_query` | `number` | `5` | Results per query |

**Returns:** Deduplicated URLs, snippets, titles, and per-query mapping.

### fetch_pages

Fetch and extract clean text from multiple web pages in parallel.

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `urls` | `string[]` | *(required)* | URLs to fetch |
| `max_chars` | `number` | `15000` | Max characters per page |
| `timeout` | `number` | `30` | Timeout in seconds |

**Returns:** Extracted text content, titles, and errors per URL.

## Agents & Skills

The toolkit installs **agents** (autonomous subagents with a defined workflow) and **skills** (on-demand expertise that agents load when needed).

### Agents

- **`web-searcher`** — Quick web search agent. Runs a few targeted queries and returns URLs, snippets, or direct answers.
- **`deep-researcher`** — Comprehensive multi-source research agent. Expands a research question into 10 diverse queries, searches all in parallel, fetches every result page, and synthesizes a detailed report with citations.

### Skills

- **`web-search`** — Search methodology and result handling
- **`deep-research`** — Multi-phase research workflow

### Installation

**Claude Code:**

```bash
npx web-research-toolkit install claude-code
```

**OpenCode:**

```bash
npx web-research-toolkit install opencode
```

## Architecture

Prompts are maintained once and work across platforms:

- **Canonical prompts** in `packages/toolkit/prompts/` — pure instructions, no frontmatter
- **Platform templates** in `packages/toolkit/templates/` — frontmatter specific to each platform
- **Installer** assembles frontmatter + prompt body at install time, replacing `{{placeholders}}` with metadata

This means adding a new platform only requires new templates — the prompt content stays shared.

## Development

```bash
npm install          # install all workspace deps
npm run build        # build both packages
npm test             # test both packages
npm run typecheck    # type check both packages
```

Monorepo structure:

```
packages/
├── mcp/       # web-research-mcp — MCP server
└── toolkit/   # web-research-toolkit — agent installer
```

## Publishing

```bash
npm publish -w packages/mcp
npm publish -w packages/toolkit
```

## License

MIT
