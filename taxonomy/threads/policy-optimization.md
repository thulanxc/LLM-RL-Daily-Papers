# Policy Optimization Methods

## Evolution
PPO (2017) → RLHF-PPO (2022) → DPO (2023) → GRPO (2024) → DAPO (2025) → Variants (2026)

## Foundational
- **PPO** — Schulman et al. (2017). Proximal Policy Optimization. Clipped surrogate objective for stable policy updates.
- **RLHF-PPO** — Ouyang et al. (2022). Adapted PPO for language model alignment with human preference reward models.
- **DPO** — Rafailov et al. (2023). Direct Preference Optimization. Reformulates RLHF as supervised learning on preference pairs. [2305.18290]
- **GRPO** — Shao et al. (2024). Group Relative Policy Optimization. Removes critic via group-relative advantages. [2402.03300]
- **DAPO** — ByteDance (2025). Scales GRPO with Clip-Higher, Dynamic Sampling, Token-Level PG Loss. [2503.14476]
- **Dr. GRPO** — (2025). Improved GRPO addressing length bias and variance issues. [2503.20783]
- **REINFORCE++** — Hu (2025). Simplified RL baseline for LLMs. [2501.03262]

## Recent (April 2026)
- **SKPO** — Skip-Connected Policy Optimization for credit assignment. [2604.08690]
- **SPPO** — Sequence-Level PPO for long-horizon reasoning. [2604.08865]
- **TEPO** — Token-Level Policy Optimization linking group rewards to tokens. [2604.12736]
- **Policy Split** — Dual-mode entropy regularization. [2604.11510]
- **TPO** — Target Policy Optimization unifying PG/PPO/GRPO/DPO. [2604.06159]
- **StaRPO** — Stability-augmented with ACF + Path Efficiency. [2604.08905]
- **DDO-RM** — Distributionally guided preference optimization. [2604.11119]
- **DRTO** — Distributionally robust token optimization. [2604.08577]
- **PIPO** — Policy improvement with retrospective verification. [2604.00860]

## April 17, 2026 additions
- **PreRL / Dual Space RL** — First RL on pre-train edge distribution `P(y)` instead of `P(y|x)`. Negative-Sample Reinforcement is 14.89× better for transition thoughts, 6.54× for reflection. [2604.14142]
- **CAPO** — Calibration-Aware Policy Optimization. Logistic AUC surrogate + uncertainty-aware advantage. Breaks accuracy-calibration trade-off in GRPO. [2604.12632]
- **SPO (MM-Doc-R1)** — Similarity-based Policy Optimization. Per-state similarity-weighted baselines replace GRPO's shared-initial-state baseline in multi-turn. [2604.13579]

## April 19, 2026 additions
- **IG-Search** — Step-level reward from Information Gain between real retrieval and counterfactual random retrieval (gold-answer log-prob). Training-free per-token advantage modulation inside GRPO for search agents. +1.6 EM over trajectory-level MR-Search. [2604.15148]
- **CW-GRPO** — Contribution-Weighted GRPO. LLM judge assigns per-round contribution scores; outcome advantages are rescaled (not replaced) by these scores. Preserves group-relative unbiasedness while amplifying informative rounds. +6.3% on Qwen3-1.7B. [2604.14267]
- **GFT** — Group Fine-Tuning. SFT reinterpreted as PG with extremely sparse implicit reward and unstable IPW. Fixed via Group Advantage Learning + Dynamic Coefficient Rectification; yields SFT policies that transition more smoothly into RL. [2604.14258]
- **VGF** — Value Gradient Flow. Recasts behavior-regularized RL as Optimal Transport from reference distribution to value-optimal distribution, solved via discrete gradient flow. Removes explicit policy parameterization and KL hyperparameter; SOTA on LLM RL and offline RL. [2604.14265]
- **TC-GRPO (RAD-2)** — Temporally Consistent GRPO. Adds temporal smoothing across adjacent rollout steps for long-horizon credit assignment. Primarily for planning but generalizable to long-horizon agentic RL. [2604.15308]
- **TCER** — Triviality-Corrected Endogenous Reward. Adapts unsupervised confidence rewards to open-ended writing using specialist–generalist relative information gain + probability-dependent correction, avoiding triviality collapse. [2604.11522]

## April 20, 2026 additions
- **GroupDPO** — Memory-efficient group-wise DPO via no-grad coefficient precomputation. First practical scaling of DPO to k ≫ 4 on a single H100. [2604.15602]
- **RCFG** — Reward-weighted classifier-free guidance is provably a policy-improvement operator. Test-time-only policy optimization and RL warm-start via distillation. [2604.15577]
- **Flexible Empowerment BoN** — Empowerment relocated from reward to Best-of-N sampler (Tsallis-based). N becomes a test-time exploration-exploitation knob. [2604.15614]

## Key Trend (updated April 20)
The credit-assignment thread has fragmented into four orthogonal design axes: (1) **probability space** (PreRL `P(y)` vs. standard `P(y|x)`); (2) **advantage structure** (CAPO calibration-aware, SPO per-state similarity, TC-GRPO temporal-consistent, MARS² tree-structured group, GroupDPO k≫4 DPO); (3) **process signal injection** (IG-Search per-token log-prob IG inside GRPO vs. CW-GRPO per-round contribution rescaling — training-free signal vs. judge-based signal); (4) **regularization geometry** (VGF Optimal-Transport replacing KL). Meanwhile **GFT** demonstrates the SFT↔RL boundary is fully soluble: SFT is a degenerate PG special case. **April 20's GroupDPO + RCFG + Flexible Empowerment BoN add a fifth axis — *when* policy improvement happens (train-time gradient vs. test-time sampling vs. test-time guidance)**. Combined, SFT / DPO / GRPO / OT / RCFG now appear as instances of a single group-advantage + budget-regularized optimization framework indexed by (group size, regularization geometry, advantage rescaling, probability space, update locus).
