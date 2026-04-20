# Contribution Guidelines

Thank you for taking the time to contribute. Please read this document before opening a pull request.

## The List's Scope

This list curates **open-weight language models** — models where weights are publicly downloadable — and the tools practitioners need to evaluate, deploy, and fine-tune them.

**In scope:**
- Models with publicly downloadable weights
- Inference tools, servers, and runtimes specifically for open-weight models
- Fine-tuning frameworks
- Evaluation benchmarks and tools
- Deployment infrastructure
- Community resources and leaderboards

**Out of scope:**
- API-only models without public weights (GPT-4o, Claude, Gemini Pro, etc.)
- Models announced but not yet released (weights must be downloadable)
- General ML tools not specific to language model inference or fine-tuning
- Papers without accompanying public code or weights

## Adding a Model

Every model entry must include:

| Field | Required | Notes |
| :--- | :---: | :--- |
| Model name | ✅ | Exact name as on HuggingFace |
| Parameter count | ✅ | In B (billions) |
| Context window | ✅ | In K or M tokens |
| License | ✅ | Exact SPDX identifier (e.g. `Apache-2.0`, `MIT`) |
| HuggingFace link | ✅ | Link to model card |
| Key strengths | ✅ | One short phrase |
| Best use case | ✅ | One short phrase |

**Do not add** models to the Quick Pick or per-task recommendation tables without benchmark evidence. Include the source in your PR description.

## Adding a Tool or Resource

Tools must be:
- Open source, **or** have a documented free tier
- Actively maintained (commit within the last 6 months)
- Genuinely useful to practitioners building with open-weight models
- Not just a demo or proof of concept

Link format: `[Tool Name](url) — one-line description.`

## Benchmark Numbers

All benchmark numbers must cite a verifiable source:
- Model technical report (link to arXiv)
- Open LLM Leaderboard v3
- LM Arena / Chatbot Arena
- BigCodeBench / SWE-bench official leaderboards

Include the source URL in your PR description. Numbers sourced only from a vendor's marketing page are not accepted.

## Pull Request Checklist

Before opening a PR, verify:

- [ ] No duplicate entries (search the README first)
- [ ] Links are live and go to the correct destination
- [ ] Descriptions are neutral — no marketing language ("revolutionary", "state-of-the-art" without evidence)
- [ ] New models include license, parameter count, and context window
- [ ] Benchmark numbers include a cited source in the PR description
- [ ] No entries for unreleased models
- [ ] No vendor-sponsored placements without explicit disclosure

## Updating Existing Entries

For corrections (wrong benchmark numbers, changed license, updated VRAM requirements):
- Open a PR with the change and cite the source
- For license changes, link to the official announcement

## What Gets Rejected

- Entries without verifiable benchmark evidence in recommendation tables
- Models without public weights (API-only)
- Tools that haven't been updated in over a year
- Duplicate entries
- Self-promotion without independent community adoption evidence
- Entries with dead links

## License

By contributing to this list, you agree to release your contribution under the [CC0 license](LICENSE).
