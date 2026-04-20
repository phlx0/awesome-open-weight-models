# Contributing

## What belongs here

- Open-weight models (weights publicly available for download)
- Tools that work specifically with open-weight models
- Benchmark results with cited sources
- Hardware requirements verified by community testing

## What doesn't belong

- API-only models (GPT-4, Claude, Gemini Pro) — they are not open-weight
- Unverified benchmark claims
- Models with weights not publicly released
- Promotional content without technical substance

## PR format

### Adding a model

```
| Model Name | Params | Context | Strengths | Best For |
```

Include: license, official HuggingFace URL, and at least one benchmark citation.

### Updating benchmark numbers

Always include the source URL in your PR description. Acceptable sources:
- Official technical reports (arXiv preferred)
- Open LLM Leaderboard v3
- LM Arena
- BigCodeBench / SWE-bench official leaderboards

### Adding a tool

Tool must be:
- Open source OR have a documented free tier
- Actively maintained (commit in last 6 months)
- Genuinely useful to practitioners (not a demo)

## Style

- Tables use pipes and dashes only — no HTML
- Links use `[text](url)` format
- Notes column: one short sentence, plain English
- No marketing language ("revolutionary", "state-of-the-art" without benchmark evidence)
