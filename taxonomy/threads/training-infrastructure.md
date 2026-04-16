# Training Infrastructure & Efficiency

## Evolution
Single-GPU RL (2022) → veRL (2024) → AReaL (2025) → Async/Quantized/Efficient (2026)

## Core Challenge
RL training for LLMs is 3-10x more expensive than SFT due to rollout generation. Efficiency improvements directly expand the frontier of what's trainable.

## Recent (April 2026)
- **Relax** — Async omni-modal RL engine. 2x speedup, fault-isolated services. [2604.11554]
- **Experience Replay** — 40% compute savings from well-designed replay buffers. [2604.08706]
- **NExt** — 37.5% reduction via low-rank trajectory extrapolation. [2604.11446]
- **QaRL** — Quantization-aware RL for stable training with FP4/INT4 rollouts. [2604.07853]
- **I-PPO** — Influence-guided data attribution for PPO. [2604.01597]
- **FP4 Explore, BF16 Train** — FP4 rollouts for diffusion model RL. 4.64x acceleration. [2604.06916]

## Key Trend
Three orthogonal efficiency improvements are emerging: (1) async training (Relax), (2) data reuse (experience replay, trajectory extrapolation), and (3) reduced-precision rollouts (QaRL). These are composable — applying all three could yield >5x total speedup.
