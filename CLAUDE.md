# Research Vault — Standing Instructions

last-updated: 2026-06-30

You are operating inside Strider Settgast's research knowledge base. This is a multi-domain research vault. Your role is to retrieve, write, and maintain notes as instructed. Do not reorganize structure without explicit instruction.

The vault is a retrieval substrate — value comes from continuity and note quality, not from reasoning harder. Every note you write should be worth retrieving in a future session.

---

## Folder Structure

| Folder | Purpose | Notes |
|---|---|---|
| `00-inbox/` | Unprocessed captures awaiting triage | Write here freely; never auto-file out |
| `01-projects/` | Active research with a defined deliverable | One subfolder per project |
| `02-areas/` | Ongoing research domains (no end date) | One subfolder per domain, added as needed |
| `03-resources/` | Source material: papers, books, clippings | Organized by source type |
| `04-permanent/` | Atomic concept notes — one idea per file | Primary retrieval target |
| `05-mocs/` | Maps of Content — domain index files | Read these first to orient on a domain |
| `07-archive/` | Completed projects, deprecated notes | Excluded from active search; do not modify |
| `99-meta/` | Templates, scripts, index files, this file | Not content — not subject to search |

---

## Frontmatter Schema

Every note you create or edit must have this frontmatter. The values for `type`, `status` are closed enumerations — do not invent new values. `domain` must match the kebab-case subfolder name under `02-areas/` (or be `general` if no domain folder exists yet).

```yaml
---
title: "Full descriptive title as a phrase or declarative claim"
type: permanent          # permanent | literature | moc | capture | project | area | reference
domain: <kebab-slug>     # kebab-case: e.g., physics, machine-learning, mathematics
status: active           # active | draft | archived | evergreen
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags:
  - domain/subtopic      # slash-hierarchical only, e.g. ml/attention, physics/mhd
source: ""               # literature notes only: "Author(s), Year, Title"
source_url: ""           # literature notes only
---
```

---

## File Naming Conventions

| Note type | Convention | Example |
|---|---|---|
| Permanent/concept | `concept-slug.md` (no date) | `transformer-attention-mechanism.md` |
| Literature note | `author-year-short-title.md` | `vaswani-2017-attention-all-you-need.md` |
| MOC | `domain-name-moc.md` | `machine-learning-moc.md` |
| Capture/inbox | `YYYYMMDD-brief-slug.md` | `20260629-mhd-scaling-idea.md` |
| Project note | `project-name.md` inside `01-projects/project-name/` | |
| Reference | `resource-slug.md` | `code-repositories-map.md` |

Rules: lowercase, hyphens only, no spaces, no special characters.

---

## Session Orientation Protocol

At the start of every session, in this order:
1. Read `99-meta/hot.md` — recent context: what was worked on last session
2. Read `99-meta/active-projects.md` — open projects and their current state
3. If asked about a specific domain, read the relevant MOC in `05-mocs/` before reading individual permanent notes
4. Do NOT read the entire vault on startup — use the index to navigate

---

## Note Structure

**Permanent notes** (`04-permanent/`):
- Title in frontmatter is a declarative claim: "Attention mechanisms encode relative positional importance between tokens" — not just "Attention"
- Opening paragraph stands alone — it will often be the only chunk retrieved
- Use H2 sections when the note exceeds ~400 words:
  ```
  ## Mechanism
  ## Evidence      ← wikilinks to literature notes as [[author-year-title]]
  ## Connections   ← wikilinks to related permanent notes
  ## Open Questions
  ```

**Literature notes** (`03-resources/`):
- Frontmatter: full `source` and `source_url` fields
- Required sections: `## Key Quotes` (verbatim with page/section reference), `## My Summary` (in your own words), `## Connections`

**Reference notes** (`03-resources/`):
- For durable reference material that is not a citable source: maps, API docs, configuration guides, inventories
- No required sections — structure to the content; a `## Notes` section for annotations is conventional
- File naming: `resource-slug.md` (no date prefix)

**MOC files** (`05-mocs/`):
- Organized wikilink lists only — no prose analysis
- H2 sections by subtopic, each with `[[note-slug|Brief annotation]]` lines
- One MOC per research domain

---

## Writing Rules

- Search the vault before creating a new note — use `search_notes` first
- Write atomically: one concept or one source per file
- Prefer `patch_note` to update an existing note over creating a new one when content overlaps
- Leave anything uncertain at `status: draft`
- Use `[[wikilinks]]` for all internal cross-references; never use file paths
- Do not write speculative connections as wikilinks — only link notes that actually exist

---

## Inbox Processing Rules

- AI may write to `00-inbox/` freely during a session
- AI must NEVER auto-file a note out of `00-inbox/` — always present the filing decision to the user first
- When processing inbox on instruction: read the note, assign frontmatter fields, suggest destination and filename, wait for user confirmation before moving

---

## Constraints — Read Carefully

- Do NOT create new folders without explicit instruction
- Do NOT rename existing files (slugs are permanent identifiers once linked)
- Do NOT restructure the folder hierarchy
- Do NOT modify notes in `07-archive/` unless explicitly asked
- Do NOT add frontmatter fields not listed in the schema above
- Do NOT write to `99-meta/` except to update `hot.md`, `active-projects.md`, or `vault-index.md` as specified below

---

## Index Maintenance

Update these files as instructed or at end of session:

**`99-meta/hot.md`** — update at end of every session with ~500-word summary: what was worked on, what was learned, what is unresolved. This is the primary continuity mechanism for the next session.

**`99-meta/active-projects.md`** — update when a project is opened, advanced, or closed.

**`99-meta/vault-index.md`** — update when a new permanent note or MOC is added. One row per note: filename, title, domain, one-line summary.

---

## Domain Map

Update this table when a new domain is added to `02-areas/`.

| Domain slug | Description | MOC file |
|---|---|---|
| (none yet — add as first notes are filed) | | |

---

## Workflow Reference

Three recurring loops:

**Capture** — dump anything into `00-inbox/` without deciding where it belongs. Use the capture template (`99-meta/templates/capture.md`).

**Work** — per-session: search the vault for relevant context, pressure-test claims, write findings back to `04-permanent/` or update existing notes. Update `hot.md` at end.

**Review** — periodic (weekly): process all `00-inbox/` notes, update MOCs, prune `status: draft` notes that aren't progressing, move completed projects to `07-archive/`.
