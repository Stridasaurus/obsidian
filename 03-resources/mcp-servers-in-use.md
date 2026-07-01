---
title: "MCP servers configured for Claude Code sessions"
type: reference
domain: claude-workflow
status: active
created: 2026-06-30
updated: 2026-07-01
tags:
  - claude-workflow/configuration
source: ""
source_url: ""
---

# MCP servers in use

## Obsidian MCP

`mcp__obsidian__*` tools. Available in every session from any repo (declared in `~/.claude/CLAUDE.md`). This is the primary mechanism for this vault's read/write/search continuity.

## GitHub MCP

`@modelcontextprotocol/server-github`, registered globally at `--scope user` with a `GITHUB_PERSONAL_ACCESS_TOKEN` env var (90-day expiration). Added 2026-06-30 (session 6).

**Status: tested working, 2026-07-01.** `claude mcp list` shows it connected; confirmed functional (not just connected) by fetching live file content from a real repo via `get_file_contents`.

## Notes

- Kepano's skill pack (`[[skills-kepano-obsidian]]`) is a skills install, not an MCP server — listed separately.
