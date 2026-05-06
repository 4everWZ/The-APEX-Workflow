---
name: apex-harness
description: Use for substantial coding, research, or ML tasks that require explicit risk classification, verification routing, user consultation boundaries, anti-silent-simplification safeguards, or structured documentation outputs such as specs, design docs, implementation matrices, tradeoff logs, and status handoff docs. Do not use for trivial low-risk local edits such as minor UI text changes, comments, or narrow fixes.
---

# APEX Harness Skill for Codex

Use this skill when the task is substantial enough that you need disciplined execution rather than ad hoc coding.

This skill is for:
- significant implementation or refactor work
- machine learning / deep learning algorithm work
- research-oriented coding where evaluation semantics matter
- architecture-level or cross-module changes
- tasks that need durable documentation, implementation tracking, explicit tradeoff handling, or clean handoff across accepted iterations or separate threads

Do **not** use this skill for trivial low-risk edits such as:
- minor UI text or style changes
- comments or docstrings only
- narrow local fixes with obvious behavior and low blast radius

## What this skill does

It enforces:
- risk-calibrated execution (`Tier A / B / C`)
- stronger verification for higher-risk work
- explicit boundaries for when the user must make decisions
- prohibition on silent simplification or silent scope narrowing
- documentation-code consistency
- structured documentation outputs under `docs/`
- two-level tradeoff handling: local design tradeoffs in leaf docs, project-level deviations in `docs/tradeoffs.md`, and matrix entries that reference stable tradeoff IDs without duplicating them
- explicit status / handoff documentation for accepted Tier A work and substantial accepted Tier B work, especially for long-running work, multi-thread handoff, or phase boundaries

## Core operating rules

- Do not fake completeness.
- Do not hide unfinished work behind vague wording.
- Do not guess APIs, tensor shapes, schemas, config semantics, contracts, or implicit invariants.
- Prefer typed, asserted, or mechanically checked boundaries.
- Do not silently simplify, omit, downgrade, or narrow requested scope.
- Tradeoff logs record approved or unavoidable deviations; they do not authorize silent ones.

## How to use this skill

1. Classify the task using `references/workflow.md`.
2. Apply the correct verification intensity from `references/workflow.md`.
3. If the task changes substantial behavior, architecture, evaluation semantics, or research interpretation, follow `references/documentation_topology.md`.
4. If the task is Tier A or a substantial Tier B task, maintain a spec-to-implementation mapping using `references/matrix_template.md`.
5. If the implementation materially deviates from the original plan, record the deviation using `references/tradeoff_template.md`.
6. For accepted Tier A iterations and substantial accepted Tier B iterations, especially at phase boundaries or before switching threads, maintain or refresh a current status / handoff document using `references/status_template.md`.

## Quick routing

Use `references/workflow.md` for:
- Tier A / B / C classification
- verification policy
- user consultation boundary
- harness rules
- completion rules
- iteration handoff rules
- environment policy

Use `references/documentation_topology.md` for:
- repository documentation topology
- what belongs in `docs/specs/`
- what belongs in `docs/design/`
- what belongs in `docs/matrix_*.md`
- required anchor docs
- update rules by tier

Use `references/matrix_template.md` for:
- original-intent to current-implementation mapping

Use `references/tradeoff_template.md` for:
- `docs/tradeoffs.md` entry format with stable IDs

Use `references/status_template.md` for:
- current objective, accepted scope, implementation snapshot, blockers, validation status, next steps, and next-thread handoff

## Repository assumptions for this skill

Unless the repository clearly defines a different structure, assume:
- `docs/specs/` = active specifications and leaf docs
- `docs/specs/legacy/` = superseded specifications
- `docs/specs/status_*.md` = current-state snapshots and handoff notes for accepted Tier A work and substantial accepted Tier B work
- `docs/design/` = global architecture, system framework, or network structure docs
- `docs/matrix_*.md` = spec-to-implementation matrices
- `docs/tradeoffs.md` = repository-wide approved or unavoidable deviations

If the repository already has a stronger convention, follow repository truth.

## Minimal always-on behavior

Even when this skill is active:
- keep diffs proportionate to task scope
- prefer existing reliable tests over redundant scaffolding
- ask the user before committing to material research or architecture tradeoffs
- do not claim completion unless claimed scope, verification, and required documentation are mutually consistent
