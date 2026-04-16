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
