# LLM RL Daily Papers

A curated daily research digest tracking advances in Reinforcement Learning for Large Language Models.

## Overview

This repository maintains a daily digest of papers at the intersection of Reinforcement Learning and Large Language Models. The field has evolved rapidly since the foundational RLHF work (Ouyang et al., 2022), spawning diverse research threads including:

- **Policy Optimization**: PPO, DPO, GRPO, DAPO, and their many variants
- **RL with Verifiable Rewards (RLVR)**: Training with outcome-verifiable reward signals
- **Reward Modeling**: Process reward models, outcome reward models, generative reward models
- **Reasoning RL**: Training reasoning/thinking capabilities through RL
- **Agentic RL**: Multi-turn agent training with RL, tool use, code generation
- **Alignment**: RLHF, RLAIF, Constitutional AI, preference optimization
- **Training Infrastructure**: Efficient RL training, distributed systems, quantization
- **Multimodal RL**: Extending RL training to vision-language and omni-modal models

## Daily Digests

| Date | Papers | Highlights |
|------|--------|------------|
| [2026-04-19](newspaper/2026-04-19.html) | +20 | **IG-Search (2604.15148)** turns gold-answer log-prob info-gain into a training-free step-level reward inside GRPO; **CW-GRPO (2604.14267)** rescales outcome advantages with LLM-judge per-round contribution scores (+6.3% on Qwen3-1.7B); **GFT (2604.14258)** reframes SFT as PG-with-sparse-implicit-reward, fixes it with Group Advantage + Dynamic Coefficient Rectification; **VGF (2604.14265)** replaces KL regularization with Optimal Transport + Gradient Flow; **TC-GRPO (RAD-2, 2604.15308)** adds temporal consistency to group-relative advantage; **TCER (2604.11522)** extends RLVR to open-ended writing via relative info gain; **MindDR (2604.14518)** — 30B production-scale three-agent deep-research with four-stage SFT/Search-RL/Report-RL/Preference training; **MARS² (2604.14564)** extends group-relative advantage to multi-agent shared search trees; **TREX (2604.14116)** automates the full LLM fine-tuning loop with tree-search agents + FT-Bench; **RadAgent / RaTA-Tool / APEX-MEM** broaden agentic RL to 3D medical, multimodal tool retrieval, and long-term conversational memory; **IUQ / Cross-Query Contradictions / IE-as-Cache** give claim-level, set-level, cache-based verifier signals; **LongCoT (2604.14140)** benchmark exposes <10% accuracy on 10k–100k-token reasoning for GPT-5.2 / Gemini 3 Pro |
| [2026-04-17](newspaper/2026-04-17.html) | +13 | **PreRL (2604.14142)** opens Pre-train-Space RL with Negative-Sample Reinforcement (14.89× reflection boost); **CAPO** fixes GRPO's calibration collapse via AUC surrogate; **SPO** (MM-Doc-R1) challenges GRPO's shared-baseline assumption in multi-turn; **Decoupled Multi-Objective GRPO** (ToolOmni) separates retrieval/execution advantages; **Causal-Decomposition RM** / **C2 Rubric RM** / **Sycophancy Calibration Collapse** form a complete reward-hacking matrix; **CRAFT** builds Reasoning-KG for CoT synthesis; **Shortest-Path Generalization** shows RL stabilizes but doesn't expand capability |
| [2026-04-16 深夜版 · Night Edition](newspaper/2026-04-16-night-edition.html) | +19 | **New**: Reward Hacking survey (4-level taxonomy + DPO Reward Collapse); MEDS memory-enhanced dynamic reward shaping; E³-TIR three-experience fusion warm-up; ATTC adaptive tool trust calibration; PTE hardware-aware TIR efficiency; Self-Guide policy-reward co-evolution; LangMARL language-space MARL; MIA memory intelligence agent with alternating RL; MedVR annotation-free visual reasoning (EVR+CCA); Saliency-R1; QuarkMedSearch; ReasonXL multilingual SFT+RLVR; CARO DPO analogy reasoning; Frontier-Eng engineering benchmark; SandMLE micro-scale MLE sandbox |
| [2026-04-16 晚间增刊 · Late Edition](newspaper/2026-04-16-late-edition.html) | +19 | RAGEN-2 diagnoses Template Collapse via Mutual Information; PROGRS outcome-conditioned PRM centering; Process Reward Agents as test-time plug-in; TInR internalizes tool knowledge; CURE claim-level factuality calibration; KG-Reasoner & TRACE reshape multi-hop KGQA; OOM-RL uses capital loss as alignment signal |
| [2026-04-16](newspaper/2026-04-16.html) | 45 | Inaugural edition. SD-Zero for sample-efficient RL, Relax async RL engine, SKPO skip-connected credit assignment, GrandCode beats all humans in competitive programming, SUPERNOVA extends RLVR to general reasoning |

## Repository Structure

```
LLM-RL-Daily-Papers/
├── README.md                  # This file — living index and field overview
├── newspaper/                 # Daily HTML digests
│   └── YYYY-MM-DD.html       # One file per day
└── taxonomy/                  # Research thread organization
    ├── README.md              # Research direction map
    └── threads/               # Individual research threads
```

## Landmark Papers

The field is built on several foundational works:

| Paper | Year | Contribution |
|-------|------|-------------|
| [InstructGPT](https://arxiv.org/abs/2203.02155) (Ouyang et al.) | 2022 | Foundational RLHF pipeline: SFT → Reward Model → PPO |
| [Constitutional AI](https://arxiv.org/abs/2212.08073) (Bai et al.) | 2022 | RLAIF — AI feedback replaces human feedback |
| [DPO](https://arxiv.org/abs/2305.18290) (Rafailov et al.) | 2023 | Direct preference optimization without explicit RL |
| [Let's Verify Step by Step](https://arxiv.org/abs/2305.20050) (Lightman et al.) | 2023 | Process reward models for mathematical reasoning |
| [STaR](https://arxiv.org/abs/2203.14465) (Zelikman et al.) | 2022 | Self-taught reasoning through bootstrapping |
| [DeepSeekMath / GRPO](https://arxiv.org/abs/2402.03300) (Shao et al.) | 2024 | Group Relative Policy Optimization |
| [KTO](https://arxiv.org/abs/2402.01306) (Ethayarajh et al.) | 2024 | Prospect-theoretic preference optimization |
| [DeepSeek-R1](https://arxiv.org/abs/2501.12948) | 2025 | RL-based reasoning model with emergent CoT |
| [DAPO](https://arxiv.org/abs/2503.14476) | 2025 | Open-source LLM RL system at scale |
| [Dr. GRPO](https://arxiv.org/abs/2503.20783) | 2025 | Improved GRPO for reasoning training |
| [REINFORCE++](https://arxiv.org/abs/2501.03262) (Hu) | 2025 | Simplified RL baseline for LLMs |

## How to Use

1. **Daily reading**: Open the latest `newspaper/YYYY-MM-DD.html` in your browser for a newspaper-style digest
2. **Research threads**: Check `taxonomy/README.md` to understand how papers connect across research directions
3. **Historical lookup**: Browse past digests in the `newspaper/` directory

## Contributing

This digest is generated by an AI research analyst. If you notice errors or missing papers, please open an issue.

## License

Content is provided for research purposes. All papers are linked to their original arXiv entries.
