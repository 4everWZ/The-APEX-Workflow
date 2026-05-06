# Documentation Topology

Code and documentation must not silently drift.

## 1. When Documentation Updates Are Mandatory

Documentation updates are mandatory when changes affect:
- architecture
- behavior
- usage
- evaluation semantics
- external contracts
- reproducibility
- maintainability

## 2. Update Rules by Tier

### Tier A
Documentation updates are generally required.

### Tier B
Update docs when:
- interfaces change
- new config keys or flags are introduced
- behavior changes are user-visible
- the implementation adds a non-obvious constraint
- architecture or evaluation semantics change

### Tier C
Documentation updates are usually unnecessary unless the change crosses a behavior, architecture, or contract boundary.

## 3. Repository Layout Assumption

When formal spec evolution is required, maintain a flat fixed-anchor topology:

- `docs/specs/00_*.md` — overview and top-level decomposition
- `docs/specs/algo_*.md` — one per major algorithm or research module
- `docs/specs/dev_*.md` — one per integration or system component
- `docs/specs/integration_*.md` — end-to-end assembly and validation checklist
- `docs/specs/status_*.md` — current-state snapshots and handoff notes for accepted Tier A work and substantial accepted Tier B work
- `docs/specs/legacy/` — superseded specifications
- `docs/design/` — global architecture, system framework, or overall network structure docs
- `docs/matrix_*.md` — spec-to-implementation matrix
- `docs/tradeoffs.md` — approved or unavoidable project-level deviations

Move the original pre-implementation spec to `docs/specs/legacy/` when it is superseded by formalized active documentation.

## 4. Required Anchor Documents

### 4.1 Overview
`00_*.md` must contain:

- project purpose
- scope and explicit non-goals
- primary success criteria
- top-level decomposition
- links to relevant docs

### 4.2 Algorithm Leaf Docs
Each `algo_*.md` must contain:
1. Goals & Boundaries
2. Math / Logic / Interfaces
3. Code Mapping
4. Tradeoffs
5. Verification

Use these for major model blocks, losses, data semantics, evaluation protocols, or research modules.

### 4.3 Development Leaf Docs
Each `dev_*.md` must contain:
1. Goals & Boundaries
2. Interfaces / Responsibilities
3. Code Mapping
4. Tradeoffs
5. Verification

Use these for service components, integration boundaries, state ownership, or operational subsystems.

### 4.4 Tradeoff Layering Rule

Tradeoffs are intentionally split across two layers.

**Leaf-doc tradeoffs (`algo_*.md` / `dev_*.md`)** record local design tradeoffs only:

- module-level or subsystem-level choices
- local limitations
- implementation-level alternatives and their consequences

**Global tradeoffs (`docs/tradeoffs.md`)** record project-level deviations only:

- original spec vs actual implementation
- approved compromises
- unavoidable deviations
- major rejected alternatives with project-wide implications

Do not copy the same full tradeoff narrative into both places.

If a topic appears in both places:
- keep the leaf doc version short and local
- keep the full deviation record in `docs/tradeoffs.md`
- reference the corresponding tradeoff entry by stable ID from the leaf doc when useful (for example, `TRD-001`)

### 4.5 Spec-to-Implementation Matrix
`docs/matrix_*.md` is mandatory for Tier A and recommended for substantial Tier B work.

Purpose:
- map original intent to current implementation status
- show what exists, what is partial, what is deferred, and how each item is verified
- reference project-level deviations by tradeoff ID instead of duplicating long explanations

### 4.6 Integration
`integration_*.md` must contain:

- end-to-end assembly view
- integration dependencies
- validation checklist
- benchmark / regression / harness entry points
- known hard boundaries
- final acceptance status

### 4.7 Status / Handoff
`status_*.md` is recommended for accepted Tier A iterations and substantial accepted Tier B iterations, especially for long-running work, phase boundaries, or before switching threads.

It should contain:
- current objective
- accepted in-scope / out-of-scope boundary for the current iteration
- current implementation state
- validation snapshot
- active blockers or unresolved assumptions
- recommended next steps
- key references to relevant overview, leaf docs, matrix files, integration docs, and tradeoff IDs

Use this document as the primary handoff surface between threads and between major accepted iterations. Do not overload `AGENTS.md` with changing project state.

Treat `status_*.md` as a **current-state snapshot**, not as an append-only diary:
- overwrite the main sections as the project advances
- optionally keep a short recent milestone history if it improves continuity
- archive obsolete full snapshots only when they are no longer the active handoff surface

## 5. Omission Rule

If a module is omitted, state exactly:

**Not implemented in the current version.**

## 6. Zero-Drift Synchronization

When implementation changes materially:
- update affected leaf docs immediately
- update `docs/design/` if the high-level structure changes
- update the matrix if coverage or implementation status changes
- update integration docs if validation or assembly changes
- update status / handoff docs at accepted Tier A checkpoints, substantial accepted Tier B checkpoints, before thread switches, or whenever blockers / next steps materially change

Remove stale docs, dead references, deprecated harnesses, and filler text.
