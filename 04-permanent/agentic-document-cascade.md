---
title: Document cascade from roadmap to CLAUDE.md keeps decisions, plans, and
  implementation detail at separate layers
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

Coding projects follow a five-layer document cascade, split across two phases and (for research projects) two tools. **DECIDE phase** (Roadmap, Manifesto) is human-facing planning with no repo context — for research projects this runs in a separate Claude.ai Project, not Claude Code. **BUILD phase** (SPEC, design, CLAUDE.md) is agent-facing and runs in Claude Code with full repo context. The manifesto is the handoff artifact: written to stand alone so Claude Code can inherit from it without ever seeing the roadmap.

Non-research / already-decided projects can skip straight to a manifesto — the roadmap layer exists specifically because **research can't be planned linearly**: each next step depends on the last experiment's outcome. Stuffing one manifesto with conditional "if X then module Y" branches was the old failure mode (hard for humans and agents alike). The fix: separate *deciding what to build* (roadmap) from *specifying what to build* (manifesto) — a manifesto is therefore always unconditional, a complete buildable plan for one already-chosen path.

## The Five Layers

### 0. ROADMAP.md (DECIDE phase, new layer)
Living, human-facing meta-plan — the plan for *deciding* the project plan. Never feeds the agent cascade directly; only the manifesto does. Sections: purpose (one line); invariant vision & boundaries (true across every branch); cross-branch glossary; research-phase exit conditions (executable — when to stop deciding and lock a manifesto); **decision tree** (assumption-anchored — each node has an ID, the assumption under test, a link to an experiment card, a decision rule with measurement+threshold, a small discrete outcome set each routing to a next node or terminal stub, kill criteria, and status); experiment cards (one per experiment, runnable without conversation context: method, runnable check, timebox/cost, kill criteria, where it runs, proof-of-result outputs); manifesto stubs (one paragraph per terminal branch, fields aligned to the manifesto skeleton, enough to judge go/no-go); experiment log (dated, **append-only** — corrections are appended, never edited); status/current frontier.

Research-specific principles carried by this layer: pre-register each experiment's pass/fail threshold *before* it runs; one experiment tests one assumption; sequence by information value (cheapest + most-pruning, or riskiest-and-most-catastrophic-if-false, first); elaborate the tree lazily (only the active frontier gets fully specified; deeper branches stay one-liners); commit kill criteria that abandon a branch outright, defeating sunk-cost continuation; experiments are throwaway spikes by default — capture what was *learned*, not the code.

### 1. Manifesto
High-level, human-facing. The *why*, the scope boundaries, the invariants, and the module map for **one already-chosen branch**. Single source of truth that all downstream documents inherit from; never conditional.

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

**Handoff additions** (when a manifesto crosses from a roadmap into the repo): be self-contained — carry the relevant invariants, glossary terms, and defining constraint down from the roadmap verbatim, since Claude Code never sees the roadmap; record provenance — which branch, and which experiment IDs justify the key decisions; end with an **implied-SPEC index** (name + one-line scope per SPEC this manifesto implies) — Claude Code's starting point. Never write the SPECs themselves at this layer.

Done-check: a fresh reader can list the modules they'd build and the rules every module must follow *without guessing*.

### 2. SPEC.md (one per module, BUILD phase)
Technical and exhaustive, written *for an agent*. Takes one slice of the manifesto and makes it precise. Contains the implementation detail that would make a manifesto too long.

### 3. design.md (one per SPEC, BUILD phase)
Turns a SPEC into a concrete implementation plan in that module's named tech stack.

### 4. CLAUDE.md (one per folder, BUILD phase)
Lean ambient context for Claude Code. Pointers and invariants, never the specs themselves. Every line costs attention — keep it minimal. Contains "nouns" (where things are, commands, conventions, hard rules).

## Principles (apply at every layer)

- **Stable at root, volatile at leaves.** Durable stuff (purpose, invariants, vocabulary) belongs in the roadmap/manifesto. Implementation detail that will drift belongs in specs/designs. If a manifesto is getting long and implementation-flavored, move that detail down.
- **Inherited-by-all or owned-by-one.** Things that must stay consistent everywhere go at the root. Module-specific things name their module.
- **Success criteria must be executable.** Definitions of done should map to a test or runnable check, not a vibe. Pre-registered in the roadmap/manifesto, fully fleshed out in specs.
- **State constraints as imperatives.** "Never X," "Always Y" — not soft suggestions.
- **Name things once.** One glossary, reused identically from roadmap through every branch manifesto to code.
- **Carve at natural joints.** Each module = a coherent task one agent can complete in one focused session.

## Connections

[[rv-prediction]] — first project to produce a manifesto through this cascade (RV-pred Claude.ai Project → `MANIFESTO.md`, now locked, build phase starting in Claude Code)

## Sources

`C:\Users\strid\Downloads\project-instructions.md` (system prompt for the "Research Roadmaps & Manifestos" Claude.ai Project — the DECIDE-phase tool) · `C:\Users\strid\Desktop\Prompts\Class\RV-pred\MANIFESTO.md` (worked example of the manifesto layer)
