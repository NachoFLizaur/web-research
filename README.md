# Web Research MCP Server

MCP server for web research - search and page fetching.

## Features

- **multi_search**: Search using multiple queries via DuckDuckGo
- **fetch_pages**: Fetch and extract content from multiple URLs in parallel

## Installation

```bash
# Using the launcher script (auto-creates venv)
./run.sh

# Or manual installation
python3 -m venv .venv
.venv/bin/pip install -e .
```

## Usage

This MCP server is designed to be used with OpenCode or other MCP-compatible clients.

## Dependencies

- `mcp` - Model Context Protocol SDK
- `duckduckgo-search` - DuckDuckGo search API
- `requests` - HTTP library
- `beautifulsoup4` - HTML parsing
