---
title: "repo-state skill — fetch-before-clean git status workflow"
type: reference
domain: claude-workflow
status: draft
created: 2026-06-30
updated: 2026-06-30
tags:
  - claude-workflow/skills
source: ""
source_url: ""
---

# repo-state skill

Custom Claude Code skill at `~/.claude/skills/repo-state/SKILL.md` (global, not vault-scoped — applies in any repo). Built in response to an `/insights` usage report that surfaced a recurring failure: repo state reported as "clean" without checking the remote first.

## Workflow

1. `git fetch` (always first)
2. `gh pr list`
3. Branch status vs. remote
4. Last 5 commits
5. Summary paragraph

Hard rule: never say "clean" or "up to date" until the remote has actually been fetched. This is also codified directly in `~/.claude/CLAUDE.md` under **Repo State**.

## Notes

- **Status: untested as of 2026-06-30 (session 6).** Built session 5, not yet run against a real repo. Run `/repo-state` in a non-vault repo to verify the fetch-first behavior before trusting it.
- Invoke via `/repo-state`.
