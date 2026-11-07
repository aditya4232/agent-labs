# Agent Labs Documentation

Status: research and architecture baseline; no live evaluation platform is claimed.

- [AI builder context](AI-BUILD-CONTEXT.md): product truth, ownership, research standards, safety boundaries and build workflow.
- [Architecture](ARCHITECTURE.md): system boundaries and evidence artifacts.
- [Evaluation protocol](EVALUATION-PROTOCOL.md): reproducible experiment requirements.
- [Roadmap](ROADMAP.md): delivery phases.
- [Security research program](SECURITY-RESEARCH-PROGRAM.md): current Node.js/Linux watch, MCP/agent papers, defensive labs and responsible testing.
- [Research and benchmark standards 2026](RESEARCH-AND-BENCHMARK-STANDARDS-2026.md): consumer trust context, reproducible metrics, threat corpus, safe execution and release gates.
- [Development handoff](DEVELOPMENT-HANDOFF.md): platform components, advisory workflow, first labs, experiment schema, safety controls and release gates.

## Evidence standard
Every claim includes scope, authorization, environment, versions, dataset hash, sample size, method, uncertainty, limitations and reproducibility artifacts. Security testing is restricted to owned systems, intentionally vulnerable labs or explicitly authorized scope. No arbitrary third-party scanning or exploitation.

## Product boundary
Agent Labs owns experiments, datasets, benchmark results and security reports. It does not store Clemo billing state, Agent Workspace provider secrets or production chat transcripts. Only sanitized, opt-in traces may be evaluated.
