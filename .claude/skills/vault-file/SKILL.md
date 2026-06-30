---
name: vault-file
description: File an inbox note into the vault. Use when the user asks to file, process, or triage a note from 00-inbox, or when asked to suggest where a note should go. Always stops for user confirmation before moving anything.
---

# Vault File

File a note from `00-inbox/` into its permanent home. Follow the schema and naming conventions in CLAUDE.md exactly — do not reproduce them here.

## Workflow

1. **Read the note** — read the inbox note in full.

2. **Search for duplicates** — run `search_notes` with 2-3 keywords from the content. If a closely related permanent note exists, flag it: filing may mean updating that note instead of creating a new one.

3. **Propose frontmatter** — draft complete frontmatter (all required fields from the schema). State your reasoning for `type`, `domain`, and `tags` in one sentence each.

4. **Propose destination** — state the target folder and filename following the naming conventions in CLAUDE.md. Explain why.

5. **STOP** — present the proposal to the user and wait for confirmation. Do not move, rename, or write anything until the user explicitly confirms.

6. **Execute on confirmation** — once confirmed:
   - Update the note's frontmatter in place (`patch_note` or `update_frontmatter`)
   - Move the note to the confirmed destination (`move_note`)
   - Report what was done

**Hard rule:** Never call `move_note` before the user confirms. If uncertain about `type` or `domain`, say so and offer options — do not guess silently.