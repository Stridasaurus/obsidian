---
title: "CLAUDE.md hierarchy across Code-Repositories — current file contents and rationale"
type: reference
domain: claude-workflow
status: active
created: 2026-06-30
updated: 2026-06-30
tags:
  - claude-workflow/configuration
source: ""
source_url: ""
---

# CLAUDE.md hierarchy

Four-tier context hierarchy across this user's environment, audited and updated 2026-06-30 (session 6) after reviewing an `/insights` usage report. This is the personal-environment instance of the general pattern in `[[agentic-document-cascade]]` (stable invariants at root, volatile detail at leaves) — that note describes the manifesto→SPEC→design→CLAUDE.md cascade *within* a coding project; this note tracks the *cross-repo* CLAUDE.md layering that sits above it.

## Tiers (load order)

1. `~/.claude/CLAUDE.md` — global, every session
2. `Code-Repositories/CLAUDE.md` — applies to all repos under that root
3. Folder-level files — `Python/CLAUDE.md`, `Sites/CLAUDE.md`
4. Individual project `CLAUDE.md` files (e.g. this vault's own `CLAUDE.md`)

**Tiers 1–3 are not in any git repo** — they live outside tracked directories and have no version history.

## Current contents (as of 2026-06-30)

- **`~/.claude/CLAUDE.md`**: Obsidian vault pointer/wrap-up instructions; **Environment** (Windows 11/PowerShell — no Bash heredoc syntax, use `--body-file` for multi-line CLI content); **Planning vs Implementation** (plan-only discipline — don't implement until told to proceed); **Repo State** (never report clean until `git fetch` + `gh pr list`; see `[[skill-repo-state]]`)
- **`Code-Repositories/CLAUDE.md`**: ecosystem best-practices default (npm/cargo/go conventions per project type); **New repo setup** sequence — clone → install deps → run tests/dev server → verify `.gitignore` → generate CLAUDE.md after pulling latest remote; confirm a file exists on remote before deleting it locally
- **`Sites/CLAUDE.md`** (new file, session 6): **Stack & Deploy target** (defers to each project's own CLAUDE.md; check `.github/workflows/` for CI config; kept tech-agnostic on purpose); **Deployment & Verification** (DOM queries not screenshots, check base paths, smoke test before declaring done)
- **`Python/CLAUDE.md`**: **Coding standards** — `ruff format` + `ruff check`; type hints best-effort on public function signatures in installable packages (skip notebook cells); NumPy-style docstrings for public API only
- **`lab-notebooks/CLAUDE.md`**: **What this is** — "low-stakes space for notebooks and experiments before they are formalized into proper documentation or migrated to main projects." Only one of this batch that lives in a tracked git repo; committed and pushed.
- **`External-Repositories/CLAUDE.md`**: deleted session 6 — was a misleading 1-line empty file

## Notes

- Driven by an `/insights` report covering 51 sessions; main findings were first-attempt code bugs, deploy/env config failures, and scope overreach (implementing when only a plan was requested) — the Planning vs Implementation rule above is the direct fix for the last one.
- Remaining open items from that audit: GitHub MCP server setup (see `[[mcp-servers-in-use]]`), PostToolUse lint hooks (user wants explanation before implementing — recommended as per-repo project-level `.claude/settings.json` since lint commands differ), boilerplate intro-line cleanup across project CLAUDE.mds (deferred).
