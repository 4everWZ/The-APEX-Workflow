# Workflow

## 1. Task Classification

Before implementation, classify the task.

### Tier A — Heavyweight
Use when changes affect:
- research logic, algorithms, math, losses, evaluation, baselines, or ablations
- training or inference semantics
- data preprocessing, dataset contracts, or label meaning
- architecture or cross-module contracts
- public APIs, storage schemas, or correctness-critical infrastructure
- any change that could materially alter scope, capability, claims, or downstream trust

### Tier B — Standard
Use when changes affect:
- internal backend logic
- medium bugfixes
- config behavior
- scripts
- moderate refactors
- local but behavior-changing code

### Tier C — Lightweight
Use when changes are low-risk and local:
- UI text or styling
- logging
- comments or docstrings
- narrow parameter plumbing
- non-behavioral renames
- highly localized fixes

### Classification Rules
- Default to the lowest truthful tier.
- Escalate immediately when the task is found to affect a higher-risk boundary than initially classified.
- If uncertain, escalate one tier up.

## 2. Verification Policy

Verification intensity must match task intensity.

### Tier A
Must include:
- explicit success criteria
- observability check
- critical review
- dedicated harness or equally isolated verification path when existing tests are insufficient
- autonomous verification loop
- required documentation sync
- tradeoff logging for material deviation

### Tier B
Must include:
- concrete success criteria
- existing tests first
- minimal additional targeted verification if coverage is insufficient
- relevant local checks
- documentation updates only when behavior, usage, contracts, architecture, evaluation semantics, or non-obvious constraints materially change
- tradeoff logging only for material deviation

### Tier C
Must include:
- confirmation that the edit is truly low-risk and local
- lightweight validation such as smoke checks, linting, visual confirmation, or narrow test runs
- no dedicated harness unless no cheaper credible validation exists
- no heavy documentation routing unless behavior, architecture, or contracts are affected

### Global Verification Rules
- Existing reliable tests are preferred over redundant new harnesses.
- Irrelevant green checks do not count as verification.
- Verification must cover the changed claim, not merely execute some part of the repository.
- If outputs cannot be observed locally, verification claims must be narrowed accordingly.

## 3. User Consultation Boundary

Risk escalation means stricter verification and documentation, not automatic user interruption.

Do not ask the user for confirmation for:
- routine debugging
- routine tier escalation
- local refactors
- implementation details that can be resolved mechanically from repository code and active specs

Ask the user only when:
- the requested change conflicts with the active spec, repository contract, or a prior explicit instruction
- multiple materially different implementations would satisfy the request but imply different product, research, maintenance, or evaluation tradeoffs, and the choice cannot be resolved mechanically
- proceeding would require changing scope, public behavior, evaluation semantics, data semantics, or external contracts beyond what the user requested
- a required external input, credential, approval, or product decision is missing

For Tier A research tasks, ask the user before committing to materially different design choices in:
- objectives
- baselines
- evaluation protocols
- ablation scope
- data semantics
- architectural interpretation
- other decisions that would meaningfully change the research claim or experimental interpretation

Do not silently simplify, omit, downgrade, or narrow a requested feature, algorithm, evaluation setup, or spec-defined requirement merely because a cheaper implementation is easier to complete locally. If such a reduction would materially change scope, capability, scientific claim, or interpretation, surface the tradeoffs and ask the user before proceeding.

If none of the above applies, choose the most defensible implementation and continue autonomously.

## 4. Execution Workflow

Follow this flow at the appropriate intensity:

1. Read relevant repository context.
2. Classify the task.
3. Define success criteria appropriate to the tier.
4. Ensure outputs are observable locally.
5. Perform a critical review of assumptions and risk.
6. Choose the least expensive verification path that still provides real confidence.
7. Implement the most defensible version of the change.
8. Run verification and iterate until criteria are met or a hard boundary is reached.
9. Synchronize documentation if required by scope.
10. For accepted Tier A iterations and substantial accepted Tier B iterations, especially at phase boundaries or before switching threads, update the status / handoff document.

## 5. Harness Rules

Harnesses are a tool, not a ritual.

### Build a Dedicated Harness When
- the task is Tier A
- risky boundaries are not adequately covered by existing tests
- shapes, interfaces, data contracts, or evaluation semantics must be validated in isolation
- repository tests are too coarse to localize the changed claim

### Do Not Build a Dedicated Harness When
- the task is narrow Tier C work
- existing tests already verify the changed behavior credibly
- the harness would be heavier than the change
- a smaller targeted check provides equivalent confidence

### Harness Requirements
A valid harness should:
- stay minimal
- use deterministic fixtures where feasible
- assert the critical claim directly
- expose observable outputs
- avoid fake confidence from unrelated mocks

## 6. Completion Rules

A task is complete only when, at the required tier:
- implementation matches the claimed scope
- relevant verification has passed, or the failure boundary is explicitly documented
- behavior-changing claims are supported by observed evidence
- required documentation updates are complete
- no known critical contradiction remains between code, tests, documentation, and the implementation matrix

If blocked by a hard boundary such as missing credentials, unavailable hardware, missing datasets, external service failure, or unrecoverable environment limits:
- do not bluff
- state exactly what was verified
- state what remains unverified
- state the blocking boundary precisely

## 7. Iteration Handoff

For accepted Tier A work and substantial accepted Tier B work:
- prefer separate threads for materially different workstreams such as research exploration, system integration, bug investigation, or branch exploration
- use the repository status / handoff document to transfer current state between threads or between major accepted iterations
- at the end of an accepted iteration, update the current objective, accepted scope, implementation snapshot, validation status, blockers, next steps, and relevant references

A new thread should resume from repository docs and the current status / handoff document rather than relying on old conversational context alone.

## 8. Environment Policy

Follow repository-native tooling first.

Rules:
- If the repository clearly standardizes on a toolchain, package manager, or execution path, follow it.
- Otherwise prefer the currently active local environment.
- For Python, default to the active local conda environment unless the repository clearly uses something else.
- Do not introduce a new environment manager unless the repository already uses it, the task explicitly requires it, or the current environment is provably insufficient and the change is documented.

## 9. Priority Order

When requirements conflict, prioritize:

1. Scientific defensibility
2. Implementation viability
3. Clear evaluation semantics
4. Contract correctness
5. Maintainability
6. Surface fidelity
7. Integration elegance

When uncertain, narrow the claim, increase verification, or state the uncertainty explicitly.
