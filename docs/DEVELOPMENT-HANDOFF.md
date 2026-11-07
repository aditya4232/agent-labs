# Agent Labs Development Handoff

Reviewed 2026-11-07. Controlled research/evaluation plan only; no live scanning or exploitation service is claimed.

## Product definition

Agent Labs produces reproducible evidence about agent safety, security controls and reliability for security engineers, AI engineers and researchers. It is not an unrestricted offensive scanner.

## Platform capabilities

Research registry (paper/advisory, claim, source, date, affected products, owner and review state); lab catalog (scope, threat model, authorization, dataset, tools and safety); experiment runner (pinned versions, seeds, quotas, timeout, isolation and kill switch); dataset registry (provenance, license, sensitivity, hash and retention); evaluator (metrics, baselines, confidence intervals); evidence store (raw machine-readable outputs and sanitized reports); publishing workflow (draft, peer review, security review, disclosure, publish/supersede); benchmark dashboard.

## Current advisory watch

### Linux kernel CERT-In CIVN-2026-0539

Issued 2026-11-06 for CVE-2026-98432, a use-after-free in the IPv4 TCP networking subsystem. The advisory lists affected stable lines and fixed commits. Lab should map installed package versions to vendor backports; upstream semver comparison alone is insufficient.

https://www.cert-in.org.in/s2cMainServlet?VLCODE=CIVN-2026-0539&pageid=PUBVLNOTES01

### Node.js October 2026 security release

Node.js published fixes on 2026-10-21 for maintained 22.x, 24.x and 26.x lines. Issues include DNS NUL truncation, TLS hostname verification/normalization, permission model, crypto snapshot and archive parsing. CERT-In CIVN-2026-0512 lists fixed upstream versions 26.12.1, 24.22.1 and 22.23.4. Check OS vendor backports.

https://nodejs.org/en/blog/vulnerability/october-2026-security-releases
https://www.cert-in.org.in/s2cMainServlet?VLCODE=CIVN-2026-0512&pageid=PUBVLNOTES01

### OWASP GenAI Security Top 10 2026

Update lab mappings to OWASP's 2026 edition: prompt injection, sensitive information disclosure, excessive agency, supply chain, data/model poisoning, unbounded consumption, misinformation, hidden context exposure, vector/embedding weaknesses and improper output handling.

https://github.com/GenAI-Security-Project/GenAI-LLM-Top10

## First lab backlog

1. Advisory Intake & Patch Triage: parse CVE/CERT-In/vendor advisories, affected ranges, fixed versions, distro backports and remediation.
2. MCP Attack Range: synthetic servers for tool poisoning, malicious output, confused deputy, OAuth audience mismatch, token/state replay and permission escalation.
3. RAG Isolation & Poisoning: cross-tenant markers, retrieval injection, stale records, ACL and provenance checks.
4. Agent Capability Benchmark: task completion vs unauthorized action, tool precision, approval and recovery.
5. Supply-chain Triage: lockfile/SBOM advisory matching, reachability and provenance.
6. Runtime Patch Regression: pinned vulnerable/fixed versions in isolated disposable environments.

## Experiment record

Record experiment ID, owner, commit SHA, date, authorization scope/expiry, threat model version, dataset ID/version/hash/license, synthetic/real label, model/provider/version, prompt hash, tool/server versions, runtime/kernel/container image, config, seeds, trials, sample size, baseline/control, metrics/confidence intervals, raw artifacts, sanitized report, limitations, reviewer and disclosure status.

Metrics: unauthorized action rate, sensitive disclosure, capability integrity violation, false refusal/positive, task success under attack, citation correctness, recovery, patch coverage/reachability, time-to-remediate, cost, latency and variance.

## Safety and authorization

Only owned systems, intentionally vulnerable labs or explicitly authorized targets. Exact scope and expiry required before run. No arbitrary public IP/domain scanning, credential theft, persistence, stealth, destructive action, exfiltration or denial of service. Use synthetic accounts/data/tokens. Egress deny-by-default, resource/time limits, isolated ephemeral targets, kill switch and verified teardown. Public reports focus on defensive mitigation and regression tests; coordinate disclosure.

## Development phases

P0 research registry, citation metadata, advisory intake and manual review.
P1 experiment schema, dataset registry, artifact store and deterministic evaluator.
P2 synthetic MCP attack range and baseline benchmark.
P3 RAG isolation/poisoning and agent capability suite.
P4 advisory/SBOM triage and disposable runtime regression.
P5 report publishing, benchmark comparison and opt-in sanitized Agent Workspace trace import.

## Acceptance gates

Authorization mandatory and enforced; no arbitrary public target; egress/resource ceilings tested; dataset license/provenance/hash; replay pinned; raw/sanitized artifact access separated; findings include confidence/limitations/reproduction; disclosure status explicit; retention/deletion/audit tested.
