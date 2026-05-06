# Spec-to-Implementation Matrix Template

Use this for `docs/matrix_<topic>.md`.

| Requirement ID | Original Intent | Current Status | Implementation Pointer | Verification Pointer | Notes |
|---|---|---|---|---|---|
| R1 |  | Implemented / Partially Implemented / Deferred / Not Implemented |  |  |  |
| R2 |  | Implemented / Partially Implemented / Deferred / Not Implemented |  |  |  |

## Guidance

- **Requirement ID**: short stable identifier such as `R1`, `R2`, `Ablation-1`, `API-3`
- **Original Intent**: what the original spec actually asked for
- **Current Status**:
  - `Implemented`
  - `Partially Implemented`
  - `Deferred`
  - `Not Implemented`
- **Implementation Pointer**: file, module, API, config key, or doc reference
- **Verification Pointer**: test, harness, benchmark, command, or manual validation path
- **Notes**: constraints, caveats, partial-scope clarification, or a short pointer to a relevant project-level tradeoff ID such as `TRD-001`

## Rules

- This matrix is a coverage document, not a tradeoff log.
- If implementation status differs from the original spec because of a project-level deviation, reference the relevant entry in `docs/tradeoffs.md` by stable tradeoff ID in **Notes**.
- Do not duplicate full tradeoff narratives here.
