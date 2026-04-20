# Awesome Open-Weight Models [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A practitioner-first guide to open-weight language models: benchmarks, licensing, hardware requirements, deployment stacks, and per-task recommendations — curated for engineers shipping real products.

**Not a paper list. Not a hype list. A decision-making tool.**

Every entry answers: *should I use this model for my use case, and how?*

---

## Contents

- [Why This List](#why-this-list)
- [Model Families](#model-families)
  - [Qwen (Alibaba)](#qwen-alibaba)
  - [Gemma (Google)](#gemma-google)
  - [Llama (Meta)](#llama-meta)
  - [DeepSeek](#deepseek)
  - [Mistral](#mistral)
  - [GLM (Zhipu AI)](#glm-zhipu-ai)
  - [Phi (Microsoft)](#phi-microsoft)
  - [Command R (Cohere)](#command-r-cohere)
- [Benchmark Comparison Tables](#benchmark-comparison-tables)
- [Licensing Guide](#licensing-guide)
- [Hardware Requirements](#hardware-requirements)
- [Per-Task Recommendations](#per-task-recommendations)
- [Deployment Stacks](#deployment-stacks)
- [Quantization Guide](#quantization-guide)
- [Fine-Tuning Resources](#fine-tuning-resources)
- [Evaluation Tools](#evaluation-tools)
- [Community & Leaderboards](#community--leaderboards)
- [Contributing](#contributing)

---

## Why This List

April 2026 is the most competitive month in open-source AI history. In a single quarter, six major labs shipped Apache 2.0-licensed frontier models that rival proprietary alternatives:

| Model | Lab | License | Release |
|---|---|---|---|
| Qwen 3.5 | Alibaba | Apache 2.0 | Mar 2026 |
| Gemma 4 | Google DeepMind | Apache 2.0 | Apr 2, 2026 |
| Llama 4 | Meta | Llama 4 Community | Mar 2026 |
| DeepSeek V4 | DeepSeek | MIT | Feb 2026 |
| Mistral Small 4 | Mistral AI | Apache 2.0 | Mar 2026 |
| GLM-5.1 | Zhipu AI | Apache 2.0 | Apr 2026 |

Developers face an impossible evaluation problem. This list is the single authoritative reference.

---

## Model Families

### Qwen (Alibaba)

**License**: Apache 2.0 across all sizes. Most commercially deployed open-weight family globally.

| Model | Params | Context | Strengths | Best For |
|---|---|---|---|---|
| Qwen3.5-0.5B | 0.5B | 32K | Edge, embedding | On-device, IoT |
| Qwen3.5-1.8B | 1.8B | 32K | Tiny but capable | Mobile, edge inference |
| Qwen3.5-7B | 7B | 128K | Multilingual, coding | General dev tasks |
| Qwen3.5-14B | 14B | 128K | Code + reasoning | Production coding agents |
| Qwen3.5-32B | 32B | 128K | Near-frontier | Best open model under 70B |
| Qwen3.5-72B | 72B | 128K | Frontier-class | Production RAG, complex reasoning |
| Qwen3.5-VL-7B | 7B | 128K | Vision-language | Multimodal apps |
| Qwen3.5-VL-72B | 72B | 128K | Best open VLM | Document understanding, OCR |
| QwQ-32B | 32B | 128K | Extended thinking | Math, hard reasoning |

**Resources**
- [Official HuggingFace org](https://huggingface.co/Qwen)
- [Qwen Blog](https://qwenlm.github.io/)
- [Qwen2.5 Technical Report](https://arxiv.org/abs/2412.15115) — still most complete reference
- [Awesome Qwen](https://github.com/QwenLM/awesome-qwen) — official resource list

**Deployment notes**: Qwen family has the best GGUF quantization support. Q4_K_M recommended sweet spot for quality/speed.

---

### Gemma (Google)

**License**: Apache 2.0 (Gemma 4 onward). Major shift from prior Gemma license restrictions.

| Model | Params | Context | Strengths | Best For |
|---|---|---|---|---|
| Gemma4-2B | 2B | 32K | Tiny, quality-dense | Edge, classification |
| Gemma4-7B | 7B | 128K | Reasoning, instruction-following | Chatbots, RAG |
| Gemma4-27B | 27B | 128K | Near-GPT-4o level | Production apps |
| Gemma4-70B | 70B | 128K | Frontier | Enterprise deployments |
| Gemma4-27B-IT | 27B | 128K | Instruct-tuned | RLHF-ready baseline |
| ShieldGemma-2 | 9B | — | Safety classification | Content moderation |

**Resources**
- [Gemma on HuggingFace](https://huggingface.co/google/gemma)
- [Google AI for Developers — Gemma](https://ai.google.dev/gemma)
- [Gemma 4 Technical Report](https://ai.google.dev/gemma/docs/gemma4)
- [Gemma.cpp](https://github.com/google/gemma.cpp) — C++ inference, edge deployment

**Deployment notes**: Best-in-class JAX/TPU performance. For GPU inference, use with vLLM or Ollama. Gemma4-27B fits in 24GB VRAM at Q4.

---

### Llama (Meta)

**License**: Llama 4 Community License — free for products under 700M MAU. Not Apache 2.0.

| Model | Params | Context | Strengths | Best For |
|---|---|---|---|---|
| Llama 4 Scout 17B | 17B (MoE) | 10M | Huge context, multimodal | Document analysis |
| Llama 4 Maverick 17B | 17B (MoE) | 1M | Balanced, multimodal | General purpose |
| Llama 3.3 70B | 70B | 128K | Mature ecosystem | Production, widest tool support |
| Llama 3.2 3B | 3B | 128K | Lightweight | On-device, iOS/Android |
| Llama 3.2 11B Vision | 11B | 128K | Vision | Image understanding |

> **License Warning**: Llama 4 Community License restricts use if your product has >700M monthly active users. Meta must approve large-scale deployments. For unrestricted commercial use, prefer Apache 2.0 models (Qwen, Gemma 4, DeepSeek).

**Resources**
- [Meta Llama official](https://llama.meta.com/)
- [Llama on HuggingFace](https://huggingface.co/meta-llama)
- [awesome-llama](https://github.com/imaurer/awesome-decentralized-llama) — ecosystem resources
- [Llama.cpp](https://github.com/ggml-org/llama.cpp) — gold standard CPU/GPU inference

---

### DeepSeek

**License**: MIT on most models. Fully permissive, no usage restrictions.

| Model | Params | Context | Strengths | Best For |
|---|---|---|---|---|
| DeepSeek-V4 | 685B (MoE) | 128K | Frontier reasoning | Self-hosted frontier API replacement |
| DeepSeek-V4-0324 | 685B (MoE) | 128K | Updated, stronger | Coding, math, analysis |
| DeepSeek-R2 | 671B (MoE) | 128K | Chain-of-thought | Hard reasoning tasks |
| DeepSeek-Coder-V3 | 33B | 128K | Code-specialized | Code generation, review |
| DeepSeek-V4-Lite | 16B (MoE) | 128K | Fast, efficient | Low-latency inference |

> **Self-hosting note**: Full DeepSeek-V4 requires 8× H100 80GB. For smaller setups, use DeepSeek-V4-Lite or run via compatible API providers that serve the full model.

**Resources**
- [DeepSeek on HuggingFace](https://huggingface.co/deepseek-ai)
- [DeepSeek GitHub](https://github.com/deepseek-ai)
- [DeepSeek-V3 Technical Report](https://arxiv.org/abs/2412.19437) — MoE architecture deep dive

---

### Mistral

**License**: Apache 2.0 (Mistral Small 4 onward). Earlier models have custom "Mistral AI Non-Production" license — check before commercial use.

| Model | Params | Context | Strengths | Best For |
|---|---|---|---|---|
| Mistral Small 4 | 22B | 128K | Efficiency king, function calling | Agentic workflows, tool use |
| Mistral-7B-v0.3 | 7B | 32K | Mature, widely supported | Starter model, fine-tuning base |
| Mixtral-8x7B | 56B (MoE) | 32K | Fast MoE inference | High-throughput inference |
| Mixtral-8x22B | 141B (MoE) | 65K | High capability | Complex tasks, low serving cost |
| Codestral | 22B | 32K | Code-specialized, FIM | Code completion (Copilot replacement) |
| Mistral-Nemo | 12B | 128K | NVIDIA partnership | Edge-to-cloud continuity |

**Resources**
- [Mistral AI on HuggingFace](https://huggingface.co/mistralai)
- [Mistral Documentation](https://docs.mistral.ai/)
- [Mistral Cookbook](https://github.com/mistralai/cookbook) — recipes and examples

---

### GLM (Zhipu AI)

**License**: Apache 2.0 (GLM-5.1).

| Model | Params | Context | Strengths | Best For |
|---|---|---|---|---|
| GLM-5.1-9B | 9B | 128K | Bilingual (EN/ZH), fast | Chinese-English applications |
| GLM-5.1-32B | 32B | 128K | Strong reasoning | Competitive with Qwen 32B |
| GLM-4V | 9B | 8K | Vision + Chinese | Document OCR, Chinese multimodal |
| CogVideoX | — | — | Video generation | Video AI applications |

**Resources**
- [Zhipu on HuggingFace](https://huggingface.co/THUDM)
- [ChatGLM GitHub](https://github.com/THUDM/ChatGLM3)

---

### Phi (Microsoft)

**License**: MIT.

| Model | Params | Context | Strengths | Best For |
|---|---|---|---|---|
| Phi-4 | 14B | 16K | Best-in-class at size | Mobile, constrained compute |
| Phi-4-mini | 3.8B | 16K | Tiny but punches up | On-device reasoning |
| Phi-4-multimodal | 5.6B | 128K | Vision + audio | Edge multimodal |

**Resources**
- [Phi on HuggingFace](https://huggingface.co/microsoft/phi-4)
- [Phi-4 Technical Report](https://arxiv.org/abs/2412.08905)

---

### Command R (Cohere)

**License**: CC-BY-NC-4.0 for research, commercial license required for production.

| Model | Params | Context | Strengths | Best For |
|---|---|---|---|---|
| Command R+ | 104B | 128K | RAG-optimized, citations | Enterprise RAG |
| Command R | 35B | 128K | Efficient RAG | Production RAG at scale |

**Resources**
- [Cohere on HuggingFace](https://huggingface.co/CohereForAI)

---

## Benchmark Comparison Tables

### General Reasoning (MMLU-Pro / GPQA Diamond)

| Model | MMLU-Pro | GPQA Diamond | Notes |
|---|---|---|---|
| DeepSeek-V4-0324 | 81.2 | 71.5 | Frontier open model |
| Qwen3.5-72B | 79.4 | 68.3 | Best Apache 2.0 at size |
| Gemma4-70B | 78.9 | 67.1 | Google's flagship |
| Llama 4 Maverick 17B | 73.5 | 59.2 | MoE efficiency |
| Qwen3.5-32B | 75.1 | 63.8 | Best <40B model |
| Mistral Small 4 | 68.3 | 55.7 | Efficiency leader |
| QwQ-32B | 76.4 | 65.9 | Extended thinking |

### Coding (HumanEval+ / SWE-bench Verified)

| Model | HumanEval+ | SWE-bench | Notes |
|---|---|---|---|
| DeepSeek-Coder-V3 | 92.1 | 49.6 | Best open coder |
| Qwen3.5-72B | 90.8 | 46.3 | Strong general + code |
| Qwen3.5-32B | 88.4 | 42.1 | Best <40B coder |
| Codestral 22B | 87.9 | 40.5 | FIM, completion-optimized |
| Gemma4-27B | 84.2 | 38.7 | Solid Google baseline |
| Llama 3.3 70B | 83.6 | 37.2 | Mature ecosystem |

### Math (AIME 2024 / 2025)

| Model | AIME 2024 | AIME 2025 | Notes |
|---|---|---|---|
| DeepSeek-R2 | 79.8 | 72.1 | CoT specialist |
| QwQ-32B | 72.4 | 65.3 | Best open reasoning model |
| DeepSeek-V4-0324 | 68.9 | 61.2 | Strong general model |
| Qwen3.5-72B | 63.1 | 56.8 | Competitive |
| Gemma4-70B | 58.4 | 51.9 | Improving |

### Multilingual (FLORES+ benchmark)

| Model | EN | ZH | DE | FR | JA | AR |
|---|---|---|---|---|---|---|
| Qwen3.5-72B | 94.1 | 91.8 | 88.3 | 87.9 | 86.2 | 82.4 |
| GLM-5.1-32B | 91.2 | 93.4 | 82.1 | 81.8 | 80.5 | 76.3 |
| Gemma4-70B | 93.8 | 85.2 | 87.9 | 88.4 | 84.1 | 79.8 |
| Llama 3.3 70B | 93.5 | 81.9 | 86.2 | 87.1 | 82.3 | 77.4 |

> **Source**: Results drawn from model technical reports, LM Arena leaderboard, and Open LLM Leaderboard v3. Always run your own evals on your domain before shipping to production.

---

## Licensing Guide

This table answers: *can I use this commercially without restrictions?*

| Model Family | License | Commercial Use | Derivative Works | Attribution Required | User Limit |
|---|---|---|---|---|---|
| Qwen 3.5 | Apache 2.0 | ✅ Unrestricted | ✅ Yes | ✅ Yes | None |
| Gemma 4 | Apache 2.0 | ✅ Unrestricted | ✅ Yes | ✅ Yes | None |
| DeepSeek V4 | MIT | ✅ Unrestricted | ✅ Yes | ✅ Yes | None |
| Mistral Small 4 | Apache 2.0 | ✅ Unrestricted | ✅ Yes | ✅ Yes | None |
| GLM-5.1 | Apache 2.0 | ✅ Unrestricted | ✅ Yes | ✅ Yes | None |
| Phi-4 | MIT | ✅ Unrestricted | ✅ Yes | ✅ Yes | None |
| Llama 4 | Community License | ⚠️ Restricted | ⚠️ Restricted | ✅ Yes | 700M MAU cap |
| Llama 3.x | Community License | ⚠️ Restricted | ⚠️ Restricted | ✅ Yes | 700M MAU cap |
| Mixtral / Mistral 7B | Apache 2.0 | ✅ Unrestricted | ✅ Yes | ✅ Yes | None |
| Command R+ | CC-BY-NC-4.0 | ❌ Non-commercial | ⚠️ CC terms | ✅ Yes | Commercial license required |
| Gemma 1/2 | Gemma License | ⚠️ Restricted | ⚠️ Restricted | ✅ Yes | Check terms |

> **Key rule**: For fully permissive commercial deployment with no headaches, default to Apache 2.0 or MIT models. Qwen 3.5, Gemma 4, DeepSeek, and Mistral Small 4 are all safe choices.

---

## Hardware Requirements

### Minimum GPU VRAM to Run (BF16 / FP16)

| Model | Params | BF16 VRAM | Comfortable Setup |
|---|---|---|---|
| Qwen3.5-0.5B | 0.5B | 1 GB | Any modern GPU |
| Phi-4-mini | 3.8B | 8 GB | RTX 3070 / M2 |
| Qwen3.5-7B | 7B | 14 GB | RTX 3080 / M2 Pro |
| Mistral Small 4 | 22B | 44 GB | 2× RTX 3090 |
| Qwen3.5-32B | 32B | 64 GB | 2× A100 40GB |
| Gemma4-27B | 27B | 54 GB | 2× RTX 4090 |
| Qwen3.5-72B | 72B | 144 GB | 2× A100 80GB |
| DeepSeek-V4 | 685B | 1.4 TB | 8× H100 80GB |
| Llama 4 Scout 17B | 17B MoE | 38 GB | 2× RTX 4090 |

### With Quantization (Q4_K_M GGUF)

| Model | BF16 VRAM | Q4_K_M VRAM | Quality Loss |
|---|---|---|---|
| Qwen3.5-7B | 14 GB | ~5 GB | Minimal |
| Qwen3.5-32B | 64 GB | ~20 GB | Low |
| Qwen3.5-72B | 144 GB | ~45 GB | Moderate |
| Llama 3.3 70B | 140 GB | ~43 GB | Moderate |
| DeepSeek-Coder-V3 | 66 GB | ~22 GB | Low |

### CPU-Only Inference (Ollama / llama.cpp)

Viable for development and light production up to ~13B models. Expect 5–15 tokens/sec on modern Apple Silicon (M3 Max+).

| Hardware | Max Model Size | Notes |
|---|---|---|
| M3 Ultra (192GB) | 100B+ | Excellent for large open models |
| M3 Max (48GB) | 32B Q4 | Good production option |
| M3 Pro (36GB) | 20B Q4 | Solid dev workstation |
| M2 (16GB) | 7B Q4 | Adequate for development |
| High-end x86 + RAM | 70B+ (slow) | RAM bandwidth bottleneck |

---

## Per-Task Recommendations

### Coding Assistance

| Use Case | Best Choice | Runner-Up | Notes |
|---|---|---|---|
| Code generation (general) | DeepSeek-Coder-V3 33B | Qwen3.5-32B | DeepSeek specialized; Qwen more balanced |
| Code completion (FIM) | Codestral 22B | Qwen3.5-7B | Codestral built for FIM |
| Bug fixing / refactoring | Qwen3.5-72B | DeepSeek-V4 | Long context, strong reasoning |
| Small model code | Qwen3.5-7B | Phi-4-mini | Best at size bracket |
| SWE-bench / agent coding | DeepSeek-V4-0324 | Qwen3.5-72B | Highest SWE-bench open scores |

### Reasoning & Math

| Use Case | Best Choice | Runner-Up | Notes |
|---|---|---|---|
| Hard math (AIME-level) | DeepSeek-R2 | QwQ-32B | CoT specialists |
| General reasoning | DeepSeek-V4 | Qwen3.5-72B | Frontier reasoning |
| Fast reasoning (<40B) | QwQ-32B | Qwen3.5-32B | Best compact reasoner |
| Scientific QA | DeepSeek-V4 | Gemma4-70B | GPQA performance |

### Multilingual Applications

| Use Case | Best Choice | Runner-Up | Notes |
|---|---|---|---|
| Chinese-English | Qwen3.5-72B | GLM-5.1-32B | Qwen trained heavily on Chinese |
| European languages | Gemma4-70B | Mistral Small 4 | Strong EU language support |
| Japanese | Qwen3.5-32B | Gemma4-27B | Both strong; Qwen leads |
| Arabic | Qwen3.5-72B | Gemma4-70B | Qwen best Arabic open model |
| General multilingual | Qwen3.5-72B | — | Best overall multilingual open model |

### Vision & Multimodal

| Use Case | Best Choice | Runner-Up | Notes |
|---|---|---|---|
| Document OCR / understanding | Qwen3.5-VL-72B | Gemma4-27B | Qwen VL best open VLM |
| Image QA | Qwen3.5-VL-7B | Llama 4 Scout | Efficient, strong |
| Video understanding | GLM-5.1 + CogVideoX | Llama 4 Scout | Llama Scout has video context |
| Chinese document OCR | GLM-4V | Qwen3.5-VL | GLM stronger on Chinese docs |

### RAG & Long Context

| Use Case | Best Choice | Runner-Up | Notes |
|---|---|---|---|
| Enterprise RAG | Command R+ | Qwen3.5-72B | Command R+ citation-tuned |
| Long context (1M+ tokens) | Llama 4 Scout 17B | Gemma4-70B | Scout has 10M context |
| On-device RAG | Qwen3.5-7B | Phi-4 | Both fit 16GB VRAM |

### Agentic / Tool Use

| Use Case | Best Choice | Runner-Up | Notes |
|---|---|---|---|
| Function calling | Mistral Small 4 | Qwen3.5-32B | Mistral optimized for tool use |
| Multi-step agent | Qwen3.5-72B | DeepSeek-V4 | Best planning + instruction-following |
| Lightweight agent | Qwen3.5-7B | Mistral-7B | Tool calling at 7B scale |
| Code agent | DeepSeek-Coder-V3 | Qwen3.5-32B | Highest agent-coding benchmarks |

---

## Deployment Stacks

### Local Inference

| Tool | Models Supported | Use Case | Notes |
|---|---|---|---|
| [Ollama](https://github.com/ollama/ollama) | All major families | Development, personal use | Easiest setup, Mac/Windows/Linux |
| [LM Studio](https://lmstudio.ai/) | All GGUF models | Desktop GUI | Best UX for non-technical users |
| [llama.cpp](https://github.com/ggml-org/llama.cpp) | All GGUF models | Performance, custom | Gold standard, most control |
| [Jan](https://github.com/janhq/jan) | Major families | Desktop app | Open-source LM Studio alternative |
| [GPT4All](https://github.com/nomic-ai/gpt4all) | Quantized models | Offline enterprise | Privacy-first, no cloud |

### Production Inference Servers

| Tool | Strengths | Best For | GPU |
|---|---|---|---|
| [vLLM](https://github.com/vllm-project/vllm) | Highest throughput, PagedAttention | High-traffic APIs | NVIDIA (best), AMD (beta) |
| [TGI (Text Generation Inference)](https://github.com/huggingface/text-generation-inference) | HuggingFace native, streaming | HuggingFace ecosystem | NVIDIA, AMD, Gaudi |
| [SGLang](https://github.com/sgl-project/sglang) | Structured generation, speed | Complex output schemas | NVIDIA |
| [llama.cpp server](https://github.com/ggml-org/llama.cpp) | Low VRAM (quantized), CPU | Edge production | Any |
| [Ollama (serve mode)](https://github.com/ollama/ollama) | Simple API, GGUF | Small teams, dev | Any |
| [ExLlamaV2](https://github.com/turboderp/exllamav2) | Fast GPTQ inference | NVIDIA, quantized | NVIDIA |
| [MLC-LLM](https://github.com/mlc-ai/mlc-llm) | Cross-platform, mobile | iOS/Android/web | Universal |
| [Aphrodite](https://github.com/PygmalionAI/aphrodite-engine) | vLLM fork, long context | Large batches | NVIDIA |

### Cloud / Managed Hosting

| Provider | Notable Models | Pricing Model | Notes |
|---|---|---|---|
| [Groq](https://groq.com/) | Llama, Mistral, Gemma | Per-token | Fastest inference (LPU hardware) |
| [Together AI](https://www.together.ai/) | 50+ open models | Per-token | Best open-model selection |
| [Fireworks AI](https://fireworks.ai/) | Llama, Qwen, Mistral | Per-token | Speed-optimized |
| [Replicate](https://replicate.com/) | Most open models | Per-second | Easy API, serverless |
| [Modal](https://modal.com/) | Any model via custom deploy | Compute time | Infrastructure as code |
| [Vast.ai](https://vast.ai/) | Self-managed H100s | GPU hours | Cheapest H100 access |
| [RunPod](https://runpod.io/) | Self-managed, pod/serverless | GPU hours | Good for large model hosting |
| [Cerebras](https://www.cerebras.net/) | Llama family | Per-token | Extreme speed (CS-3 wafer chip) |
| [Hyperbolic](https://hyperbolic.xyz/) | Llama, Qwen, DeepSeek | Per-token | Low latency, competitive pricing |

---

## Quantization Guide

### Format Comparison

| Format | Tool | VRAM Reduction | Quality | Speed | Best For |
|---|---|---|---|---|---|
| GGUF Q2_K | llama.cpp | ~75% | Poor | Fast | Very constrained RAM |
| GGUF Q4_K_M | llama.cpp | ~55% | Good | Fast | **Recommended default** |
| GGUF Q5_K_M | llama.cpp | ~45% | Very Good | Good | Quality-critical tasks |
| GGUF Q8_0 | llama.cpp | ~20% | Excellent | Moderate | Near-lossless |
| GPTQ 4-bit | AutoGPTQ | ~55% | Good | Fast | NVIDIA production |
| AWQ 4-bit | AutoAWQ | ~55% | Good | Fastest | NVIDIA, high throughput |
| EXL2 | ExLlamaV2 | Variable | Good | Very Fast | NVIDIA, custom bit-rates |
| BnB 4-bit | bitsandbytes | ~55% | Good | Moderate | Quick dev setup |

### Where to Get Quantized Models

- [Bartowski on HuggingFace](https://huggingface.co/bartowski) — best GGUF quantizations, all major models
- [LoneStriker](https://huggingface.co/LoneStriker) — GGUF and EXL2
- [TheBloke](https://huggingface.co/TheBloke) — large GPTQ/GGUF catalog (older models)
- [mradermacher](https://huggingface.co/mradermacher) — GGUF quantizations

---

## Fine-Tuning Resources

### Frameworks

| Tool | Stars | Method | Notes |
|---|---|---|---|
| [Unsloth](https://github.com/unslothai/unsloth) | 28k+ | LoRA/QLoRA | 2× faster, 60% less VRAM; **recommended default** |
| [LLaMA-Factory](https://github.com/hiyouga/LLaMA-Factory) | 38k+ | LoRA/Full/RLHF | Best UI, supports 100+ models |
| [Axolotl](https://github.com/axolotl-ai-cloud/axolotl) | 8k+ | LoRA/Full | Config-file driven, production-ready |
| [TRL (HuggingFace)](https://github.com/huggingface/trl) | 10k+ | RLHF/DPO/GRPO | Reference implementation for alignment |
| [torchtune](https://github.com/pytorch/torchtune) | 5k+ | Full/LoRA | Native PyTorch, easy to customize |
| [ms-swift](https://github.com/modelscope/ms-swift) | 6k+ | LoRA/Full | Strong Qwen support, ModelScope |

### Key Techniques

| Technique | Use Case | Tools | Notes |
|---|---|---|---|
| LoRA | Efficient fine-tuning | Unsloth, Axolotl | Rank 16–64 typical; low VRAM |
| QLoRA | Fine-tune on consumer GPUs | Unsloth, Axolotl | 4-bit base + LoRA adapters |
| DPO | Alignment, preference | TRL | Replace RLHF for most use cases |
| GRPO | Reasoning alignment | TRL, Unsloth | Used in DeepSeek-R1 recipe |
| Full fine-tuning | Maximum quality | torchtune, Axolotl | Needs multi-GPU setup |
| Distillation | Compress large → small | TRL, custom | Teach 7B from 72B outputs |

### Datasets

| Dataset | Size | Use Case | License |
|---|---|---|---|
| [Open-Hermes-2.5](https://huggingface.co/datasets/teknium/OpenHermes-2.5) | 1M | General instruction | Apache 2.0 |
| [Magpie-Pro](https://huggingface.co/datasets/Magpie-Align/Magpie-Pro-1M-v0.1) | 1M | High-quality instruct | Apache 2.0 |
| [UltraFeedback](https://huggingface.co/datasets/openbmb/UltraFeedback) | 250K | DPO/preference | Apache 2.0 |
| [Capybara](https://huggingface.co/datasets/LDJnr/Capybara) | 16K | Reasoning, long-form | Apache 2.0 |
| [SlimOrca](https://huggingface.co/datasets/Open-Orca/SlimOrca) | 500K | Instruction following | MIT |
| [MetaMathQA](https://huggingface.co/datasets/meta-math/MetaMathQA) | 395K | Math reasoning | MIT |
| [CodeFeedback](https://huggingface.co/datasets/m-a-p/CodeFeedback-Filtered-Instruction) | 156K | Code instruction | Apache 2.0 |

---

## Evaluation Tools

| Tool | What It Measures | Notes |
|---|---|---|
| [lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness) | Comprehensive benchmarks | EleutherAI standard, used by Open LLM Leaderboard |
| [HELMET](https://github.com/princeton-nlp/HELMET) | Long-context eval | Best for context window validation |
| [LiveCodeBench](https://github.com/LiveCodeBench/LiveCodeBench) | Coding, contamination-free | Fresh problems, harder to overfit |
| [Braintrust](https://www.braintrust.dev/) | Production eval, LLM-as-judge | Best for custom domain evaluation |
| [Langfuse](https://github.com/langfuse/langfuse) | Tracing + eval in production | Open-source, self-hostable |
| [RAGAS](https://github.com/explodinggradients/ragas) | RAG evaluation | Standard for retrieval-augmented systems |
| [DeepEval](https://github.com/confident-ai/deepeval) | Unit-test-style eval | Developer-friendly, many metrics |
| [PromptFoo](https://github.com/promptfoo/promptfoo) | Red teaming + eval | CI-integrated, adversarial testing |

---

## Community & Leaderboards

### Leaderboards

| Resource | What It Ranks | Notes |
|---|---|---|
| [Open LLM Leaderboard v3](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard) | Open models, standardized benchmarks | HuggingFace canonical leaderboard |
| [LM Arena (Chatbot Arena)](https://lmarena.ai/) | Human preference, blind A/B | Best for real-world quality judgment |
| [BigCodeBench](https://bigcode-bench.github.io/) | Code generation | Best coding leaderboard |
| [SWE-bench Leaderboard](https://www.swebench.com/) | Real GitHub issue resolution | Hardest coding benchmark |
| [SEAL Leaderboard](https://scale.com/leaderboard) | Scale AI's expert evaluation | Strong contamination controls |

### Communities

| Community | Platform | Members | Focus |
|---|---|---|---|
| [r/LocalLLaMA](https://www.reddit.com/r/LocalLLaMA/) | Reddit | 688k+ | Self-hosting, model releases, benchmarks |
| [r/MachineLearning](https://www.reddit.com/r/MachineLearning/) | Reddit | 3M+ | Research, new models |
| [HuggingFace Discord](https://discord.gg/huggingface) | Discord | Active | Model releases, fine-tuning help |
| [EleutherAI Discord](https://discord.gg/eleutherai) | Discord | Active | Open-source training, eval |
| [AI Twitter/X](https://twitter.com/i/lists/1589462940141228038) | X | — | Real-time model releases |

### Tracking New Releases

- [HuggingFace Daily Papers](https://huggingface.co/papers) — research papers same day as arXiv
- [TheAIGrid Newsletter](https://theaigrid.com/) — weekly model release roundup
- [Latent Space Podcast](https://www.latent.space/) — deep technical breakdowns
- [Simon Willison's blog](https://simonwillison.net/) — practitioner notes on new models

---

## Contributing

Contributions welcome. PRs accepted for:

- New model releases with benchmark data
- Hardware requirement corrections
- Deployment stack updates
- New evaluation tools
- Per-task recommendation updates

**Requirements for PRs:**
1. Model entries must include license, parameter count, and context window
2. Benchmark numbers must cite source
3. No vendor-sponsored placements without disclosure
4. No entries for non-released models (announcement ≠ release)

See [CONTRIBUTING.md](CONTRIBUTING.md) for full guidelines.

---

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)

This list is CC0. No rights reserved.
