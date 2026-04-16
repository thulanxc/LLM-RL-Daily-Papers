# RL with Verifiable Rewards (RLVR)

## Evolution
RLHF (2022) → Outcome-Based RL (2024) → DeepSeek-R1 (2025) → RLVR Expansion (2026)

## Core Idea
Instead of learning a reward model from human preferences, use verifiable signals (correct/incorrect answers, passing/failing tests) as reward. Simpler, more scalable, and avoids reward hacking.

## Foundational
- **DeepSeek-R1** (2025). Demonstrated that RLVR with GRPO can produce emergent chain-of-thought reasoning. [2501.12948]
- **DeepSeekMath** — Shao et al. (2024). GRPO with math verification rewards. [2402.03300]

## Recent (April 2026)
- **SUPERNOVA** — Extends RLVR to general reasoning via data curation framework. 52.8% improvement on BBEH. [2604.08477]
- **SD-Zero** — Self-revision converts binary rewards to dense supervision. Sample-efficient, no external teacher. [2604.12002]
- **Imperfect Verifiers** — RLVR robust to 15% verifier noise across 3 model families. [2604.07666]
- **Bidirectional Entropy** — Informative vs. spurious entropy decomposition in RLVR. [2604.04894]
- **Cog-DRIFT** — Cognitive reformulation turns hard problems into solvable variants. [2604.04767]
- **Self-Distilled RLVR** — Token-level self-distillation for update magnitude + RLVR for direction. [2604.03128]
- **PubSwap** — Federated RLVR with public-data off-policy coordination. [2604.12160]
- **NExt** — Low-rank trajectory extrapolation for RLVR acceleration (37.5% savings). [2604.11446]
- **Negotiation RLVR** — Verifiable rewards for strategic negotiation. [2604.09855]
- **PerMix-RLVR** — Preserving persona expressivity under RLVR training. [2604.08986]

## Key Trend
RLVR is expanding beyond math/code to general reasoning (SUPERNOVA), negotiation, and multimodal tasks. The "imperfect verifier" result lowers the barrier for new domains.
