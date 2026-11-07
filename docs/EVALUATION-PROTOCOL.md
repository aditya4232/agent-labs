# Agent Labs Evaluation Protocol

## Experiment record
Record experiment/version, run ID, timestamp, git commit, environment/container digest, dataset/version/license/hash/split provenance, exact model/provider/revision, inference parameters, context limits, prompt/policy/tool-schema/evaluator versions, seed where supported, concurrency, retries, timeout, task counts, exclusions and reasons, per-task outputs/scores/failure class/latency/tokens/cost, evaluator version and human adjudication.

Never store secrets or private user content. Public artifacts use synthetic or licensed data.

## Benchmark design
- Pre-register hypothesis and primary metric before final evaluation.
- Include a meaningful deterministic/no-retrieval/current-policy baseline.
- Separate development and held-out sets; do not tune on held-out tasks.
- Run multiple independent trials; report n, median/mean and uncertainty.
- Match token, tool, time and monetary budgets.
- Include ablations for major components.
- Preserve raw result JSON and evaluator output.
- Document evaluator bias and human review for subjective criteria.

## Agent trace schema
Run envelope and ordered spans: trace_id, run_id, parent_span_id, span_id, sequence, type (model/tool/retrieval/policy/human_approval/transform), timestamps, status, model/tool ID, token/cost metadata, input/output hashes and redacted summaries, policy decision, approval reference, error class, retries, source references and evaluator assertions.

Trace payloads are untrusted. Escape content, never execute embedded markup, enforce size limits and redact credentials, PII and document text.

## Security taxonomy
Map experiments to OWASP LLM risks: prompt injection, sensitive information disclosure, supply chain, data/model poisoning, improper output handling, excessive agency, system prompt leakage, vector/embedding weaknesses, misinformation and unbounded consumption. Record attacker capability, trust boundary, vector, expected policy, fake/real tool mode, objective, success criteria, defense, bypasses and false-positive/negative review.

## Reporting
Each report includes question, methodology, dataset/model versions, results with denominators, failure analysis, limitations, reproducibility command and downloadable JSON. Do not use one composite score unless weighting is justified and sensitivity analysis is published.
