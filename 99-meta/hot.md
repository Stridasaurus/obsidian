---
title: Recent Context Cache
type: meta
updated: 2026-06-30
---

# Recent Context Cache

**Last updated:** 2026-06-30 (session 7)

## What was done (session 8 — 2026-06-30)

### Domain taxonomy decisions + proactive permanent-note flagging + CLAUDE.md hierarchy rule

Entirely meta/infrastructure session — no research content written. Triggered by the user asking whether neuroscience and finance should get MOCs like machine-learning and space-physics already have.

**Neuroscience/finance MOCs: held off.** Checked the vault — there is only **one permanent note in the entire vault** (`agentic-document-cascade.md`). MOCs index permanent notes; creating MOCs for domains with zero permanent-note content would just be empty scaffolding. Decision: wait until neural-gibf (neuroscience) and rv-prediction (finance/ML) actually produce extractable permanent notes, which should happen soon given they're top-priority active projects.

**Domain slug decisions made:**
- `neural-gibf-proposal.md`: `domain: computational-neuroscience` → `neuroscience` (shorter, doesn't preclude computational work later — user's reasoning, agreed)
- `rv-prediction.md`: churned `machine-learning` → `finance` → reverted to `machine-learning`. Landed on a principle: `domain` (singular field, drives MOC filing) should reflect the *primary axis of contribution/methodology*; secondary axes are already captured via slash-hierarchical `tags` (this note already had both `machine-learning/time-series` and `finance/volatility` tagged). Since RV-prediction is "an ML project using finance as a medium" (user's framing), domain = machine-learning is correct.

**Vault self-assessment given on request.** Structurally well-suited to me as reader (schema, mandatory Constraints & Invariants section, hot.md/active-projects.md continuity files) but badly underpopulated — only 1 permanent note, empty inbox, sparse MOCs. Walked the user through the automatic vs. manual halves of the system: hot.md read/write is automatic (session-start read, "wrap up" trigger to write); 00-inbox capture and 04-permanent extraction are NOT automatic and weren't being used.

**New standing behavior adopted.** User asked me to proactively flag durable/atomic concepts as permanent-note candidates during project work rather than waiting to be asked. Added as a one-line rule under "Obsidian Research Vault" in `~/.claude/CLAUDE.md` (kept deliberately terse after user feedback that the first draft was too verbose for a global file).

**Tag cleanup.** User asked for a state-of-the-system report, which surfaced two real inconsistencies: `ml/*` vs `machine-learning/*` tag prefixes used for the same concept (`machine-learning-moc.md` had the former), and a stale `computational-neuroscience/source-localization` tag left over after the domain rename above. Fixed both — tags now consistently use the full domain slug as the top-level segment. (Stray-looking tags like `tag`, `nested/tag` etc. were a false alarm — they're example syntax inside the `obsidian-markdown` skill's own reference docs, not vault content.) Note: a `merge: false` call on `machine-learning-moc.md`'s frontmatter briefly wiped its title/type/domain/status fields — caught immediately via read-back and restored; worth remembering `update_frontmatter` needs `merge: true` (default) unless a full replace is actually intended.

**New vault rule added** to `CLAUDE.md` Writing Rules: tag top-level segment must exactly match an existing `domain` slug — prevents the `ml/` vs `machine-learning/` drift from recurring.

**CLAUDE.md hierarchy leanness principle added globally.** User has noticed CLAUDE.md files I write tend to be too verbose. Added a short "CLAUDE.md Leanness" section to the top of `~/.claude/CLAUDE.md`: leanness strictness increases with scope — global is leanest, repo-level looser, subdirectory loosest — while every level should still convey what it needs.

### Unresolved / next steps

- **`04-permanent/` is still the main gap** — only 1 note vault-wide. Should start filling in naturally now that proactive flagging is active, but worth checking back on.
- **Neuroscience/finance MOCs** — revisit once each domain has a few permanent notes worth indexing.
- **RV Prediction + CT essay** (top 2 priorities, due ~2026-07-07) — still no actual research work started; this session and session 7 were both pure meta/organizational work.
- **Uncommitted changes**: vault has frontmatter edits across several notes plus the vault `CLAUDE.md` edit; `~/.claude/CLAUDE.md` also edited (not git-tracked, lives outside repos).
- Carried over unchanged: `repo-state` skill still untested, GitHub MCP still unverified, research backlog (`secs-elementary-current-system.md`, `fukushima-theorem.md`, `gibf-beamforming-core.md`, 4 literature notes) unwritten.

---

## What was done (session 7 — 2026-06-30)

### Project prioritization + new claude-workflow area

**Priority ranking captured.** User stated priority order across active projects: 1) Realized Volatility Prediction, 2) a category-theory/differential-geometry course essay (both due ~2026-07-07), 3) SECS-GIBF Viability (mag-GIBF, career move), 4) Dynamica (already started, unfinished work looks bad), 5) Neural-GIBF/MEG (not yet started). Clarified with the user that the CT essay is a **separate** project from the math-blog brainstorm, not the same thing — but it's an explicit precursor: the user won't start the blog until the essay is done and expects the essay's material to roll directly into Post 1 ("Sets vs. Categories") and/or the duality posts (5a/5b).

**New project created:** `01-projects/category-theory-diffgeo-essay/category-theory-diffgeo-essay.md` — status in-progress, due ~2026-07-07, notes the math-blog dependency.

**`99-meta/active-projects.md` restructured** with explicit numbered priority order and due dates; math-blog reframed as "gated on #2" rather than independently ranked. **`99-meta/vault-index.md`** projects table updated to match. Saved persistent memory `project_priority_2026q3.md` so future sessions open already knowing this order.

**New `02-areas/claude-workflow/` domain added**, on user request ("I want to be organized about how I use Claude"). This is an ongoing practice domain (no deliverable/end date) for CLAUDE.md hierarchy, custom skills, MCP servers, and configuration — deliberately placed in `02-areas/` rather than `01-projects/` since it never "completes." Created:
- `02-areas/claude-workflow/claude-workflow.md` — area note (scope: CLAUDE.md hierarchy, skills, MCP servers, hooks, recurring conventions)
- `05-mocs/claude-workflow-moc.md` — MOC
- Registered the new `claude-workflow` domain in the vault's own `CLAUDE.md` Domain Map table

**Backfilled history from past sessions' narrative into atomic reference notes** (previously this content only existed as prose in this file). Five new notes in `03-resources/`, domain `claude-workflow`:
- `skill-vault-file.md` — tested working, status active
- `skill-repo-state.md` — **still untested**, status draft
- `skills-kepano-obsidian.md` — the 5-skill third-party install
- `claude-md-hierarchy.md` — current contents of all 5 CLAUDE.md tiers, links to `[[agentic-document-cascade]]` as the general pattern this is an instance of
- `mcp-servers-in-use.md` — Obsidian MCP (active) + GitHub MCP (**still untested**, status draft)

MOC and `vault-index.md` updated to point to these real notes instead of `*(stub)*` placeholders.

**Inbox checked — empty.** Only `.gitkeep` present; the two stale daily notes referenced in old session logs (`20260629-daily.md`, `20260630-daily.md`) don't actually exist on disk, confirming the prior session's finding. Nothing to triage this session.

### Unresolved / next steps

- **`repo-state` skill still untested** — run `/repo-state` in a non-vault repo to verify fetch-first behavior
- **GitHub MCP still untested** — restart Claude Code, confirm GitHub tools appear in `/context`
- **RV Prediction + CT essay** (priorities 1–2) need actual work started — due ~2026-07-07, nothing done yet this session beyond tracking
- **Research backlog unchanged (longstanding, still highest content priority once course deadlines clear):** `secs-elementary-current-system.md`, `fukushima-theorem.md`, `gibf-beamforming-core.md` still unwritten; literature notes for Suzuki 2011, Vanhamäki & Juusola 2020, Wax & Kailath 1985, Fukushima 1976 still pending
- Vault has uncommitted changes from this session (active-projects.md, vault-index.md, CLAUDE.md, new project/area/MOC/reference notes) — not yet committed/pushed

---

## What was done (session 6 — 2026-06-30)

### CLAUDE.md audit and improvements

Reviewed and improved the CLAUDE.md hierarchy across the whole environment, prompted by the `/insights` usage report from this two-week window.

**Structure understood:** Three-tier hierarchy — `~/.claude/CLAUDE.md` (global, every session), `Code-Repositories/CLAUDE.md` (all repos), folder-level files (`Python/`, `Sites/`), then individual project files. The `Code-Repositories/`, `Python/`, `Sites/`, and `~/.claude/` CLAUDE.mds are **not in any git repo** — they live outside tracked directories.

**Changes made:**

`~/.claude/CLAUDE.md` — added three sections:
- **Environment:** Windows 11 / PowerShell rule (no Bash heredoc syntax)
- **Planning vs Implementation:** plan-only discipline — do not implement until explicitly told to proceed
- **Repo State:** never report clean until `git fetch` + `gh pr list`; reference `/repo-state` skill

`Code-Repositories/CLAUDE.md` — added **New repo setup** sequence: clone → install → test → .gitignore → CLAUDE.md (after pulling). Confirm remote file existence before deleting locally.

`Sites/CLAUDE.md` (new file) — created with two sections:
- **Stack & Deploy target:** defers to each project's CLAUDE.md; check `.github/workflows/` for CI config. Kept tech-agnostic intentionally (may use more than Vite/React in future).
- **Deployment & Verification:** DOM queries (not screenshots), check base paths, smoke test before declaring done.

`Python/CLAUDE.md` — added **Coding standards** section: ruff format, ruff check, type hints best effort on public function signatures (skip notebook cells), NumPy docstrings for public API only.

`lab-notebooks/CLAUDE.md` — added **What this is** section: "Low-stakes space for notebooks and experiments before they are formalized into proper documentation or migrated to main projects." This is the only changed file in a tracked git repo — committed and pushed.

`External-Repositories/CLAUDE.md` — deleted (was a 1-line empty file; misleading).

**Python coding standards decision:**
- ruff format + ruff check (user's choice)
- Type hints: best effort — annotate public function signatures in installable packages; skip in notebook cells (recommended given mixed research/notebook codebase)
- Docstrings: public API only, NumPy format (standard for scientific Python)

**Remaining from report (still open):**
- GitHub MCP server (`claude mcp add github -- npx -y @modelcontextprotocol/server-github`) — needs GITHUB_PERSONAL_ACCESS_TOKEN in Windows user env vars first
- Hooks (PostToolUse lint) — user wants explanation before implementing; recommended as project-level `.claude/settings.json` per repo since lint commands differ
- Boilerplate intro line cleanup across project CLAUDE.mds — deferred to next session

---

## What was done (session 6 — 2026-06-30)

### vault-file skill verified; math blog project registered; GitHub MCP added

**vault-file skill tested and confirmed working.** The two stale daily notes from hot.md (`20260629-daily.md`, `20260630-daily.md`) turned out not to exist on disk — they were phantom references written as if the Daily Notes plugin had created them, but it only fires from the Obsidian UI. Instead, a real capture was used as the test: the math blog brainstorm from `C:\Users\strid\Desktop\Prompts\Personal\Blogprop1.md`.

The vault-file workflow ran correctly end-to-end:
1. Wrote capture to `00-inbox/20260630-blog-proposal.md`
2. Searched for duplicates (none found)
3. Proposed frontmatter (`type: project`, `domain: general`, tags `writing/blog`, `mathematics/category-theory`, `mathematics/duality`) and destination (`01-projects/math-blog/math-blog.md`)
4. Stopped and waited for user confirmation — hard rule enforced correctly
5. On confirmation: updated frontmatter in place, moved note, created `math-blog/` project folder

**Math blog registered as active project.** `vault-index.md` and `active-projects.md` both updated. The blog is a 10-post series using categorical duality as the unifying thread, running from pure math foundations (category theory, tensors, measurement, duality) through applied interdisciplinary science (Fourier/beamforming, stochastic processes, learning). Post 7 (GIBF) is the signature applied piece. Status: `draft`. Next action: choose writing platform, flesh out Post 1 outline.

**GitHub MCP server added globally.** `@modelcontextprotocol/server-github` registered at `--scope user` with `GITHUB_PERSONAL_ACCESS_TOKEN` env var. Will be available in all repos after restarting Claude Code. Token set with 90-day expiration.

### Unresolved / next steps

- **Test GitHub MCP:** restart Claude Code and verify GitHub tools appear in `/context`
- **Test `repo-state`:** still untested; run `/repo-state` in any non-vault repo
- **Research backlog (unchanged, highest priority):** `secs-elementary-current-system.md`, `fukushima-theorem.md`, `gibf-beamforming-core.md` still unwritten — source PDFs on disk
- **Literature notes** for Suzuki 2011, Vanhamäki & Juusola 2020, Wax & Kailath 1985, Fukushima 1976 still pending
- **Active projects** next actions unchanged from session 5

---

## What was done (session 5 — 2026-06-30)

### Claude Code tooling upgraded: kepano skills + custom skills

This session was entirely meta — no research content. Prompted by running `/insights`, which surfaced a usage report across 51 sessions. The report's key findings shaped the work done.

**Insights report summary (for reference in future sessions):**
- Best-working setup: Obsidian vault via MCP as a "second brain" — the continuity mechanism is working
- Main friction: first-attempt code bugs, deploy/env config failures, scope overreach (implementing when only a plan was asked for)
- Quick wins identified: Custom Skills for recurring routines, Hooks for pre-flight git sync

**kepano/obsidian-skills installed.** Cloned `kepano/obsidian-skills` and copied its contents into `obsidian/.claude/` (the vault's Claude config directory). Five skills now live in `obsidian/.claude/skills/`:
- `obsidian-markdown` — correct Obsidian-flavored syntax (wikilinks, callouts, properties) without needing to describe it each session
- `obsidian-bases` — Obsidian Bases file creation/editing
- `json-canvas` — JSON Canvas files
- `obsidian-cli` — Obsidian CLI interaction
- `defuddle` — **most immediately useful**: strips web page clutter to clean markdown before writing to vault, saving tokens on web captures

These will appear in `/context` after restarting Claude Code in the vault session (they require the opening `---` frontmatter delimiter to be present in each SKILL.md — user verified this was added).

**Two custom skills written (not yet confirmed loading):**

`vault-file` — in `obsidian/.claude/skills/vault-file/SKILL.md`. Workflow: read inbox note → search vault for duplicates → propose complete frontmatter → propose destination + filename → **STOP and wait for user confirmation** → move on confirmation only. Hard rule: never call `move_note` before user confirms. This encodes the vault CLAUDE.md constraint ("AI must NEVER auto-file a note out of 00-inbox").

`repo-state` — in `~/.claude/skills/repo-state/SKILL.md` (global, not project-scoped). Workflow: `git fetch` first → `gh pr list` → branch status → last 5 commits → summary paragraph. Hard rule: never say "clean" until remote has been fetched. This prevents the recurring issue from the insights report where stale repo state was reported as clean.

**Four tools evaluated for integration:**
1. `kepano/obsidian-skills` → installed (above)
2. `karpathy/autoresearch` → skipped; requires NVIDIA GPU, is for ML training research, not applicable to this domain
3. `anthropics/skill-creator` → used its methodology (draft-first iteration) to write the custom skills; the full eval loop is overkill for personal skills but the draft → describe → test pattern was followed
4. `teng-lin/notebooklm-py` → deferred for user to explore; most relevant angle is Obsidian sync + zero-token research offload (throw IBF/SECS papers into NotebookLM, let Gemini do analysis, Claude does synthesis). Risk: unofficial Google API, can break.

### Unresolved / next steps

- **Verify skills load**: start a fresh Claude Code session in the vault directory, run `/context all`, confirm `vault-file`, `repo-state`, and the 5 kepano skills appear in the Skills section. If missing, check that each SKILL.md has `---` as its very first line.
- **Try `vault-file`**: there are two stale daily notes in `00-inbox` (`20260629-daily.md`, `20260630-daily.md`) — use `/vault-file` to process them as a first test
- **Try `repo-state`**: run `/repo-state` in any non-vault repo before starting work to verify the fetch-first behavior
- **Research backlog unchanged**: `secs-elementary-current-system.md`, `fukushima-theorem.md`, `gibf-beamforming-core.md` still unwritten; literature notes for Suzuki 2011, Vanhamäki & Juusola 2020, Wax & Kailath 1985, Fukushima 1976 still pending
- **notebooklm-py**: user was going to explore this independently; potentially useful for batch-analyzing IBF_Project PDFs

---

## What was done (session 4 — 2026-06-30)

### Vault optimized for Claude-as-reader; MOC stubs created

**Committed and pushed sessions 2–3 work.** All infrastructure changes (Templater, Dataview, Daily Notes config, template fixes, local-library.md, schema update) were staged and pushed to remote as a single commit.

**Created stub MOCs.** `05-mocs/space-physics-moc.md` and `05-mocs/machine-learning-moc.md` — both contain H2-sectioned wikilink lists for the relevant backlog notes, annotated with `*(stub)*` where the target note doesn't exist yet. Vault-index.md updated to reflect both.

**Redesigned permanent note structure for Claude-as-reader.** Key realization: this vault is written entirely for Claude, not for human reading. This changes the design significantly — the reader is a fresh Claude session with no prior context, not a human with progressive understanding. Changes made:

- **CLAUDE.md** — old four-section structure (Mechanism / Evidence / Connections / Open Questions) replaced with five sections:
  - `## Formulation` — equations inline, all notation defined here
  - `## Constraints & Invariants` — non-obvious things Claude must not violate; failure modes; things that look plausible but are wrong. Flagged as the highest-value section of any permanent note.
  - `## Connections` — wikilinks to chain-read
  - `## Open Questions` — what's unresolved
  - `## Sources` — pointer to lit note and/or PDF path for verification before building on the note
- Added rule: natural-language concept names must appear beside any LaTeX notation — `search_notes` is plain keyword search, so `\nabla\times\mathbf{J}` won't match a query for "curl of current density"
- Added rule: in MOCs, planned notes may be listed with `*(stub)*` suffix as TODOs; in permanent notes, only link notes that exist
- Default status in permanent template changed to `draft`

- **`99-meta/templates/permanent.md`** — updated to match the new five-section structure

### Key insight from advisor call
Retrieval is link-graph traversal, not just reading. The highest-leverage surface is discoverability: declarative title, tags, MOC annotation, and opening line. A perfectly dense note the MOC doesn't point to never gets loaded. Also confirmed: `search_notes` is plain keyword search returning file path + short excerpt — full note is retrieved separately with `read_note`. Sections do not need to be self-contained for chunking reasons, but LaTeX must be accompanied by natural-language names for keyword searchability.

## Unresolved / next steps

- **Item 5 (next):** Write first permanent notes from source PDFs — start with `secs-elementary-current-system.md`. Source: `Desktop\School\IBF_Project\SECS.pdf` and `Ionospheric SECS.pdf`. Read PDFs before writing — Constraints & Invariants section must come from source, not memory.
- **Item 5 continued:** `fukushima-theorem.md`, `gibf-beamforming-core.md`
- **Item 6:** Literature notes for Suzuki 2011, Vanhamäki & Juusola 2020, Wax & Kailath 1985, Fukushima 1976
- Neural-GIBF Week 1 still blocked on 4 open decisions
- SECS-GIBF: next action is building geometry + transfer modules

---

## What was done (session 3 — 2026-06-30)

### Local PDF library cataloged

Short session. The main action was registering a local PDF collection that already existed on the desktop into the vault and into Claude's persistent memory, so future sessions can reference it without re-deriving the paths.

Two folders cataloged:

**`C:\Users\strid\Desktop\School\IBF_Project\`** — five papers directly relevant to the active GIBF/SECS research projects: SECS.pdf, Ionospheric SECS.pdf, GIB.pdf, Suzuki GIBF.pdf, Elastic Net.pdf. These are the primary source documents for `01-projects/gibf/` and `01-projects/neural-gibf/`.

**`C:\Users\strid\Desktop\School\Textbooks\`** — broad collection spanning physics (Griffiths E&M 4th, Halliday & Resnick), quantum mechanics (Griffiths QM 3rd, Sakurai), mathematics (Nagle ODEs, Briggs Calculus, Fleisch Vectors & Tensors, Leinster Category Theory, Type Theory, Brown-Churchill Complex Variables, Bertsekas & Tsitsiklis Probability), finance (Shreve Stochastic Calculus I & II, Tsay Financial Time Series, Brealey-Myers-Allen Corporate Finance), neuroscience (Dayan & Abbott Theoretical Neuroscience, Churchland Neurophilosophy, Tononi Effective Information), and electronics (Eggleston Basic Electronics). Also contains CV.

### Notes created/updated
- **`03-resources/local-library.md`** — new reference note with a full table of every PDF, organized by domain
- **`99-meta/vault-index.md`** — added Resources section; bumped `updated` to 2026-06-30
- **Memory** — `reference_local_library.md` added to Claude's persistent memory so future sessions know where to look without being told

## Unresolved / next steps

- No research content written this session; same backlog as session 2
- IBF_Project papers are now accessible — good starting point for literature notes (Suzuki GIBF, SECS, Ionospheric SECS are the three most directly relevant to the open items below)
- **Item 4:** Create stub MOCs — `05-mocs/space-physics-moc.md` and `05-mocs/machine-learning-moc.md`
- **Item 5:** Write first permanent notes: `fukushima-theorem.md`, `secs-elementary-current-system.md`, `gibf-beamforming-core.md`
- **Item 6:** Literature notes for the 4 papers cited in SECS-GIBF: Suzuki 2011, Vanhamäki & Juusola 2020, Wax & Kailath 1985, Fukushima 1976 — source PDFs now on disk
- Neural-GIBF Week 1 still blocked on 4 open decisions
- Uncommitted git changes in vault (local-library.md, vault-index.md) — commit when next substantive session wraps

---

## Previous session (session 2 — 2026-06-30)

## What was done

This session was entirely infrastructure — no research content was written. The goal was to finish the three-plugin setup (Templater, Daily Notes, Dataview) that was started at the end of the previous session.

### Schema update
Added `reference` as a sixth note type to the frontmatter schema in `CLAUDE.md`. References live in `03-resources/`, use `resource-slug.md` naming (no date prefix), and have no required sections. This was motivated by `code-repositories-map.md`, which didn't fit any of the five existing types cleanly. The `type` enum in the schema is now: `permanent | literature | moc | capture | project | area | reference`.

### Template files fixed
All four template files in `99-meta/templates/` had `YYYY-MM-DD` as literal placeholder text for the `created` and `updated` frontmatter fields. These were patched to use Templater's auto-fill syntax: `<% tp.date.now("YYYY-MM-DD") %>`. The four templates updated: `permanent.md`, `capture.md`, `literature.md`, `moc.md`.

### Templater plugin configured
The community plugin Templater was installed and its template folder set to `99-meta/templates`. The "Trigger Templater on new file creation" option was left OFF to avoid auto-applying templates to every new file. Workflow for using templates: `Ctrl+N` (new note) → `Ctrl+P` → `Templater: Open Insert Template modal` → pick template → dates auto-fill.

### Daily Notes plugin configured
The core Daily Notes plugin was enabled and configured:
- **New file location:** `00-inbox` — daily notes now route into the inbox instead of vault root
- **Date format:** `YYYYMMDD-[daily]` — produces filenames like `20260630-daily.md`, matching the vault's capture naming convention

A Moment.js gotcha encountered: the literal string `daily` contains format tokens (`d` = day-of-week, `a` = am/pm, `l` = locale date, `y` = year), so the format `YYYYMMDD-daily` produced garbled output like `20260630-2ami6/30/20262026`. Fix: wrap literal text in square brackets → `YYYYMMDD-[daily]`.

### Dataview plugin
Installed and enabled. No configuration required for basic use.

## Current state of vault infrastructure

- Templates: fully functional with auto-fill dates
- Daily notes: routing correctly to `00-inbox`
- Dataview: ready for frontmatter queries
- All project notes have correct `type: project` frontmatter (fixed last session)
- The two stale daily notes (`20260629-daily.md`, `20260630-daily.md`) are sitting in `00-inbox` unprocessed — should be triaged or deleted at next review

## Unresolved / next steps

- **Item 4:** Create stub MOCs — `05-mocs/space-physics-moc.md` and `05-mocs/machine-learning-moc.md`
- **Item 5:** Write first permanent notes: `fukushima-theorem.md`, `secs-elementary-current-system.md`, `gibf-beamforming-core.md`
- **Item 6:** Literature notes for the 4 papers cited in SECS-GIBF: Suzuki 2011, Vanhamäki & Juusola 2020, Wax & Kailath 1985, Fukushima 1976
- Neural-GIBF Week 1 still blocked on 4 open decisions — resolve before scheduling build time
- No research content was added this session; the vault infrastructure is now ready for actual research work to begin
