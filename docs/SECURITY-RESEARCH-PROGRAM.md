# Security Research and Agent Evaluation Program

Status: defensive research and controlled testing program; no authorization for testing third-party systems.
Date: 2026-11-07.

## Mission

Agent Labs is a reproducible research environment for security engineers, defenders and AI builders. Every result states scope, authorization, environment, method, dataset/model/tool versions, sample size, limitations and reproduction artifacts.

## Research tracks

1. Agent/MCP security: prompt injection, tool poisoning, confused deputy, OAuth audience confusion, state-handle hijacking, unsafe invocation and cross-tenant leakage.
2. RAG security/reliability: retrieval injection, provenance, data isolation, stale knowledge, citation correctness and private-data exfiltration.
3. Software supply chain: SBOM, vulnerable dependencies, malicious packages, typosquatting, maintainer compromise, build provenance and dependency confusion.
4. Runtime/kernel: Linux advisories, container boundaries, namespaces/capabilities, syscall exposure and sandbox escapes.
5. Node/web runtime: DNS normalization, TLS verification, decompression, HTTP parsing, permission model and dependency chain.
6. Cloud/identity: SSRF, workload identity, secrets, OAuth/OIDC, webhook replay and CI/CD token overreach.
7. Agent reliability: tool correctness, long-running recovery, context budgets, routing and approval effectiveness.

## Current security watch — verified examples

### Node.js October 21, 2026 security release

Official Node.js release describes high-severity DNS NUL truncation and TLS hostname normalization issues, a Brotli decoder memory-safety issue and other HTTP/permission-model flaws across maintained 22.x, 24.x and 26.x lines. CERT-In published CIVN-2026-0512 on 22 October 2026. Use the official fixed-version matrix for each runtime line; do not copy generic upgrade advice without checking the deployed version.

- https://nodejs.org/en/blog/vulnerability/october-2026-security-releases
- https://www.cert-in.org.in/s2cMainServlet?VLCODE=CIVN-2026-0512&pageid=PUBVLNOTES01

### Linux kernel — CERT-In November 6, 2026

CERT-In CIVN-2026-0539 reports a critical use-after-free affecting kernel versions 4.4 and later, with fixed versions across maintained stable branches. The note describes possible memory corruption, code execution or denial of service. Build a patch-triage lab with disposable VMs and vendor kernel packages, not production exploitation.

- https://www.cert-in.org.in/s2cMainServlet?VLCODE=CIVN-2026-0539&pageid=PUBVLNOTES01

### Agent/MCP security research

- MCP Security Bench (2025) evaluates attacks across planning, tool invocation and response handling: https://arxiv.org/abs/2510.15994
- Security Considerations for AI Agents (2026) discusses indirect prompt injection, confused deputy behavior, connectors and multi-agent cascading failures: https://arxiv.org/abs/2603.12230
- AgentSecBench (2026) proposes instruction-integrity, retrieval-confidentiality and capability-integrity evaluations: https://arxiv.org/abs/2605.26269
- Official MCP 2026-07-28 security guidance covers audience-bound tokens, consent, confused deputy and state-handle misuse: https://github.com/modelcontextprotocol/modelcontextprotocol/blob/main/docs/docs/2026-07-28/tutorials/security/security_best_practices.mdx

Papers are hypotheses and evaluation designs, not proof a defense works in our system. Reproduce relevant claims in our own harness.

## Labs to build

### CVE Patch Triage
Input advisory/CVE, product, kernel/runtime version and package inventory. Output affected/fixed range, distro backport caveat, reachability/exposure, patch priority, verification and rollback notes. No exploit execution by default.

### MCP Attack Range
Synthetic MCP servers with benign/malicious descriptions, forged outputs, prompt injection, confused-deputy attempts, state-handle reuse and OAuth audience mismatch. Measure unauthorized action, data disclosure, false refusal and task completion.

### RAG Poisoning
Synthetic corpora with poisoned documents, stale records and cross-tenant markers. Test provenance, source ACL enforcement and instruction/data separation.

### Dependency Supply-Chain
Use lockfiles/SBOM and public advisories. Detect vulnerable ranges, malicious package indicators and transitive exposure. Never publish unverified claims about maintainers.

### Sandbox Escape Regression
Disposable isolated environments only, no secrets, no production network and documented teardown. Public demos use synthetic vulnerable targets.

### Agent Reliability
Benchmark planning, tool selection, recovery, budget compliance, citation accuracy and human approval across pinned model/tool versions.

## Responsible testing policy

Only test owned systems, intentionally vulnerable labs or targets with written authorization and exact scope. No arbitrary public IP/domain scanning, persistence, stealth, credential theft, destructive actions, exfiltration or denial-of-service. Use synthetic identities/data/tokens/domains. Keep proof-of-concept minimal and non-destructive; prefer regression tests and patch verification. Coordinate disclosure with maintainers. Publish mitigations and detection logic; restrict details that materially enable abuse. Every lab has kill switch, resource/time limits, egress deny-by-default and teardown verification.

## Evaluation protocol

Record experiment ID, commit SHA, date, owner, authorization scope, dataset ID/version/hash, contamination checks, model/provider/version, sampling parameters, prompt hash, tool/server versions, permissions, hardware/runtime/kernel/container image, trials/seeds/baseline/control, sample size, metrics/confidence intervals, raw machine-readable outputs, sanitized report, failure analysis and reproduction steps.

Metrics: unauthorized action success, sensitive-data disclosure, tool-integrity violation, false positive/refusal, task completion under attack, time-to-detect/recover and patch coverage/reachability.

## Publishing template

Executive summary; threat model; scope; method; results; artifacts; limitations; mitigations; disclosure status; references. Never claim "secure" based on a small benchmark. Label simulated vs real-world data.

## Sources

- Node.js security releases, 21 Oct 2026: https://nodejs.org/en/blog/vulnerability/october-2026-security-releases
- CERT-In Node.js CIVN-2026-0512: https://www.cert-in.org.in/s2cMainServlet?VLCODE=CIVN-2026-0512&pageid=PUBVLNOTES01
- CERT-In Linux kernel CIVN-2026-0539: https://www.cert-in.org.in/s2cMainServlet?VLCODE=CIVN-2026-0539&pageid=PUBVLNOTES01
- MCP Security Bench: https://arxiv.org/abs/2510.15994
- AgentSecBench: https://arxiv.org/abs/2605.26269
