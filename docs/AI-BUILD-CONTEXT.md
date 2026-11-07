# Agent Labs — AI Build Context

**Last reviewed:** 2026-11-07  
**Truth status:** research/design phase. No live evaluation runner, public scanner, exploit service, dataset registry or benchmark dashboard is implemented.

## Mission
Produce reproducible evidence about AI agent quality, reliability, security and cost. Labs are defensive, scoped and safe by construction; not an unrestricted vulnerability scanner or marketing leaderboard.

## Ownership
Agent Labs owns research registry, datasets, experiment specs, runner, evaluator, evidence artifacts, reports and benchmark history. Agent Workspace owns user chats and secrets. Clemo owns credits/commerce. Portfolio owns public editorial material. Only synthetic/public or explicitly consented, minimized, sanitized traces may enter Labs.

## Research quality
Every experiment pins commit, environment/container digest, model/provider/revision, prompt/policy/tool schema, dataset license/version/hash/split, evaluator version, seed where supported, concurrency, timeout, retry policy, sample size, exclusions, baseline and authorization scope. Report denominators, confidence intervals, variance, failures and limitations. Separate exploratory, validation and held-out test sets. No tuning on held-out data.

## Core metrics
Task success and partial success; citation support/unsupported claims; tool schema/target correctness; unauthorized action and sensitive disclosure rates; prompt injection success; recovery/cancel correctness; p50/p95/p99 TTFT/ITL/total duration; tokens and cost per successful task; user correction/abandonment where consented.

## Security research boundaries
Only owned systems, intentionally vulnerable synthetic targets or exact written authorization with expiry. No arbitrary public scans, credential theft, stealth, persistence, exfiltration, destructive actions or DoS. Synthetic credentials, egress deny-by-default, ephemeral isolated runners, CPU/memory/time/output ceilings, kill switch and verified teardown. Dataset license/provenance/sensitivity review is mandatory.

## Experiment lifecycle
Proposed → reviewed → authorized → queued → running → evaluating → peer_review → published/superseded/aborted. Runner authorization and scope are enforced outside model output. Raw artifacts access-separated from sanitized reports. Artifact ingestion is untrusted; never execute embedded content. Trace import is opt-in, minimized, redacted, revocable and time-limited.

## Benchmarking
Separate API overhead, queue wait, retrieval/prefill, TTFT, ITL/TPOT, tool time, total wall clock, tokens, retries and cost. For self-hosted inference pin GPU, driver, CUDA/runtime, quantization, serving engine, batch policy, prompt/output distribution, concurrency, warm/cold state and cache. Compare equivalent prompts, budgets and model revisions. Include no-agent baseline and human adjudication for subjective tasks.

## Technology policy
TypeScript for web/API and orchestration. Python for evaluation harness, statistics and ML experiments. Rust only for isolated high-performance parsing or sandbox components after profiling. Go only for independently operated runner services when workload and ops justify it. Prefer containerized ephemeral workers with explicit resource limits; never run arbitrary experiment code in the API process.

## Data and privacy
No secrets or raw private prompts in public reports. Hash and minimize trace inputs. Enforce retention/deletion and license attribution. Never train on imported traces without explicit opt-in. Public reports must be reviewed for sensitive data and coordinated disclosure.

## Initial delivery order
P0 schemas, experiment manifest, dataset provenance model and deterministic evaluator core.
P1 reproducibility CLI/runner for synthetic fixtures.
P2 MCP threat corpus and authorization/approval test harness.
P3 RAG isolation/provenance/poisoning tests.
P4 latency/quality/cost evaluation and model comparison.
P5 report publishing and opt-in sanitized trace ingestion.

## AI builder workflow
Treat every claim as a hypothesis until reproduced. Write deterministic fixtures and tests first. Pin versions. Run safe synthetic targets only. Publish exact command/output, data hashes, denominators, uncertainty and limitations. Do not imply that a benchmark proves general security or performance outside its tested scope.
