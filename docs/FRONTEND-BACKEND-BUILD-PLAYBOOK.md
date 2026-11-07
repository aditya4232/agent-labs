# Agent Labs Frontend and Research Platform Build Playbook

**Status:** implementation contract for a defensive research platform; no live runner/dashboard is claimed.

## Product experience

Agent Labs is a reproducible research and evaluation workbench, not a generic analytics dashboard or unrestricted scanner. Its core value is credible evidence: experiment definitions, dataset provenance, authorization scope, environment pins, run status, metrics, uncertainty, failure analysis and reproducibility artifacts.

Primary screens: research overview; experiment catalog; experiment detail/protocol; dataset registry/provenance; run queue/status; result comparison; metric and trace inspector; report publication; authorization/safety review; admin/audit. Distinguish exploratory results from validated and held-out results. Never present a score without denominator, version, sample count and limitations.

## Frontend architecture and visual system

- Next.js App Router, React, strict TypeScript and Tailwind CSS v4.
- Server Components for report pages and static research descriptions; client islands for filters, run controls, charts, trace inspection and comparison.
- Motion for React only for meaningful state changes. GSAP/Three.js are not needed for the core evidence UI.
- Accessible tables and charts, explicit units/axes, source/denominator annotations, downloadable machine-readable results and keyboard navigation.
- Zod and versioned OpenAPI/JSON Schema contracts.
- Vitest, React Testing Library, Playwright, axe-core and visual regression.

Design for analytical clarity: neutral research surfaces, strong typographic hierarchy, restrained accent color, legible dense tables and explicit uncertainty. Avoid decorative dashboards, unlabeled charts, glowing gradients, fake live activity and arbitrary confidence scores.

## Taste Skill and Impeccable

Install in the frontend repository:

```bash
npx skills add https://github.com/Leonxlnx/taste-skill --skill "design-taste-frontend"
npx impeccable install
```

Reload Claude Code, run `/impeccable init` and keep PRODUCT.md / DESIGN.md aligned with the research mission. Enable hooks only after reviewing and approving them: `/impeccable hooks on`.

Use Taste Skill to shape a coherent art direction; use Impeccable to critique, audit, polish and detect UI anti-patterns. Research evidence, accessibility and data visualization correctness override stylistic recommendations. Avoid asking both skills to redesign the same screen concurrently. Browser checks require Node 22+ and Chrome/Edge/Chromium. References: https://github.com/Leonxlnx/taste-skill, https://www.tasteskill.dev/docs/, https://impeccable.style/docs/.

## Figma

Figma is useful for the experiment detail, run lifecycle, comparison table/chart, trace inspector and report page. Define reusable tokens, table density, chart grammar, uncertainty/limitations treatment, responsive behavior and empty/error states. Prototype complex run state transitions, not every static report page. Keep charts editable and backed by typed data; screenshots are not data visualizations.

## Backend and research runtime

- TypeScript + Hono on Cloudflare Workers for registry, API and orchestration control plane.
- Python for evaluation harness, statistics, dataset processing and ML experiments.
- Isolated ephemeral container/runner for experiment execution; never execute arbitrary code in the API Worker.
- Dataset registry with provenance, license, sensitivity, hash, version, split and retention.
- Experiment manifest pins source commit, image/container digest, model/provider/revision, prompt/policy/tool schema, dataset hash/split/license, evaluator, seed, concurrency, timeout, retries, sample size, exclusions, baseline and authorization scope.
- Deterministic evaluator and machine-readable result schema. Keep raw artifacts access-separated from sanitized reports.
- Queue/worker execution with bounded resources, deadlines, cancellation, idempotency and verified teardown.

## Safety and trust boundaries

Only synthetic targets, owned systems or exact written authorization with expiry. No arbitrary public scans, credential theft, stealth, persistence, exfiltration, destructive actions or DoS. Synthetic credentials, egress deny-by-default, CPU/memory/time/output ceilings and kill switch are mandatory. Treat uploaded artifacts and model/tool output as untrusted; never execute embedded content during ingestion. Trace import is opt-in, minimized, redacted, revocable and time-limited.

## Research integrity and metrics

Every result includes denominators, confidence intervals/variance, failures, exclusions, baseline, limitations and reproduction instructions. Separate exploratory, validation and held-out sets; never tune on held-out data. Measure task success, partial success, citation support, tool correctness, unauthorized action, sensitive disclosure, prompt-injection success, recovery/cancel correctness, p50/p95/p99 latency, tokens and cost per successful task. For inference benchmarks pin hardware/runtime/quantization/serving/batch/cache/prompt/output distribution and warm/cold state.

## Delivery order

1. Typed schemas, experiment manifest, dataset provenance and deterministic evaluator.
2. CLI and reproducible runner for synthetic fixtures.
3. MCP/tool authorization and approval test corpus.
4. RAG isolation/provenance/poisoning experiments.
5. Latency, quality, cost and model comparisons.
6. Report publishing and opt-in sanitized trace ingestion.

## Verification

Test authorization boundaries, malicious artifacts, dataset hash/license validation, deterministic repeatability, runner teardown, egress restrictions, resource limits, cancellation and result schema. UI tests cover chart labels/units, denominator/uncertainty display, responsive tables, keyboard navigation, empty/error states and no-JS report readability. Use Impeccable detector as a design lint, never as a substitute for domain review. Report exact test commands, environment, sample sizes and limitations.
