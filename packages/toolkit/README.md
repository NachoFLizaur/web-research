<div align="center">

# Web Research Toolkit

**Pre-built AI agents and skills for web research, compatible with Claude Code and OpenCode.**

One command. Fully configured. Start researching.

[![npm](https://img.shields.io/npm/v/web-research-toolkit)](https://www.npmjs.com/package/web-research-toolkit)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/NachoFLizaur/web-research/blob/main/LICENSE)
[![Node.js](https://img.shields.io/badge/Node.js-%3E%3D18-green.svg)](https://nodejs.org)

</div>

---

## Table of Contents

- [Quick Start](#quick-start)
- [What It Does](#what-it-does)
- [What Gets Installed](#what-gets-installed)
- [Agents](#agents)
  - [web-searcher](#web-searcher)
  - [deep-researcher](#deep-researcher)
- [Skills](#skills)
- [Architecture](#architecture)
- [The MCP Server](#the-mcp-server)
- [License](#license)

---

## Quick Start

```bash
npx web-research-toolkit install opencode
```

or

```bash
npx web-research-toolkit install claude-code
```

That's it. The installer configures the MCP server, installs agents, and sets up skills — no separate setup needed.

---

## What It Does

Installs pre-built AI agents and skills into your project for web research:

- **Agents** — Autonomous subagents with defined workflows (quick search and deep research)
- **Skills** — On-demand expertise that agents load when needed (search methodology, research workflow)
- **MCP server** — Automatically configured to provide search and content extraction tools

Everything is installed locally in your project directory. One command, zero configuration.

---

## What Gets Installed

| File | Claude Code | OpenCode |
|------|:-----------:|:--------:|
| MCP server config | `.mcp.json` | `opencode.json` |
| Plugin manifest | `.claude-plugin/plugin.json` | — |
| Web Searcher agent | `agents/web-searcher.md` | `.opencode/agents/web-searcher.md` |
| Deep Researcher agent | `agents/deep-researcher.md` | `.opencode/agents/deep-researcher.md` |
| Web Search skill | `skills/web-search/SKILL.md` | `.opencode/skills/web-search/SKILL.md` |
| Deep Research skill | `skills/deep-research/SKILL.md` | `.opencode/skills/deep-research/SKILL.md` |

---

## Agents

### web-searcher

Quick web search agent. Runs 1-3 targeted queries and returns concise answers with source URLs.

**Good for:**
- Factual lookups ("What's the latest version of React?")
- Finding documentation or API references
- Quick answers with sources

**How it works:** Formulates focused search queries, calls `multi_search`, and returns URLs, snippets, or direct answers. Fast and lightweight.

### deep-researcher

Comprehensive multi-source research agent. Expands a research question into 10 diverse queries, searches all in parallel, fetches every result page, and synthesizes a detailed report.

**Good for:**
- Complex technical questions ("How do different ORMs handle connection pooling?")
- Comparative analysis ("Pros and cons of server-side rendering frameworks")
- Topics requiring multiple sources and synthesis

**How it works:** Generates diverse search queries, runs them all via `multi_search`, fetches full page content with `fetch_pages`, then synthesizes findings into a structured report with citations and confidence levels.

---

## Skills

Skills are methodology guides that agents load on demand.

| Skill | What It Covers |
|-------|---------------|
| **web-search** | Search methodology — when to search vs. fetch, query optimization, result handling |
| **deep-research** | Multi-phase research workflow — query expansion, source evaluation, synthesis |

Skills are loaded automatically when an agent determines they're relevant to the current task.

---

## Architecture

Prompts are maintained once and work across platforms:

- **Canonical prompts** — Pure instructions, no platform-specific frontmatter
- **Platform templates** — Frontmatter and metadata specific to each platform (Claude Code, OpenCode)
- **Installer** — Assembles frontmatter + prompt body at install time, replacing `{{placeholders}}` with metadata

Adding support for a new platform only requires new templates — the prompt content stays shared.

---

## The MCP Server

This toolkit uses [`web-research-mcp`](https://www.npmjs.com/package/web-research-mcp) under the hood. The installer configures it automatically — you don't need to set it up separately.

If you want just the MCP server without agents, see the [`web-research-mcp` package](https://www.npmjs.com/package/web-research-mcp).

---

## License

[MIT](https://github.com/NachoFLizaur/web-research/blob/main/LICENSE)
