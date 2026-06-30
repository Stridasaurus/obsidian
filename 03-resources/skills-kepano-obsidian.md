---
title: "kepano/obsidian-skills — installed third-party skill pack"
type: reference
domain: claude-workflow
status: active
created: 2026-06-30
updated: 2026-06-30
tags:
  - claude-workflow/skills
source: ""
source_url: ""
---

# kepano/obsidian-skills

Cloned from `kepano/obsidian-skills` and installed into `obsidian/.claude/skills/` (vault-scoped). Five skills, installed 2026-06-30 (session 5):

- **obsidian-markdown** — correct Obsidian-flavored syntax (wikilinks, callouts, properties) without re-describing it each session
- **obsidian-bases** — create/edit Obsidian Bases files
- **json-canvas** — create/edit JSON Canvas files
- **obsidian-cli** — interact with Obsidian via its CLI
- **defuddle** — strips web page clutter to clean markdown before writing to vault; most immediately useful for web captures (saves tokens vs. raw `WebFetch`)

## Notes

- Each `SKILL.md` requires `---` as the literal first line (frontmatter delimiter) or it won't be picked up — this tripped the install initially.
- Verify these still appear under `/context all` if skill loading behavior ever seems off.
