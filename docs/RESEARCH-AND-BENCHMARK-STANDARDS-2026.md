# Agent Labs research and benchmark standards — 2026

**Reviewed:** 2026-11-07  
**Status:** research protocol and engineering requirements; no live scanner, exploit service or production benchmark is claimed.

## Mission

Agent Labs must answer whether an AI/agent system is useful, reliable, safe and economical under representative and adversarial conditions. It is not a marketing leaderboard or an unrestricted scanner. Every public claim must be reproducible and bounded by its test conditions.

## Consumer-market context

AI adoption does not eliminate trust requirements. Ipsos reports high AI awareness in India, while Gartner's 2026 US consumer survey identifies accuracy and reluctance to delegate purchase decisions as barriers. NIQ's India metro shopping study reports strong AI-shopping use but is limited to its surveyed metros and categories:
- https://www.ipsos.com/en-in/ipsos-ai-monitor-2026-india-report
- https://www.gartner.com/en/newsroom/press-releases/2026-05-27-gartner-survey-finds-consumers-want-ai-shopping-help-but-not-ai-purchase-decisions
- https://nielseniq.com/global/en/insights/report/2026/agentic-commerce-india-2026/

Research priority: evaluate not only task completion, but user trust, factual grounding, permission correctness, failure transparency, recoverability, accessibility and cost per successful task. For consumer-facing products, "agent completed the task" is insufficient if it acted without consent or cannot explain evidence.

## Benchmark design rules

- Pre-register hypothesis, primary metric, inclusion/exclusion rules and analysis before final evaluation.
- Include deterministic, no-agent or current-policy baseline.
- Use held-out evaluation data; never tune prompts, policies or thresholds on the final test set.
- Match model revision, system prompt, tool schema, context window, sampling parameters, timeout, token/tool budget and concurrency.
- Report n, independent trials, confidence intervals, variance, exclusions and missing runs.
- Stratify by task type, difficulty, language, context length, adversarial class, user skill and device/network class where relevant.
- Publish raw machine-readable results and exact evaluator version; human-adjudicate subjective outcomes with blinded rubric where possible.
- Report both macro and per-class results. A single composite score requires justified weights and sensitivity analysis.
- Treat model-graded evaluations as noisy; validate evaluator agreement against human-reviewed samples.
- Do not compare providers on different prompts or unequal budgets without explicitly labeling the confound.
- Record failed runs and retries; never silently discard them.

## Required metrics

| Dimension | Metrics |
|---|---|
| Usefulness | task success, partial success, user-rated helpfulness, time saved |
| Factual quality | citation precision/recall, entailment, unsupported-claim rate, freshness |
| Tool correctness | schema validity, correct target/resource, tool precision/recall |
| Safety | unauthorized action rate, policy bypass, sensitive disclosure, prompt-injection success |
| Reliability | recovery, cancellation correctness, duplicate side effects, retry rate |
| Speed | API acknowledgement, queue time, TTFT, ITL/TPOT, total duration p50/p95/p99 |
| Cost | tokens, provider cost, retries, tool calls, cost per successful task |
| UX | approval burden, abandonment, correction rate, comprehension and accessibility |

A system is not "better" if latency improves while task quality, security, or cost per successful task regresses beyond pre-registered guardrails.

## Agent and MCP threat corpus

Use synthetic targets and fake credentials. Cover:
- direct and indirect prompt injection from documents, webpages, issues and tool outputs;
- MCP tool poisoning and metadata changes after approval;
- confused deputy, scope escalation, OAuth issuer/audience/resource mismatch, state/token replay;
- SSRF, DNS rebinding, redirects, IPv4/IPv6, cloud metadata and private IP access;
- cross-tenant retrieval, stale ACL, vector poisoning and source provenance failure;
- secret leakage through prompts, traces, errors, logs and artifacts;
- approval replay or action/argument/target substitution;
- duplicate queue delivery and retry-induced duplicate external side effects;
- excessive agency, unbounded tool loops, token/resource exhaustion and unsafe fallback;
- malicious file/archive inputs, path traversal, symlink escape and decompression bombs.

Detection heuristics are signals only. Passing an injection classifier is not proof of safety; enforce permissions, isolation, egress controls, human approvals and deterministic policy outside the model.

OWASP Agent/MCP security guidance: https://owasp.github.io/DevSecOpsGuideline/2-Process/2-2-Develop/2-2-5-AI-Agent-and-MCP-Security/  
NSA MCP security design considerations: https://www.nsa.gov/Press-Room/Press-Releases-Statements/Press-Release-View/Article/4496698/nsa-releases-security-design-considerations-for-ai-driven-automation-leveraging/

## Performance benchmarking

For interactive inference, separate platform overhead from provider behavior:
- client-to-edge/API acknowledgement;
- queue/scheduler wait;
- context retrieval and prefill;
- TTFT;
- inter-token latency / TPOT;
- total generation and final response;
- tool latency and approval wait;
- retries, tokens and cost.

For self-hosted inference, pin GPU type, driver, CUDA/runtime, model quantization, serving engine, batch policy, prompt/output length distribution and concurrency. Include warm and cold runs, cache hit/miss and queue saturation. Use continuous batching and prefix/KV cache only where the measured workload benefits. Do not report tokens/sec without describing the denominator and load.

vLLM documents request-level TTFT, queue time, generation time, inter-token latency and throughput as distinct measurements: https://github.com/vllm-project/vllm/blob/main/docs/features/per_request_metrics.md  
AWS inference guidance describes latency-aware routing, prefix caching, chunked prefill and continuous batching as workload-dependent optimizations: https://docs.aws.amazon.com/pdfs/prescriptive-guidance/latest/gen-ai-inference-architecture-and-best-practices-on-aws/gen-ai-inference-architecture-and-best-practices-on-aws.pdf

## Reproducibility artifact schema

Each run stores: experiment ID/version; owner; commit SHA; timestamp; authorization scope and expiry; environment/container digest; dataset ID/version/license/hash/split; synthetic/real classification; model/provider/revision; prompt/policy/tool schema/evaluator versions; inference parameters; seed where supported; concurrency; retries; timeout; task count; exclusions; per-task output hash and redacted summary; metrics; uncertainty; raw result JSON; sanitized report; reviewer; disclosure status; retention and deletion status.

Never store production secrets or private user prompts in public benchmark artifacts. Opt-in trace imports must be minimized, redacted, consented and revocable.

## Safe execution architecture

- Only owned, intentionally vulnerable or explicitly authorized targets with exact scope and expiry.
- No arbitrary public IP/domain scans, credential theft, persistence, stealth, exfiltration, destructive action or denial of service.
- Disposable isolated targets; egress deny-by-default; fake accounts/tokens; strict CPU/memory/time/output ceilings; kill switch and verified teardown.
- Separate runner identity from researcher identity; short-lived scoped credentials only.
- Artifact ingestion treats content as untrusted; sanitize HTML/Markdown; never execute embedded code.
- Dataset provenance, license, sensitive-data review and deletion policy are mandatory.
- Publish defensive reproduction and mitigation, coordinate disclosure, and document limitations.

## Release gates

1. Protocol and threat model approved before each lab run.
2. Dataset provenance/license/hash verified.
3. Baseline and held-out set present.
4. Environment/model/prompt/tool versions pinned.
5. Safety boundary, egress and resource caps tested.
6. Result includes denominators, uncertainty and failure analysis.
7. Reviewer reproduces a sample or full run.
8. Raw and sanitized artifacts access-separated.
9. No unsupported generalization beyond the benchmark's population/workload.
10. Every release records known limitations and superseded results.

## Research backlog

P0: advisory intake with vendor-backport-aware patch triage.  
P1: deterministic trace evaluator and reproducibility manifest.  
P2: synthetic MCP attack range and policy-bypass matrix.  
P3: RAG tenant-isolation, provenance and poisoning suite.  
P4: model-router quality/latency/cost Pareto evaluation.  
P5: reliability under retries, cancellation, network loss, overload and provider degradation.
