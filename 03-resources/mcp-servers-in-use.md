---
title: "MCP servers configured for Claude Code sessions"
type: reference
domain: claude-workflow
status: draft
created: 2026-06-30
updated: 2026-06-30
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

**Status: untested as of 2026-06-30.** Needs a Claude Code restart and verification that GitHub tools actually appear in `/context` before relying on it.

## Notes

- Kepano's skill pack (`[[skills-kepano-obsidian]]`) is a skills install, not an MCP server — listed separately.
