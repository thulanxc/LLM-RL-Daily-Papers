# Alignment & Personalization

## Evolution
RLHF (2022) → Constitutional AI (2022) → DPO (2023) → Multi-Objective (2025) → Personalization (2026)

## Foundational
- **InstructGPT** — Ouyang et al. (2022). Foundational RLHF pipeline. [2203.02155]
- **Constitutional AI** — Bai et al. (2022). RLAIF with AI feedback. [2212.08073]
- **DPO** — Rafailov et al. (2023). Preference optimization without RL loop. [2305.18290]
- **KTO** — Ethayarajh et al. (2024). Prospect-theoretic alignment. [2402.01306]

## Recent (April 2026)
- **SPARD** — Self-paced curriculum for RL alignment. Dynamic reward weighting. [2604.07837]
- **PALM** — Portfolio of policies for multi-preference personalization. [2604.04144]
- **PerMix-RLVR** — Preserving persona expressivity under RLVR. [2604.08986]
- **VRF** — Variational reward factorization for user-level personalization. [2604.00997]
- **Decomposing the Delta** — What models learn from preference pairs. [2604.08723]
- **RLHF Statistical Perspective** — Rigorous statistical foundations. [2604.02507]

## Key Trend
Alignment is shifting from "one model fits all" to personalization. PALM, VRF, and PerMix-RLVR all address how to serve diverse user preferences without training separate models. The portfolio approach (PALM) and factorized rewards (VRF) are complementary strategies.

## Morning Edition (April 21) — 对齐理论与个性化新增

- **Demystifying Online Alignment** [2604.17207] — Enoch H. Kang shows that the O(log T) KL-regularized regret bounds for online RLHF / online DPO conflate learning cost with exploration randomness. Under a *decision-centric regret* (only evaluate the top-ranked response at inference), standard greedy online alignment achieves **constant O(1) cumulative regret**. First formal explanation for why these simple algorithms empirically work.
- **HorizonBench** [2604.17283] — 4,245 evaluation items from 360 simulated users with 6-month dialogues (avg ~163K tokens). Data generator uses a structured mental-state graph where typed life-event edges drive preference changes. Identifies "belief-update failure" as a targetable deficit in modern LLMs — testbed for long-context personalization, memory-augmented architectures, theory-of-mind reasoning.
- **Rejection Criterion for Proxy Alignment** [2604.16146] — Principled rejection criterion for BoN / rejection-sampling test-time alignment; characterizes the alignment-efficiency Pareto frontier analytically and outperforms fixed-threshold BoN.

### Connections
- Demystifying ↔ Shortest-Path Generalization (April 17): both theoretical works constraining the explanatory scope of RL/alignment methods.
- HorizonBench ↔ APEX-MEM / MIA: HorizonBench supplies the evaluation axis that memory-augmented agents urgently need.
- Rejection Criterion ↔ Flexible Empowerment BoN (2604.15614) ↔ RCFG (2604.15577): three ways test-time RL is being formalized beyond hand-tuned BoN.
