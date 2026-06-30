---
title: "vault-file skill — inbox triage workflow with mandatory user confirmation"
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

# vault-file skill

Custom Claude Code skill at `obsidian/.claude/skills/vault-file/SKILL.md` (project-scoped to this vault). Encodes the vault's hard inbox rule: "AI must NEVER auto-file a note out of `00-inbox/`."

## Workflow

1. Read the inbox note
2. Search the vault (`search_notes`) for duplicates/overlapping content
3. Propose complete frontmatter (type, domain, status, tags)
4. Propose destination folder + filename
5. **Stop and wait for explicit user confirmation**
6. Only on confirmation: update frontmatter in place, then move the note

Hard rule: never call `move_note` before the user confirms.

## Notes

- Tested end-to-end 2026-06-30 (session 6) on the math-blog brainstorm capture (`20260630-blog-proposal.md` → `01-projects/math-blog/math-blog.md`); confirmation gate held correctly.
- Invoke via `/vault-file`.
