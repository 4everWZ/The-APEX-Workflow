# Tradeoff Log Template

Use this exact structure for each material deviation in `docs/tradeoffs.md`.

## Entry

### [TRD-001] Short Title
- **Original Spec/Idea:** ...
- **Actual Implementation:** ...
- **Reasoning:** ...

## ID Rules

- Use a short stable identifier for each entry, for example `TRD-001`, `TRD-002`, `TRD-003`.
- Keep the ID stable once assigned so leaf docs and matrices can reference it.
- The short title should summarize the deviation in one line.

## Rules

- Record only approved deviations, unavoidable deviations, or major rejected alternatives.
- Do not use FAQ-style prose.
- Do not use this file as a substitute for architecture docs, leaf docs, or the implementation matrix.
- Tradeoff logs record deviations; they do not authorize silent simplification.
- Use this file only for project-level deviations. Do not move ordinary module-level design tradeoffs out of leaf documents unless they also represent a material project-level deviation.
- If a leaf doc or matrix needs to mention a project-level deviation, reference the entry by ID instead of repeating the full explanation.
