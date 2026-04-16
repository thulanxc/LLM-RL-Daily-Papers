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

## Night Edition (April 16, late-night) Additions
- **SandMLE** [2604.04872] — Synthetic micro-environments for ML engineering agents. Training/test data constrained to 50–200 samples, ≤15s execution, **13× speedup**. First time trajectory-level on-policy RL becomes viable in MLE domain. 20.3%–66.9% medal-rate improvement on MLE-bench-lite.
- **Frontier-Eng** [2604.12290] — Not strictly infra, but provides industrial-grade simulator / verifier infrastructure with continuous rewards + hard feasibility constraints across 47 engineering tasks.
- **PTE (Prefill Token Equivalents)** [2604.05404] — Hardware-aware efficiency metric unifying internal reasoning + external tool-use cost, explicitly accounting for KV-Cache eviction and long-tool-response.
- **Adaptive Simulation Experiment** [2604.08779] — Policy-identification (vs. policy-optimization) as a cheaper alternative: Thompson-Sampling-based pairwise comparisons for best-of-N policy selection with PAC guarantees.

## Key Trend (updated)
Four orthogonal efficiency directions are now emerging:
1. **Async training** (Relax)
2. **Data reuse** (experience replay, NExt trajectory extrapolation)
3. **Reduced-precision rollouts** (QaRL, FP4 Explore)
4. **Synthetic micro-environments** (SandMLE, MathAgent synthesis) — trade data scale for structural complexity

These are composable — applying all four could yield >10× total speedup for domains like MLE that previously seemed intractable for on-policy RL.

**Night-edition meta-insight**: The PTE metric signals a paradigm shift — RL research now must include *hardware-aware* efficiency in its design loop, not just algorithmic optimality.
