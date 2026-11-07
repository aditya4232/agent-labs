# Agent Labs — reproducible research for reliable AI agents

Agent Labs is the experimentation, evaluation and evidence layer of the Aditya CUZ.in ecosystem. It tests whether agent systems behave reliably, safely and economically, and publishes reproducible artifacts rather than marketing claims.

**Status:** design phase / planned. A lab is not implemented until a runnable experiment, evaluation harness and reproducibility artifact exist.

## Role in the ecosystem
- **Portfolio:** curated case studies and reports with evidence.
- **Clemo:** workspace catalog and launcher; does not own experiment execution or private traces.
- **Agent Workspace:** supplies versioned trace events or synthetic replay fixtures.
- **Agent Labs:** owns datasets, protocols, scoring, runs and result artifacts.

## Labs
| Lab | Core question | Required output |
|---|---|---|
| Trace Lab | Did the agent satisfy task and policy at every step? | Trace viewer, step assertions, run comparison |
| Break My Agent | Which attack classes bypass tool policy? | Synthetic corpus, defense matrix, reproducible scores |
| RAG Reliability | Does retrieval improve grounded quality over a strong baseline? | Retrieval/answer metrics, citation audits, ablations |
| Context Budget Lab | What is lost during truncation and compaction? | Token accounting, retained-fact recall, cost/latency |
| Model Router Lab | What quality/latency/cost trade-off results from routing? | Pareto frontier, task strata, fallback analysis |
| Tool Reliability Lab | How do validation, retries and approvals affect tool success? | Fault injection, policy coverage, replay reports |

## Research standard
Every result includes hypothesis, protocol, baselines, dataset provenance/license, model/provider/version, prompt/policy version, parameters, seeds where supported, independent run count, uncertainty, failures, limitations, environment lockfile and machine-readable results. Never compare models with different prompts or unequal budgets without describing the confound.

## Metrics
Use task-specific metrics: task success with a written rubric; tool-call correctness; invalid argument and policy violation rate; citation precision/recall and entailment; prompt-injection success by category; latency p50/p95; tokens, retries and estimated cost per successful task; robustness across paraphrase, multi-turn, long-context and adversarial inputs. Publish denominators and uncertainty. Include deterministic/no-model baselines where meaningful.

## Safety boundary
Public labs use synthetic datasets, fake tools and isolated sandboxes. Never test against real accounts, production systems, actual secrets or third-party targets without written authorization. Prompt injection success is not proof of exploitability unless threat model and execution path match.

## Architecture
See [Architecture](docs/ARCHITECTURE.md), [Evaluation protocol](docs/EVALUATION-PROTOCOL.md), [Roadmap](docs/ROADMAP.md), [Security](SECURITY.md). Keep packages isolated per lab; share only schemas, harness primitives and UI components.
