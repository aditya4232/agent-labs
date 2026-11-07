# ADR 0002: Evaluation artifacts are first-class versioned outputs

- Status: Accepted; implementation pending.
- Date: 2026-11-07.

## Decision
Every evaluation run emits immutable machine-readable result artifacts with experiment manifest, code commit, dataset/model/prompt/evaluator versions, run metadata and per-task outputs. Reports are rendered from these artifacts. The evaluation protocol is stored alongside the experiment.

## Consequences
- Benchmarks can be audited and reproduced.
- UI cannot silently edit result values.
- Re-running a lab creates a new run, not an overwrite.
- Public reports disclose uncertainty, exclusions and limitations.
