# Architecture (planned)

- `packages/<lab>` per lab; `packages/trace-schema` shared (span-style records: step, tool, inputs/outputs, tokens, cost, timing).
- Evals run via CLI and in CI; results stored as versioned JSON next to the code that produced them.
- Break My Agent: fake tools only, per-attempt budget, rate limits and credits; attempts logged without personal data.
- Reproducibility: pinned model IDs, seeds where supported, recorded provider responses for replay.