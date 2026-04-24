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

## April 22, 2026 additions

- **ARES** [2604.18789, ACL 2026] — First red-teaming framework jointly attacking Policy and Reward Model. Introduces "systemic weakness" concept: cases where policy AND RM fail in tandem. Safety Mentor dynamically composes attacks from structured components (topic/persona/tactic/goal) and ends-to-end repairs both Policy and RM.
- **CoAct** [2604.17501] — Co-Active preference learning synergizing self-rewarding + active learning. Uses self-consistency to identify reliable self-labeled data vs. oracle-verification candidates; oracle feedback also guides generation of new within-capability instructions. +13.25% GSM8K, +8.19% MATH, +13.16% WebInstruct.
- **Abstain-R1** [2604.17073] — RLVR for calibrated abstention. Novel "clarification-aware" reward: rewards correct answers on answerable queries AND explicit abstention + semantically-aligned post-refusal clarification on unanswerable ones. 3B model achieves both behaviors simultaneously.
- **UA-Bench + RL Training** [2604.17293] — Distinguishes data uncertainty (input ambiguity) from model uncertainty (capability limits). 3,500+ benchmark; 18 frontier LLMs struggle. RL training on math-only synthetic data yields cross-domain generalization for uncertainty classification.
- **CiPO** [2604.15847] — Counterfactual-CoT machine unlearning for large reasoning models. Reframes unlearning as targeted intervention on CoT traces via iterative preference optimization on counterfactual reasoning. Preserves reasoning while completely removing target knowledge.

### Key Trend (April 22): Honesty Becomes an Optimization Target

All five papers above push "epistemic honesty" to the training objective:
- Abstain-R1: know *why* you don't know
- UA-Bench: distinguish *what kind* of uncertainty
- CoAct: know *which* self-labels to trust
- ARES: know *jointly* where policy+RM fail
- CiPO: know *how* to forget without destroying reasoning

This shifts alignment from "avoid harmful output" toward "calibrate confidence and scope of knowledge."

## April 24, 2026 additions

- **Adaptive Instruction Composition** [2604.21159] (Capital One) — Automated red-teaming framed as RL over a *combinatorial space of crowdsourced instructions*, jointly optimizing effectiveness × diversity. Outperforms random combination under target-model transfer. Marks the transition of automated red-teaming from "template enumeration" to "RL-driven combinatorial exploration."
- **IRM — Implicit Reward Model detection** [2604.21223] (NeurIPS 2025 Poster) — Uses `log p_{aligned}(x) - log p_{base}(x)` (the DPO implicit reward) as a zero-training AI-text detector. No preference data, no additional training. Evidence that alignment leaves a measurable "imprint" that can be read off by comparing instruct-tuned and base models.

### Connections
- Adaptive Red-Team ↔ ARES (2604.18789): both frame red-teaming as RL, but ARES attacks *policy + reward model jointly*, while Adaptive Composition optimizes over attack-text combinatorics.
- IRM ↔ GroupDPO (2604.15602) / DDO-RM (2604.11119): all exploit the implicit-reward view of DPO, but IRM turns it outward (detection) rather than inward (optimization).
