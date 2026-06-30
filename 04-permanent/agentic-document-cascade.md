---
title: Document cascade from manifesto to CLAUDE.md keeps stable invariants at
  root and volatile details at leaves
type: permanent
domain: general
status: evergreen
created: 2026-06-30
updated: 2026-06-30
tags:
  - meta/workflow
  - meta/agentic-projects
---

# Agentic Project Pipeline — Document Cascade

All coding projects follow a four-layer document cascade, from most-human to most-technical. Each layer feeds the next. An AI coding agent (Claude Code) builds from the specs/designs; the manifesto is primarily for the human.

## The Four Layers

### 1. Manifesto
High-level, human-facing. The *why*, the scope boundaries, the invariants, and the module map. Single source of truth that all downstream documents inherit from.

Required sections (in order of importance):
- Purpose & the problem it solves
- Core users & concrete use cases
- Project-level measurable success criteria
- Scope boundaries with **explicit non-goals**
- **Capability/module map** — one-line responsibility per module, what it owns vs. doesn't, dependency direction
- **Cross-cutting invariants & principles** (stated as imperatives: "Never X", "Always Y")
- Key decisions with rationale + open questions
- Glossary
- Global tech stack only

Done-check: a fresh reader can list the modules they'd build and the rules every module must follow *without guessing*.

### 2. SPEC.md (one per module)
Technical and exhaustive, written *for an agent*. Takes one slice of the manifesto and makes it precise. Contains the implementation detail that would make a manifesto too long.

### 3. design.md (one per SPEC)
Turns a SPEC into a concrete implementation plan in that module's named tech stack.

### 4. CLAUDE.md (one per folder)
Lean ambient context for Claude Code. Pointers and invariants, never the specs themselves. Every line costs attention — keep it minimal. Contains "nouns" (where things are, commands, conventions, hard rules).

## Principles

- **Stable at root, volatile at leaves.** Durable stuff (purpose, invariants, vocabulary) belongs in the manifesto. Implementation detail that will drift belongs in specs/designs. If a manifesto is getting long and implementation-flavored, move that detail down.
- **Inherited-by-all or owned-by-one.** Things that must stay consistent everywhere go at the root. Module-specific things name their module.
- **Success criteria must be executable.** Definitions of done should map to a test or runnable check, not a vibe. Planned in the manifesto, flushed out in specs.
- **State constraints as imperatives.** "Never X," "Always Y" — not soft suggestions.
- **Name things once.** Use the manifesto glossary consistently from manifesto to code.
- **Carve at natural joints.** Each module = a coherent task one agent can complete in one focused session.

